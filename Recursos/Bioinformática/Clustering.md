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

## Cuidados

- Un cluster puede reflejar un [[Batch effect]] y no biología. Si los clusters coinciden con las muestras, hay un problema.
- Un cluster puede ser un artefacto de [[Control de calidad en scRNA-seq]] insuficiente: dobletes y células muertas se agrupan entre sí.
- Un cluster puede corresponder a un [[Estado celular]] y no a un [[Tipo celular]].

## Siguiente paso

[[Anotación de tipos celulares]] — ponerle nombre biológico a cada cluster.

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
