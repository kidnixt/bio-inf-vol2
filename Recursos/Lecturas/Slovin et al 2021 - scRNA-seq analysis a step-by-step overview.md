---
tags: [lectura, modulo-1, single-cell, pipeline]
area: Lecturas
tipo: capítulo de libro / tutorial
autores: Shaked Slovin, Annamaria Carissimo, Francesco Panariello, Antonio Grimaldi, Valentina Bouché, Gennaro Gambardella, Davide Cacchiarelli
año: 2021
revista: "Methods in Molecular Biology vol. 2284 — RNA Bioinformatics (Springer)"
doi: 10.1007/978-1-0716-1307-8_19
aliases: [Slovin 2021, Slovin et al. 2021, scRNA-seq step-by-step]
---

# Slovin et al. (2021) — *Single-Cell RNA Sequencing Analysis: A Step-by-Step Overview*

> [!info] Ficha de la lectura
> **Tipo:** capítulo metodológico / tutorial (*Methods in Molecular Biology*, Springer)
> **Clase asociada:** [[Aproximaciones ómicas con resolución de célula única]] (clase 1)
> **PDF:** [[Slovin et al 2021 - scRNA-seq analysis a step-by-step overview.pdf]]
> **Código:** los autores comparan cuatro pipelines listos para usar — **Seurat** (R), **Scanpy** (Python), **Monocle 3** (R) y **gf-icf** (R), ver [[Seurat y Scanpy]] — — sobre un subset del dataset público *Tabula Muris* (10x Chromium).

## En una frase

Es el "manual de usuario" de la diapositiva *¿Qué sigue?* de la clase: recorre, paso por paso y con umbrales concretos, el pipeline canónico de [[scRNA-seq]] desde las lecturas crudas hasta clusters anotados y trayectorias.

## Por qué leerla después de la clase

La clase muestra el pipeline como una figura (secuenciación → cuantificación → filtrado → normalización → selección de features → reducción dimensional → clustering → downstream). Este capítulo explica **qué decisión se toma en cada caja y con qué criterio**, que es justo lo que las diapositivas no dicen.

---

## 1. El flujo de laboratorio (seis pasos)

1. Suspensión de células individuales viable (disociación).
2. Evaluar viabilidad.
3. Si la viabilidad es **< 90 %**, eliminar células muertas (gradiente de densidad, FACS o sorting magnético): las células lisadas meten ruido.
4. **Barcoding** de cada transcriptoma — el paso que distingue al single cell del [[Bulk RNA-seq|bulk]].
5. Generación de ADNc.
6. Biblioteca de secuenciación (con índices de muestra para multiplexar corridas).

### Microfluídica y estadística de Poisson

En [[Microfluídica|gotas]] ([[10x Genomics|Chromium]], inDrop, Drop-seq) cada bead lleva primers con una estructura de tres partes: [[Barcode celular]] (común a todo el bead) + [[UMI]] (distinto en cada primer) + poli-T (captura la cola poli-A → extremo 3').

- Si el encapsulado sigue una **distribución de Poisson**, que coincidan *una* célula y *un* bead en la misma gota es un evento de doble Poisson → muchas gotas vacías.
- inDrop y Chromium usan beads deformables empaquetados para lograr carga **sub-Poisson** (~80 % de gotas con un solo bead).

| Plataforma | Células capturadas del input | Input necesario |
|---|---|---|
| Drop-seq | 5–12 % | > 2 × 10⁵ |
| inDrop | ~75 % | 2 × 10³–10⁴ |
| Chromium (10x) | ~65 % | > 10³ |

Dos limitaciones de fondo: se recupera solo **1–5 % de los transcriptos** de cada célula (efecto *drop-out* → [[Sparsity]]) y el costo de las plataformas comerciales.

---

## 2. El flujo computacional, paso por paso

| Paso | Qué se hace | Detalles y umbrales del capítulo |
|---|---|---|
| **Demultiplexado** | BCL → [[FASTQ]] por muestra | `cellranger mkfastq` |
| **Alineamiento y cuantificación** | Mapear, asignar a barcode, contar UMIs | CellRanger `count` o **STARsolo**: corrigen barcodes contra una *whitelist* (1 error de edición), mapean con STAR, corrigen y deduplican UMIs, cuentan UMIs únicos por gen. Recomiendan referencia **genómica** (no transcriptómica) para descartar lecturas fuera de blanco |
| **Gotas vacías** | Separar células reales de gotas con ARN ambiente | **EmptyDrops** (modelo Dirichlet-multinomial + permutaciones + FDR) |
| **QC de células** | Filtrar outliers | Las tres covariables de la clase: genes por barcode, UMIs por barcode y **fracción mitocondrial** (descartar > **10 %**, pero ajustarlo al modelo: células tumorales o muy respiratorias tienen más ARN mitocondrial) → [[Control de calidad en scRNA-seq]], [[Genes mitocondriales]] |
| **Multipletes** | Dos células en una gota → conteos anómalamente altos | Outliers de profundidad, **por muestra** por separado |
| **Filtrado de genes** | Sacar genes casi siempre en cero | Umbral fijo de nº de células donde se detecta |
| **Normalización** | Hacer comparables células con distinta profundidad | **CPM + log** (Seurat, Scanpy, Monocle); gf-icf usa TF-IDF y norma L2. Los métodos de bulk (TMM, DESeq) se sesgan por la inflación de ceros. La normalización **no** corrige [[Batch effect]] (ComBat funciona bien en datasets simples) |
| **Selección de features** | Quedarse con genes informativos | 1.000–5.000 **[[Genes altamente variables\|HVG]]**, modelando la relación media-varianza |
| **Reducción lineal** | [[PCA]] | 10–50 PCs, elegidos con el **gráfico de codo** (*elbow plot*); ante la duda, quedarse con más |
| **Visualización** | [[t-SNE]] / [[UMAP]] | t-SNE preserva estructura local pero **las distancias entre clusters no significan nada**; UMAP preserva local y global y escala mejor |
| **[[Clustering]]** | Agrupar en el espacio de PCs | k-means (hay que saber *k*), jerárquico (lento), o **detección de comunidades** en un grafo k-NN refinado por Jaccard → **Louvain** optimizando modularidad. Parámetro de **resolución** (usan 0,5): más alto = más clusters, más chicos |
| **[[Expresión diferencial]] y anotación** | Genes marcadores de cada cluster vs el resto | Wilcoxon (rápido); MAST y bayesianos modelan drop-outs pero no escalan; después [[Gene Ontology\|GO]] / GSEA → [[Anotación de tipos celulares]] |
| **Trayectorias** | Ordenar células en un proceso continuo | [[Pseudotiempo]] (Monocle introdujo el concepto; hoy > 100 métodos); **[[RNA velocity]]** agrega dirección |

> [!tip] Chequeos rápidos de las notas del capítulo
> - Menos de **70 %** de lecturas asociadas a barcodes sugiere mucho ARN ambiente (lisis o lavados insuficientes).
> - Las lecturas bien mapeadas al genoma deberían superar el **80 %**.
> - Los umbrales de QC tienen que ser **lo más permisivos posible** para no perder poblaciones raras.

### Comparación de los cuatro pipelines

Con el índice de Jaccard entre clusters, los cuatro dan particiones biológicamente coherentes: las células de un mismo cluster pertenecen al mismo linaje, con distinto nivel de granularidad según la resolución elegida. La elección de herramienta pesa menos que entender cada paso.

---

## 3. Hacia dónde va (según los autores)

- Pipelines capaces de integrar **multiómica** (ADN, ChIP, ATAC) → [[Integración de datos multiómicos]].
- La [[Transcriptómica espacial]] como dimensión adicional para separar subpoblaciones en sistemas heterogéneos (p. ej. organoides) → [[Biología espacial - mapeando la expresión génica a su entorno|clase 2]].
- Medicina de precisión apoyada en [[Machine Learning]].

## Conceptos del vault

[[scRNA-seq]] · [[Barcode celular]] · [[UMI]] · [[Microfluídica]] · [[10x Genomics]] · [[FASTQ]] · [[Alineamiento de secuencias]] · [[Matriz de conteo]] · [[Control de calidad en scRNA-seq]] · [[Genes mitocondriales]] · [[Sparsity]] · [[Batch effect]] · [[Reducción dimensional]] · [[Genes altamente variables]] · [[PCA]] · [[t-SNE]] · [[UMAP]] · [[Clustering]] · [[RNA velocity]] · [[Seurat y Scanpy]] · [[Expresión diferencial]] · [[Gene Ontology]] · [[Anotación de tipos celulares]] · [[Pseudotiempo]]

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
- [[Módulo 1 - MOC]]
