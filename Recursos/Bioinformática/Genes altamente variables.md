---
tags: [concepto, bioinformática, single-cell, pipeline]
area: Bioinformática
aliases: [HVG, HVGs, highly variable genes, selección de features, feature selection]
---

# Genes altamente variables (HVG)

Paso de **selección de features** del pipeline de [[scRNA-seq]]: de los ~20.000–25.000 genes medidos se conservan solo los que varían entre células **más de lo esperado por su nivel de expresión**. Son los que contienen la información sobre tipos y estados celulares; el resto (genes casi siempre en cero o de expresión constante) aporta sobre todo ruido.

## Dónde está en el pipeline

```
Filtrado de células → Normalización → Selección de HVG → PCA → Clustering / UMAP
```

En el esquema de la clase aparece como *Feature Selection*: un gráfico de **dispersión génica vs expresión media**, con una curva de tendencia y los HVG marcados en rojo por encima de ella.

## Por qué no alcanza con la varianza cruda

En datos de conteo, la varianza **crece con la media**: un gen muy expresado siempre va a parecer "variable". Por eso se modela la relación media–varianza y se eligen los genes que se apartan de la curva.

| Herramienta | Cómo elige los HVG (según [[Slovin et al 2021 - scRNA-seq analysis a step-by-step overview\|Slovin et al. 2021]]) |
|---|---|
| **Scanpy** | Agrupa genes por expresión media y elige los de mayor razón varianza/media en cada grupo |
| **Seurat** | Ajusta la relación media–varianza con regresión polinomial local, estandariza y calcula la varianza de cada gen |
| **Monocle 3** | No tiene este paso |
| **gf-icf** | Lo incorpora en la normalización (frecuencia inversa en células) |

Valor típico: **1.000–5.000 HVG**, según el tamaño del dataset. Ver [[Seurat y Scanpy]].

## Qué gana el análisis

- Baja la [[Alta dimensionalidad]] antes del [[PCA]] y acelera todo lo que sigue.
- Mejora la separación en [[Clustering]] y [[UMAP]].
- En integración entre especies solo se pueden usar genes **ortólogos**: los no homólogos, si entran como HVG, hacen que las células se agrupen por especie → [[Shafer 2019 - Cross-species analysis of scRNAseq data]].

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
- [[Shafer 2019 - Cross-species analysis of scRNAseq data]] *(lectura)*
- [[Slovin et al 2021 - scRNA-seq analysis a step-by-step overview]] *(lectura)*
