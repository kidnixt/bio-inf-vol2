---
tags: [concepto, bioinformática, análisis]
area: Bioinformática
aliases: [análisis de componentes principales, principal component analysis]
---

# PCA (Análisis de Componentes Principales)

Método **lineal** de [[Reducción dimensional]]. Encuentra los ejes (componentes principales) a lo largo de los cuales los datos varían más, y reexpresa cada célula como una combinación de esos ejes.

## Su papel en el pipeline de single cell

Es el paso **estructural** del análisis, aunque no sea el que se ve en las figuras:

- Reduce de ~2.000 genes altamente variables a ~30–50 componentes.
- Funciona como filtro de ruido: la señal biológica correlacionada se concentra en las primeras componentes; el ruido no correlacionado se reparte entre las últimas.
- Es la entrada del grafo de vecinos sobre el que corren [[Clustering]] y [[UMAP]].

## Por qué no alcanza para visualizar

El PCA es lineal, y la estructura de un tejido no lo es. Las dos primeras componentes de un dataset de [[scRNA-seq]] normalmente separan sólo el eje de variación más grosero y mezclan todo lo demás. Por eso se lo usa como paso intermedio y se delega la visualización a métodos no lineales como [[UMAP]] o t-SNE.

## En bulk

En [[Bulk RNA-seq]] el PCA sí se usa directamente para visualizar: con 6–10 muestras, un gráfico PC1 vs PC2 es la herramienta estándar para ver si las muestras se agrupan por condición o por [[Batch effect]].

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
