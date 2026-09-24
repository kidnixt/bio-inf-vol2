---
tags: [lectura, modulo-3, PLM, estructura]
area: Lecturas
tipo: methods article
autores: Michael Heinzinger, Konstantin Weissenow, Joaquin Gomez Sanchez, Adrian Henkel, Milot Mirdita, Martin Steinegger, Burkhard Rost
año: 2024
revista: NAR Genomics and Bioinformatics 6(4), lqae150
doi: 10.1093/nargab/lqae150
aliases: [Heinzinger 2024, ProstT5 paper, "Bilingual language model for protein sequence and structure"]
---

# Heinzinger et al. (2024) — *Bilingual language model for protein sequence and structure*

> [!info] Ficha de la lectura
> **Tipo:** *Methods Article* — *NAR Genomics and Bioinformatics* (acceso abierto)
> **Autores:** grupo de **Rost** (TUM) junto con **Steinegger** (Seoul National University) — es decir, los autores de [[Heinzinger et al 2019 - SeqVec|SeqVec]]/[[Elnaggar et al 2021 - ProtTrans|ProtTrans]] **más** los de [[van Kempen et al 2024 - Foldseek|Foldseek]]
> **Clase asociada:** [[Modelos de lenguaje de proteínas y embeddings proteicos]] (clase 9)
> **PDF:** [[Heinzinger et al 2024 - ProstT5.pdf]]
> **Modelo:** `huggingface.co/Rostlab/ProstT5`

## En una frase

El paper de **[[ProstT5]]**: afinar [[ProtT5 y ProtBERT|ProtT5]] para **traducir en los dos sentidos** entre la secuencia de aminoácidos y el [[Alfabeto 3Di|alfabeto 3Di]] de Foldseek, modelando así las dos naturalezas de una proteína —1D y 3D— **en un solo modelo**.

## Por qué leerla después de la clase

La clase muestra la Figura 1 (arquitectura, pre-entrenamiento en dos etapas, inferencia) y los dos tokens de control. El paper aporta el **encuadre histórico** —es explícitamente un trabajo *"post-AlphaFold2"*— y el detalle del dataset, que es donde está la jugada.

---

## 1. La oportunidad que aprovecha

Dos revoluciones ocurrieron en paralelo y sin tocarse:

- Los **PLMs** aprendieron a extraer información evolutiva directamente de la secuencia, sin recuperar homólogos.
- **AlphaFold2** llevó la predicción de estructura a calidad casi experimental, y para enero de 2024 [[AlphaFold DB]] ya tenía más de **214 millones** de estructuras.

La propuesta: usar un PLM para modelar **ambas modalidades a la vez**, codificando las estructuras como cadenas 1D con el 3Di.

## 2. El método

| | |
|---|---|
| Datos | Conjunto **no redundante** construido a partir de AlphaFoldDB |
| Punto de partida | **ProtT5** ya entrenado (no se entrena desde cero) |
| Tarea de afinado | Traducir entre 3Di y aminoácidos |
| Tokens de control | `<AA2fold>` (secuencia → forma) y `<fold2AA>` (forma → secuencia, [[Inverse folding\|inverse folding]]) |

Que se parta de ProtT5 y no de cero es lo que hace el trabajo viable, y también lo que justifica que ProtT5 fuera *encoder-decoder*: la arquitectura ya estaba pensada para traducir.

## 3. El resultado

**Tres órdenes de magnitud de aceleración** para derivar el 3Di, comparado con predecir la estructura y extraerlo de ahí. Y mejor rendimiento en tareas posteriores relacionadas con estructura.

La conclusión que el paper destaca, y que la clase recoge: esto va a ser **crucial para buscar en bases metagenómicas con la sensibilidad de una comparación estructural** — es decir, combinar el alcance de la secuencia con la sensibilidad de la forma.

## 4. Qué aporta respecto de la clase

- **El contexto "era post-AlphaFold2"**: el paper se posiciona como una forma de que los PLMs *aprovechen* la revolución estructural, no compitan con ella. Es una lectura distinta de la habitual (PLM vs. AlphaFold).
- **El detalle del dataset no redundante desde AFDB**, que es lo que evita que el modelo memorice.
- **La advertencia de nombres** que la clase repite: **ProtT5** lee secuencia (1D), **ProstT5** lee secuencia *y* estructura (3D). Mismo grupo, una letra de diferencia.
- Lo que abre: [[Bouras et al 2026 - Phold|Phold]] es la aplicación directa, y el trabajo de tesis de Juan Diego Puglia usa ProstT5 como uno de sus tres extractores de [[Embedding|embeddings]].

## Conceptos del vault

[[ProstT5]] · [[Alfabeto 3Di]] · [[Foldseek]] · [[ProtT5 y ProtBERT]] · [[Inverse folding]] · [[AlphaFold DB]] · [[AlphaFold]] · [[Homología remota]] · [[Modelo de lenguaje de proteínas]]

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
- [[Módulo 3 - MOC]]
