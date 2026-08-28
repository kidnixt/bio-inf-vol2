---
tags: [concepto, bioinformática, desafío]
area: Bioinformática
aliases: [maldición de la dimensionalidad, high dimensionality]
---

# Alta dimensionalidad

> **10k–20k genes a 2–3 dimensiones.**

Tercer desafío bioinformático de la clase. Cada célula de un experimento de [[scRNA-seq]] es un punto en un espacio de **veinte mil dimensiones**, una por gen. Ese espacio tiene propiedades poco intuitivas.

## Por qué es un problema

- **Las distancias pierden significado.** En dimensiones muy altas, todos los puntos tienden a estar aproximadamente a la misma distancia entre sí, lo que degrada cualquier método basado en vecindad — incluido el [[Clustering]].
- **La mayoría de las dimensiones son ruido.** De 20.000 genes, sólo unos pocos cientos varían de forma informativa entre células; el resto aporta ruido y [[Sparsity]].
- **No se puede visualizar.**

## La respuesta

[[Reducción dimensional]]: proyectar a un espacio de decenas de dimensiones con [[PCA]] y luego a 2 con [[UMAP]] o t-SNE. El paso previo habitual es seleccionar los **genes altamente variables** (HVGs), reduciendo de 20.000 a ~2.000 antes de empezar.

> [!warning]
> Toda reducción **descarta información**. Un [[UMAP]] es una caricatura útil, no una representación fiel: las distancias entre clusters y sus tamaños relativos no son interpretables.

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
