---
tags: [concepto, bioinformática, análisis]
area: Bioinformática
aliases: [clusters, clúster, agrupamiento]
---

# Clustering

Agrupar células con perfiles de [[Expresión génica]] similares. Es el paso que convierte una nube de puntos en poblaciones discretas sobre las que se puede razonar.

## Cómo se hace en single cell

El estándar no es k-means sino **clustering sobre grafo**:

```
PCA → grafo de k vecinos más cercanos (kNN) → detección de comunidades (Leiden / Louvain)
```

Se busca conjuntos de células más conectadas entre sí que con el resto. Es un enfoque adecuado porque no asume número de clusters ni forma esférica.

## El parámetro incómodo: la resolución

El algoritmo tiene un parámetro de resolución que determina **cuántos clusters salen**. Subirlo produce más grupos más finos; bajarlo, menos y más gruesos. No hay un valor "correcto" derivable de los datos.

Esto conecta directamente con el desafío de la [[Identidad celular]]: la jerarquía `[Clase General] ➜ [Subclase] ➜ [Clúster]` que la clase muestra para el [[Tejido cerebral]] no es un hecho de la naturaleza, es en buena parte una consecuencia de dónde se fijó la resolución.

## Alternativas y el valor por defecto

[[Slovin et al 2021 - scRNA-seq analysis a step-by-step overview|Slovin et al. (2021)]] compara tres familias: **k-means** (rápido, pero hay que fijar *k*), **jerárquico** (dendrograma; lento en datasets grandes) y **detección de comunidades** (escala a millones de células). En el grafo k-NN, el peso de cada arista se refina por **similitud de Jaccard** (vecinos compartidos) y Louvain maximiza la **modularidad**. Usan resolución **0,5** como compromiso razonable. Ver [[Seurat y Scanpy]].

En la figura de la clase, el clustering se hace **en el espacio de ~50 PCs** (grafo k-NN con *k* = 3 en el dibujo), y [[t-SNE]]/[[UMAP]] solo se usan para visualizar el resultado.

## Cuidados

- Un cluster puede reflejar un [[Batch effect]] y no biología. Si los clusters coinciden con las muestras, hay un problema.
- Un cluster puede ser un artefacto de [[Control de calidad en scRNA-seq]] insuficiente: dobletes y células muertas se agrupan entre sí.
- Un cluster puede corresponder a un [[Estado celular]] y no a un [[Tipo celular]].

## Siguiente paso

[[Anotación de tipos celulares]] — ponerle nombre biológico a cada cluster.

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
- [[Shafer 2019 - Cross-species analysis of scRNAseq data]] *(lectura)*
- [[Slovin et al 2021 - scRNA-seq analysis a step-by-step overview]] *(lectura)*
- [[Stuart and Satija 2019 - Integrative single-cell analysis]] *(lectura)*
