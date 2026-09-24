---
tags: [lectura, modulo-3, PLM, eficiencia]
area: Lecturas
tipo: preprint (arXiv)
autores: Ahmed Elnaggar, Hazem Essam, Wafaa Salah-Eldin, Walid Moustafa, Mohamed Elkerdawy, Charlotte Rochereau, Burkhard Rost
año: 2023
revista: arXiv:2301.06568
doi: 10.48550/arXiv.2301.06568
aliases: [Elnaggar 2023, Ankh paper, "Ankh - Optimized Protein Language Model Unlocks General-Purpose Modelling"]
---

# Elnaggar et al. (2023) — *Ankh: Optimized Protein Language Model Unlocks General-Purpose Modelling*

> [!info] Ficha de la lectura
> **Tipo:** preprint de arXiv
> **Autores:** Elnaggar y Rost (TUM), con Proteinea Inc. y Columbia — **el mismo primer autor y el mismo senior author que [[Elnaggar et al 2021 - ProtTrans|ProtTrans]]**
> **Clase asociada:** [[Modelos de lenguaje de proteínas y embeddings proteicos]] (clase 9)
> **PDF:** [[Elnaggar et al 2023 - Ankh.pdf]]

## En una frase

El contrapunto a la narrativa del *scaling*: en vez de agrandar el modelo, **optimizarlo para proteínas** — y alcanzar el estado del arte con **menos del 10 %** de los parámetros de pre-entrenamiento, **menos del 7 %** de los de inferencia y **menos del 30 %** de dimensión de embedding.

## Por qué leerla después de la clase

La clase lo usa como la diapositiva "¿Más grande, o mejor diseñado?" y lo conecta con el resultado local de Juan Diego Puglia (el mejor modelo fue **ESM-C 300m**, el más chico). El paper es donde ese argumento está desarrollado, y tiene más filo del que la diapositiva deja ver: **viene del grupo que antes gastó 5.616 GPUs**.

---

## 1. El argumento

> "As opposed to scaling-up protein language models, we seek improving performance via **protein-specific optimization**."

El paper acepta que la proporcionalidad entre tamaño y riqueza de las representaciones está validada, pero prioriza **accesibilidad**, y ataca el problema con optimización guiada por conocimiento: más de **veinte experimentos** sobre estrategia de enmascarado, arquitectura y datos de pre-entrenamiento.

Es la primera vez en la genealogía de la clase que alguien discute el eje que todos los demás dan por sentado.

## 2. Los resultados

Ankh y Ankh-base comparados contra ProtT5-XL-U50, [[ESM-1b y ESM-2|ESM-1b, ESM-2 650M, ESM-2 3B y ESM-2 15B]] en un abanico de tareas de estructura y función:

| Tarea | Ankh vs. el resto |
|---|---|
| Estructura secundaria (CASP12 / CASP14) | 83,8 % / 77,6 % — a la par o mejor |
| Predicción de contactos (ProteinNet L/1) | **49,0 %** contra 30,0 % de ESM-2 650M |
| *Fold prediction*, fluorescencia, solubilidad, GB1, localización | Al tope o empatado |

El salto grande está en **contactos**, que es justamente la tarea donde la estructura emergente se mide más directamente.

## 3. La parte generativa

Ankh también genera variantes de proteínas, en dos escalas de datos: **High-N** (afinado sobre una familia) y **One-N** (una sola secuencia de partida). Afinado sobre variantes naturales de **malato deshidrogenasa (MDH)**, genera 500 secuencias a tres temperaturas (1,0 / 1,5 / 2,0) y compara su **entropía de Shannon por posición** contra el MSA de los datos de afinado:

- El error cuadrático medio entre la entropía natural y la generada es **0,1 / 0,09 / 0,08**, con picos y valles casi en las mismas posiciones.
- Las secuencias generadas llegan a identidades tan bajas como **70 %** (T = 1,0) y **55 %** (T = 2,0) respecto de las originales.

Es decir: **conserva las regiones conservadas e introduce diversidad en las variables**. Y con solo 500 secuencias generadas —menos del 3 % de las 16.706 naturales— reproduce la distribución.

> [!tip] Conexión con la tesis de Johny
> Esta sección es directamente relevante para el capítulo 1: es un **protocolo de evaluación de un PLM generativo** con un criterio distinto de la verosimilitud y del pLDDT — comparar la **entropía por posición** contra un MSA de referencia. Y MDH es una de las familias de Johnson et al. 2024.

## 4. Qué aporta respecto de la clase

- **La tabla de benchmarks completa**, que permite ver dónde Ankh gana y dónde empata, en vez de la afirmación general.
- **Las recomendaciones de datos**: pre-entrenar con **UniRef50** resultó superior a UniRef90, UniRef100 y BFD, por menor redundancia. Un detalle práctico que explica por qué tantos modelos llevan `UR50` en el nombre.
- **Las limitaciones declaradas**, incluida una honesta: no encontraron una fórmula única para definir "mejor", y los modelos experimentales se entrenaron solo dos épocas.
- **El encuadre ético/práctico**: los autores dedican el trabajo a promover la accesibilidad. Es el mismo punto con el que la clase cierra — *entrenar es de pocos; usar es de casi todos*.

## Conceptos del vault

[[Modelo de lenguaje de proteínas]] · [[ProtT5 y ProtBERT]] · [[ESM-1b y ESM-2]] · [[Embedding]] · [[Masked language modeling]] · [[Mapa de contactos]] · [[Alineamiento múltiple de secuencias]] · [[UniProt]]

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
- [[Módulo 3 - MOC]]
