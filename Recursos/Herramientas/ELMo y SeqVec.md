---
tags: [herramienta, modelo, PLM, embeddings, deep-learning]
area: Herramientas
aliases: [ELMo, SeqVec, biLSTM, LSTM bidireccional]
---

# ELMo y SeqVec

El paso de los [[Embedding|embeddings]] **fijos** a los **contextuales**, primero en lenguaje natural (ELMo) y después en proteínas (SeqVec).

## ELMo — la arquitectura

Peters et al. (2018), Allen AI, *Deep contextualized word representations* (arXiv:1802.05365). SeqVec no la inventa: **la aplica** a proteínas.

**Dos LSTM, entrenadas juntas.** Una pasada hacia adelante y otra hacia atrás. Se entrenan de forma conjunta (comparten capa de entrada y de salida), pero **cada dirección tiene sus propios parámetros**.

**El vector se concatena.** En cada posición se pegan las dos direcciones: `[→h ; ←h]`. **No es una sola pasada que ve todo**, son dos recorridos unidos al final — y esa es exactamente la diferencia con el [[Masked language modeling|enfoque masked]] del [[Transformer]].

**Lo que lo hizo distinto.** No usa solo la última capa: **combina todas** con pesos que aprende cada tarea. Las capas bajas capturan sintaxis, las altas semántica.

| Los números | |
|---|---|
| Capas | 2 biLSTM por dirección |
| Unidades | 4096, con proyección a 512 |
| Representaciones por token | 5 (entrada + 2 adelante + 2 atrás) |
| Entrada | **por caracteres**, no por palabras |

> **Entrada por caracteres:** como lee letra por letra, ELMo puede representar palabras que **nunca vio**. En proteínas es todavía más natural: el "vocabulario" son 20 letras.

## SeqVec — la aplicación a proteínas

Heinzinger et al. (2019), *BMC Bioinformatics* 20:723 — el mismo autor que después haría [[ProstT5]].

- **Ya no hay [[K-mer|3-meros]]:** se lee la secuencia completa.
- **El vector depende del entorno:** cada residuo mira a sus vecinos.
- **Bidireccional**, no *masked*.

**El hallazgo de la figura:** en una proyección [[t-SNE]] coloreada por localización celular, **los embeddings sin entrenar ya agrupan proteínas por función** — una señal que el modelo nunca recibió. Entrenarlo solo mejora la separación.

**El contexto se traduce en rendimiento**, con la misma tarea y la misma secuencia de entrada:

| Tarea | Resultado |
|---|---|
| Estructura secundaria (Q3) | Cerca de los mejores métodos, **sin [[Alineamiento múltiple de secuencias\|alineamientos]]** |
| Predicción de membrana | **77,6** ([[ProtVec]]) → **92,3** (DeepLoc con SeqVec) |

Su límite es el de toda arquitectura recurrente: lee **en orden**, no se paraleliza, y lo lejano se desvanece. Eso lo resuelve el [[Transformer]].

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
