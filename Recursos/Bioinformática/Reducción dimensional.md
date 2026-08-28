---
tags: [concepto, bioinformática, análisis]
area: Bioinformática
aliases: [dimensionality reduction, reducción de dimensionalidad]
---

# Reducción dimensional

Proyectar las células desde el espacio de ~20.000 genes a un espacio de pocas dimensiones, conservando la estructura relevante. Es la respuesta al desafío de la [[Alta dimensionalidad]].

## El pipeline estándar

```
Matriz cruda (20.000 genes)
   ↓ normalización + log-transformación
   ↓ selección de genes altamente variables (HVGs)  →  ~2.000 genes
   ↓ PCA                                            →  ~30-50 componentes
   ↓ grafo de vecinos (kNN)
   ↓ UMAP / t-SNE                                   →  2 dimensiones (visualización)
```

Cada paso descarta información deliberadamente. El [[PCA]] hace el trabajo estructural pesado; el [[UMAP]] es sólo la capa de visualización.

## Para qué sirve

- **Denoising**: las primeras componentes principales capturan la señal estructurada y descartan buena parte del ruido y la [[Sparsity]].
- **Eficiencia**: el [[Clustering]] y la búsqueda de vecinos operan sobre 30-50 dimensiones en lugar de 20.000.
- **Visualización**: permite ver de un golpe la composición de un tejido.

> [!warning] La trampa de la visualización
> Un [[UMAP]] es una caricatura. Las **distancias entre clusters** y sus **tamaños relativos** no son interpretables, y la posición de un cluster respecto de otro tampoco. Sólo la agrupación local es confiable.

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
- [[Biología espacial - mapeando la expresión génica a su entorno]]
