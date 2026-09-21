---
tags: [concepto, bioinformática, espacial, integracion]
area: Bioinformática
aliases: [deconvolución, deconvolution, deconvolución de spots, cell-type deconvolution]
---

# Deconvolución espacial

Estimar **qué tipos celulares, y en qué proporción**, hay dentro de cada *spot* de una técnica espacial por captura (como [[Visium]], donde un spot de 55 µm contiene ~3–30 células). Es la cara "para spots" de la [[Integración de datos single cell y spatial]]; su contraparte para datos de resolución celular es el **mapeo**.

## Deconvolución vs mapeo

| | **Deconvolución** | **Mapeo** |
|---|---|---|
| Datos espaciales típicos | Captura con barcodes (Visium, Slide-seq) — spots que mezclan células | Imagen de alto plex (MERFISH, CosMx, Xenium) — células individuales, panel limitado |
| Pregunta | ¿Qué mezcla de tipos celulares explica este spot? | ¿Qué tipo celular del scRNA-seq es esta célula? ¿Qué genes no medidos expresaría? |
| Métodos | Regresión, modelos bayesianos, scores | Integración en espacio común (Seurat, Harmony, LIGER), pciSeq |

En ambos casos, el primer paso es definir los tipos celulares con [[scRNA-seq]] de un tejido comparable.

## Familias de métodos (según [[Longo et al 2021 - Integrating single-cell and spatial transcriptomics|Longo et al. 2021]] y [[Yue et al 2023 - A guidebook of spatial transcriptomics technologies|Yue et al. 2023]])

- **Regresión**: el spot como combinación lineal de perfiles de tipos celulares (mínimos cuadrados no negativos en **SPOTlight**; ponderados en **SpatialDWLS**).
- **Bayesianos**: ajustar una binomial negativa (o Poisson) por gen y tipo celular y estimar la composición por máximo a posteriori (**RCTD** con "modo doblete", **cell2location**, **stereoscope**).
- **Scores de enriquecimiento**: puntuar cada spot por un set de genes marcadores (Seurat) — sirve también para puntuar ciclo celular, tumor/no tumor, etc.
- **Redes neuronales** (DSTG).

## Problemas

- **Mismatch** entre referencia y tejido: la disociación puede crear subtipos artificiales (respuesta de estrés) o perder tipos que no sobreviven; los métodos consideran "ruido" a un tipo que solo está en el dato espacial.
- Menor precisión cuando el spot tiene **pocos transcriptos** ([[Sparsity]]).
- Validación con mezclas *in silico* de células conocidas o con imagen de mayor resolución.

A medida que la resolución de captura llega a nivel subcelular ([[Visium HD]], [[Stereo-seq]]), la deconvolución se va convirtiendo en un **problema de mapeo**.

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
- [[Longo et al 2021 - Integrating single-cell and spatial transcriptomics]] *(lectura)*
- [[Yue et al 2023 - A guidebook of spatial transcriptomics technologies]] *(lectura)*
