---
tags: [lectura, modulo-1, spatial, herramientas]
area: Lecturas
tipo: mini review
autores: Liangchen Yue, Feng Liu, Jiongsong Hu, Pin Yang, Yuxiang Wang, Junguo Dong, Wenjie Shu, Xingxu Huang, Shengqi Wang
año: 2023
revista: Computational and Structural Biotechnology Journal 21, 940–955
doi: 10.1016/j.csbj.2023.01.016
aliases: [Yue 2023, Yue et al. 2023, A guidebook of spatial transcriptomic technologies, data resources and analysis approaches]
---

# Yue et al. (2023) — *A guidebook of spatial transcriptomic technologies, data resources and analysis approaches*

> [!info] Ficha de la lectura
> **Tipo:** mini review — *Computational and Structural Biotechnology Journal* (acceso abierto)
> **Clase asociada:** [[Biología espacial - mapeando la expresión génica a su entorno]] (clase 2)
> **PDF:** [[Yue et al 2023 - A guidebook of spatial transcriptomics technologies.pdf]]

## En una frase

Una guía de orientación para el campo de la [[Transcriptómica espacial]]: clasifica **22 tecnologías** en cuatro familias, reúne **791 datasets** de 479 artículos (2013–2022) y ordena **70 herramientas** de análisis según el paso del pipeline en que se usan.

## Por qué leerla después de la clase

La clase cita a Yue et al. (2023) en dos diapositivas: el gráfico de **publicaciones por año según la ruta (imagen vs NGS)** —con GeoMx DSP dominando en imagen y Visium en secuenciación— sale de este paper. Además la guía completa lo que la clase solo nombra: qué hace cada técnica de la línea de tiempo (MERFISH, seqFISH, STARmap, Slide-seq, Stereo-seq…) y qué software se usa en cada paso.

---

## 1. Cuatro familias de tecnologías

La clase las agrupa en dos ([[Métodos basados en sondas|sondas/imagen]] y [[Métodos basados en secuenciación|secuenciación]]); Yue las abre en cuatro:

| Familia | Idea | Ejemplos | Carácter |
|---|---|---|---|
| **ISH** (hibridación in situ) | Sondas complementarias marcadas se hibridan al ARNm en el tejido | [[FISH y smFISH\|smFISH]] ("gold standard" de sensibilidad), **seqFISH** / seqFISH+ (hasta 60 canales), **[[MERFISH]]** (códigos con corrección de errores), split-FISH, EEL FISH, [[GeoMx DSP]], [[CosMx SMI]] | Dirigido (panel), subcelular, muy eficiente, caro |
| **ISS** (secuenciación in situ) | Se secuencia el ARN (o su ADNc) **dentro** del tejido: sondas *padlock* + amplificación por círculo rodante (RCA) | FISSEQ, **STARmap**, HybISS, **ExSeq** (+ microscopía de expansión), BOLORAMIS, **[[Xenium]]** (10x) | Dirigido, menos eficiente por el paso de retrotranscripción |
| **NGS** (captura con barcodes + secuenciación) | El ARN se captura sobre una superficie con [[Barcode espacial\|barcodes de posición]] y se secuencia | **ST** (2016, 1007 spots, 100 µm) → [[Visium]], **Slide-seq** / V2 (beads de 10 µm), **HDST** (beads en pocillos de 2 µm), **DBiT-seq** (grilla 50 × 50 por microfluídica; ARN + proteína), **Seq-Scope**, **[[Stereo-seq]]** (DNA nanoballs, spots de **500 nm**, secciones de hasta 13,2 × 13,2 cm — permite embriones enteros) | Transcriptoma completo, sin sesgo, baja eficiencia de captura |
| **Reconstrucción espacial** | Cortar el tejido en rodajas, secuenciar cada una y reconstruir computacionalmente (como una tomografía) | voxelation, **tomo-seq** (embrión de pez cebra), **STRP-seq** (cortes de 14 µm en distintos ángulos) | Sin imagen, baja resolución |

Detalles que complementan las diapositivas:

- La resolución de las técnicas NGS pasó de **100 µm (ST, 2016) a 500 nm (Stereo-seq)**.
- Eficiencia de detección: seqFISH ~84 %, MERFISH ~80 %; EEL FISH ~13 % pero barato, rápido (10 cm² en 61 h) y con **menos difusión lateral** gracias a la electroforesis → ver [[Lateral diffusion]].
- La sonda de **CosMx SMI** se inspira en el diseño de MERFISH, por eso es más robusta que GeoMx DSP; ambas plataformas de NanoString detectan ARN y proteína, pero no en el mismo corte. Xenium sí permite ARN y proteína en el mismo corte.
- **Visium** es la tecnología comercial más exitosa, y por eso concentra el software de terceros.
- La transcriptómica espacial fue el **método del año 2020** de *Nature Methods* (el hito que marca la línea de tiempo de la clase).

## 2. Los datos disponibles (hasta dic. 2022)

- 791 datasets: **192 de imagen** y **599 de secuenciación**; los de secuenciación crecen más rápido.
- Generados sobre todo en EE.UU., China y Europa; 34 especies, con predominio de humano y ratón.
- El **cerebro** es el tejido más estudiado en ambas especies; por la COVID-19 creció el uso de técnicas de imagen en **pulmón humano**.

## 3. El pipeline de análisis

### Preprocesamiento

| Datos de **imagen** | Datos de **secuenciación** (p. ej. Visium con **SpaceRanger**) |
|---|---|
| Registro de imágenes → identificación de *spots* de transcriptos (DeepBlink, BarDensr, ISTDECO) → [[Segmentación celular]] (Baysor, JSTA, Spage2vec…) | Procesar la imagen del tejido y asignar spots → alinear lecturas al genoma → unir matriz de expresión y matriz de posiciones |

Resultado en ambos casos: **matriz de expresión + matriz de ubicación**.

### Análisis downstream (y herramientas de ejemplo)

| Paso | Qué busca | Ejemplos |
|---|---|---|
| Corrección de [[Batch effect]] | Integrar varios cortes | Seurat, Harmony, Scanorama, LIGER, scVI |
| [[Reducción dimensional]] y *clustering* espacial | Dividir el tejido en dominios | PCA, SpatialPCA, UMAP; Louvain/Leiden; BayesSpace, **SpaGCN** (red convolucional de grafos), SC-MEB |
| Anotación de tipos celulares | Integrar con scRNA-seq: **mapeo** o **[[Deconvolución espacial\|deconvolución]]** → [[Integración de datos single cell y spatial]] | Seurat, CellTrek, **cell2location**, RCTD, SPOTlight, stereoscope, Tangram |
| **[[Genes espacialmente variables]] (SVGs)** | Genes cuya expresión sigue un patrón en el espacio | SpatialDE, SPARK, trendsceek, Giotto |
| Patrones y **regiones espaciales** | Módulos de co-expresión, subregiones del tejido → [[Spatial domains]] | stLearn (usa la H&E), RESEPT, SpaGCN |
| [[Comunicación célula-célula\|Interacción célula–célula]] y gen–gen | Comunicación entre vecinos → [[Neighborhoods]], [[Spatial niches]] | SpaOTsc, DIALOGUE, SVCA, GCNG, MISTy |
| Trayectorias espaciales | [[Pseudotiempo]] sobre el tejido | stLearn (pseudo-space-time), SPATA |
| **Modelos 3D** | Alinear cortes seriados | STUtility, PASTE (transporte óptimo), STAGATE |

## 4. Hacia dónde va

1. **No hay tecnología perfecta**: el trade-off entre cobertura del transcriptoma, resolución, throughput y eficiencia sigue vigente (el mismo mensaje de la clase). Falta **estandarizar** cómo se miden eficiencia de captura y resolución.
2. Agregar la **dimensión temporal** (ZipSeq, SPACECAT como puntos de partida).
3. **Multiómica espacial**: genómica, epigenómica y proteómica espaciales, con aplicación destacada en tumores.
4. La cantidad de técnicas y software exige actualización constante — y el [[Almacenamiento y visualización]] se vuelve un problema en sí.

## Conceptos del vault

[[Transcriptómica espacial]] · [[Métodos basados en sondas]] · [[FISH y smFISH]] · [[MERFISH]] · [[Xenium]] · [[Stereo-seq]] · [[Deconvolución espacial]] · [[Genes espacialmente variables]] · [[Comunicación célula-célula]] · [[Métodos basados en secuenciación]] · [[Barcode espacial]] · [[Visium]] · [[Visium HD]] · [[GeoMx DSP]] · [[CosMx SMI]] · [[10x Genomics]] · [[Nanostring]] · [[BGI]] · [[Vizgen]] · [[Segmentación celular]] · [[Lateral diffusion]] · [[Spatial domains]] · [[Integración de datos single cell y spatial]] · [[Batch effect]] · [[Almacenamiento y visualización]]

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
- [[Módulo 1 - MOC]]
