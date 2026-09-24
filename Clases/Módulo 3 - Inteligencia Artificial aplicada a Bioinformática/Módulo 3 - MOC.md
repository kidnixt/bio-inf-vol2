---
tags: [MOC, modulo-3]
---

# Módulo 3 — Inteligencia Artificial aplicada a Bioinformática

Índice del módulo. Curso **Fronteras y Perspectivas en Bioinformática** — Universidad ORT, 2026.

## Clases

| # | Clase | Docente | Material del curso |
|---|---|---|---|
| 6 | [[Métodos para el diseño computacional de fármacos]] | [[Andrés Ballesteros]] | [[Diapositivas - Métodos para el diseño computacional de fármacos.pdf\|diapositivas]] |
| 7 | *(sin material todavía)* | — | — |
| 8 | *(sin material todavía)* | — | — |
| 9 | [[Modelos de lenguaje de proteínas y embeddings proteicos]] | [[Ignacio Ferrés]] | [[Diapositivas - Modelos de lenguaje de proteínas y embeddings proteicos.pdf\|diapositivas]] |
| 10 | *(sin material todavía)* | — | — |

> [!note] Pendiente
> Ninguna de las dos clases cargadas tiene PDF de resumen del curso ni lecturas asignadas. De las clases 7, 8 y 10 no hay material. Cuando llegue, va en `Módulo 3 - Inteligencia Artificial aplicada a Bioinformática/Clase N - <tema>/` y el resumen en esta carpeta.

## El hilo conductor del módulo

Los dos módulos anteriores fueron sobre **generar datos** ([[Módulo 1 - MOC|Módulo 1]]: célula única, espacio, lecturas largas) y sobre **modelar el sistema** ([[Módulo 2 - MOC|Módulo 2]]: modelos metabólicos a escala genómica). Este módulo es sobre **aprender representaciones**: dejar que el modelo descubra cómo describir una molécula o una proteína, en vez de decidirlo a mano.

Las dos clases cargadas hacen exactamente el mismo movimiento, en dominios distintos:

| | Clase 6 — moléculas pequeñas | Clase 9 — proteínas |
|---|---|---|
| **Lo convencional** | Descriptores y *fingerprints* definidos previamente ([[Representaciones moleculares]], [[QSAR]]) | Motivos, perfiles y [[Alineamiento múltiple de secuencias\|MSA]] |
| **Lo aprendido** | Representaciones desde SMILES, grafos y estructuras 3D | [[Embedding\|Embeddings]] de [[Modelo de lenguaje de proteínas\|PLMs]] |
| **Qué desbloquea** | Generación de moléculas, [[Aprendizaje activo\|aprendizaje activo]], predicción de poses y afinidades | Estructura emergente, búsqueda por forma, diseño *de novo* |
| **El límite honesto** | *El [[Función de puntuación\|score]] ordena hipótesis dentro de un protocolo* | *Los PLMs aprenden evolución acumulada, no física* |

Y las dos terminan en la misma frase, dicha de dos maneras:

> **Un buen *score in silico* es una hipótesis, no un resultado.** · *La mesada sigue mandando.*

El puente concreto entre ambas es [[AlphaFold]]: en la clase 6 resuelve *"¿y si la estructura no está en el [[PDB]]?"*; en la clase 9 es el punto de comparación de [[ESMFold]], que hace lo mismo **sin alineamientos**.

## Mapa de conceptos del módulo

### Diseño de fármacos

[[Diseño de fármacos asistido por computadora]] · [[Diseño basado en ligandos]] · [[Diseño basado en estructura]] · [[Descubrimiento y desarrollo de fármacos]] · [[Blanco terapéutico]] · [[ADMET]] · [[Casos de éxito del diseño computacional de fármacos]] · [[Reposicionamiento de fármacos]]

### Métodos de LBDD

[[Similitud química]] · [[Farmacóforo]] · [[QSAR]] · [[Activity cliff]] · [[Representaciones moleculares]] · [[Reglas de drug-likeness]] · [[Virtual screening]]

### Métodos de SBDD

[[Docking molecular]] · [[Función de puntuación]] · [[Dinámica molecular]] · [[Energía libre de unión]] · [[Cribado virtual inverso]] · [[Cofolding]]

### Estructura de proteínas

[[Cristalografía de rayos X]] · [[Modelado por homología]] · [[Threading]] · [[AlphaFold]] · [[Mapa de contactos]] · [[Alfabeto 3Di]] · [[Homología remota]] · [[Inverse folding]]

### Modelos de lenguaje y embeddings

[[Embedding]] · [[One-hot encoding]] · [[Transformer]] · [[Masked language modeling]] · [[Modelo de lenguaje de proteínas]] · [[Aprendizaje activo]] · [[Alineamiento múltiple de secuencias]]

### Modelos y software

[[Word2vec]] · [[ProtVec]] · [[ELMo y SeqVec]] · [[ProtT5 y ProtBERT]] · [[ESM-1b y ESM-2]] · [[ESMFold]] · [[ESM3]] · [[ProstT5]] · [[Foldseek]] · [[Phold]]

### Bases de datos

[[ZINC]] · [[PubChem]] · [[ChEMBL]] · [[BindingDB]] · [[DrugBank]] · [[UniProt]] · [[PDB]] · [[AlphaFold DB]] · [[PDBbind]] · [[ESM Atlas]]

### Biología

[[Homología]] · [[Permutación circular]] · [[Bacteriófago]]

### Personas e instituciones

[[Andrés Ballesteros]] · [[Ignacio Ferrés]] · [[Facultad de Química (UdelaR)]] · [[Institut Pasteur de Montevideo]]

## El problema de los órdenes de magnitud

Un hilo cuantitativo que atraviesa las dos clases: **siempre se puede enumerar mucho más de lo que se puede medir**.

| Qué | Cuánto (corte set. 2026) |
|---|---|
| Moléculas enumerables ([[ZINC]]) | ~5 · 10¹⁰ |
| Compuestos con actividad medida ([[ChEMBL]]) | ~3 · 10⁶ |
| Complejos con estructura **y** afinidad ([[PDBbind]]) | 2,9 · 10⁴ |
| Estructuras predichas ([[AlphaFold DB]] + [[ESM Atlas]]) | ~8 · 10⁸ |
| Estructuras experimentales ([[PDB]]) | 2,6 · 10⁵ |
| Experimentos que se pueden hacer | **10–100** |

Esa asimetría es la que explica el [[Virtual screening|embudo jerárquico]], por qué [[Energía libre de unión|la afinidad sigue siendo difícil]], y por qué [[Foldseek]] tuvo que existir.

## Conexiones con los módulos anteriores

- [[Integración de datos multiómicos]], [[Sparsity]], [[Batch effect]] y [[Anotación de tipos celulares]] son los problemas del [[Módulo 1 - MOC|Módulo 1]] para los que se esperan soluciones de IA.
- El [[Basecalling]] de nanoporos ([[Dorado]]) y la [[Segmentación celular]] ya eran, de hecho, problemas de [[Deep Learning|deep learning]]: en el Módulo 1 la IA **procesa señales**; en este módulo **representa y genera** biología.
- En el [[Módulo 2 - MOC|Módulo 2]], [[Machine Learning]] e IA aparecían como uno de los avances que desbloquean la ingeniería metabólica de sistemas. El [[Ciclo DBTL]] de esa clase es el mismo ciclo *diseñar → sintetizar → medir → aprender* de la clase 6.
- Las lecturas del Módulo 1 ya mostraban ML en uso: clasificadores para anotar tipos celulares ([[Shafer 2019 - Cross-species analysis of scRNAseq data]], [[Stuart and Satija 2019 - Integrative single-cell analysis]]), segmentación con redes neuronales ([[Li and Zhou 2026 - Imaging-based Spatial transcriptomics]]) y deep learning que predice expresión desde la histología ([[Longo et al 2021 - Integrating single-cell and spatial transcriptomics]]).

## Navegación

- Curso completo → [[Fronteras y Perspectivas en Bioinformática - MOC]]
- Módulo anterior → [[Módulo 2 - MOC]]
- Siguiente módulo → [[Módulo 4 - MOC]]
