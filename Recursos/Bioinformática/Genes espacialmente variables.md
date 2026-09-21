---
tags: [concepto, bioinformática, espacial]
area: Bioinformática
aliases: [SVG, SVGs, spatially variable genes]
---

# Genes espacialmente variables (SVGs)

Genes cuya expresión **sigue un patrón en el espacio** del tejido (un gradiente, una capa, una región) en lugar de repartirse al azar. Son el equivalente espacial de los [[Genes altamente variables]] del [[scRNA-seq]]: el primer filtro para encontrar biología en un dato de [[Transcriptómica espacial]].

## Cómo se detectan

- **Enfoque tradicional**: [[Expresión diferencial]] entre regiones definidas de antemano.
- **Métodos estadísticos que usan las coordenadas** ([[Yue et al 2023 - A guidebook of spatial transcriptomics technologies|Yue et al. 2023]]):
  - **SpatialDE** — regresión con procesos gaussianos.
  - **SPARK / SPARK-X** — modelos lineales mixtos generalizados con varios *kernels* espaciales.
  - **trendsceek**, **SOMDE**, **sepal**, etc.
- **Deep learning / grafos**: **SpaGCN** (red convolucional de grafos que combina expresión, posición e histología), **Giotto** (campos aleatorios de Markov).

## Para qué se usan

- Definir [[Spatial domains]] y subregiones del tejido.
- Elegir **paneles de genes** para técnicas de imagen (que solo miden lo que se buscó) — uno de los pasos del flujo de [[Longo et al 2021 - Integrating single-cell and spatial transcriptomics|Longo et al. (2021)]].
- Encontrar gradientes continuos (p. ej. capas corticales o zonación del hígado) que no se reducen a tipos celulares discretos.

## Aparece en

- [[Longo et al 2021 - Integrating single-cell and spatial transcriptomics]] *(lectura)*
- [[Yue et al 2023 - A guidebook of spatial transcriptomics technologies]] *(lectura)*
