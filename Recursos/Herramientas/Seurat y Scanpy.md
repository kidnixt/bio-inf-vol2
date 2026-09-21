---
tags: [herramienta, software, single-cell]
area: Herramientas
aliases: [Seurat, Scanpy, Monocle, Monocle 3, CellRanger, STARsolo]
---

# Seurat y Scanpy

Los dos entornos de análisis de [[scRNA-seq]] más usados: **Seurat** en **R** y **Scanpy** en **Python**. Implementan el pipeline completo que muestra la clase (QC → normalización → [[Genes altamente variables|HVG]] → [[PCA]] → [[Clustering]] → [[UMAP]] → [[Expresión diferencial]]). La clase no los nombra, pero sí menciona que en Uruguay hay servidores con alta RAM para analizar estos datos **en R y Python**.

## Comparación (según [[Slovin et al 2021 - scRNA-seq analysis a step-by-step overview|Slovin et al. 2021]])

| | **Seurat** (R) | **Scanpy** (Python) | **Monocle 3** (R) | **gf-icf** (R) |
|---|---|---|---|---|
| Fuerte en | Tutoriales, herramientas, **integración** | **Escala** (≥ 1 millón de células) | **Trayectorias** / [[Pseudotiempo]] | Datos ralos (modelo TF-IDF del *text mining*) |
| Normalización | CPM + log | CPM + log | CPM + log | TF-IDF + norma L2 |
| HVG | Regresión media–varianza | Varianza/media por bins | — | En la normalización |
| Clustering | Louvain (grafo k-NN) | Louvain | — | Louvain |
| Marcadores | Wilcoxon (y otros) | Wilcoxon (y otros) | Modelo aditivo (VGAM) | Wilcoxon |

Antes de ellos, las lecturas se procesan con **CellRanger** (10x) o **STARsolo**: corrección de barcodes, mapeo, deduplicación de UMIs y conteo → [[Matriz de conteo]].

## Integración de datasets

Seurat incorporó la integración por **CCA** (v2) y por **anclas** de vecinos mutuos (v3), que también sirve para transferir etiquetas de un atlas y para integrar datos espaciales → [[Stuart and Satija 2019 - Integrative single-cell analysis]], [[Integración de datos single cell y spatial]]. En Python, las alternativas equivalentes son Harmony, Scanorama, scVI.

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
- [[Shafer 2019 - Cross-species analysis of scRNAseq data]] *(lectura)*
- [[Slovin et al 2021 - scRNA-seq analysis a step-by-step overview]] *(lectura)*
- [[Stuart and Satija 2019 - Integrative single-cell analysis]] *(lectura)*
