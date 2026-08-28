---
tags: [concepto, bioinformática, espacial]
area: Bioinformática
aliases: [región de interés, regiones de interés, regions of interest, ROIs]
---

# ROI (Región de Interés)

Área del tejido seleccionada por el usuario para ser perfilada como unidad. Es la lógica de trabajo del [[GeoMx DSP]].

## Cómo se define

Sobre una imagen del tejido (histología, inmunofluorescencia), el operador dibuja las regiones que quiere comparar: tumor vs estroma, capa cortical vs capa cortical, zona lesionada vs zona sana. Cada ROI se perfila por separado.

## Especificaciones en GeoMx

| | |
|---|---|
| Diámetro | 50 – 600 µm |
| Células por ROI | 50 – 500 |

## La implicancia analítica

Una ROI **no es una célula**: es un mini-bulk de decenas a cientos de células. Lo que se obtiene es un promedio local, con las mismas limitaciones que el [[Bulk RNA-seq]] —se pierden [[Tipo celular|tipos celulares]] y subpoblaciones dentro de la región— pero **con posición conocida**.

Es un compromiso deliberado: se cambia resolución celular por transcriptoma completo, throughput alto y una pregunta bien planteada a nivel de arquitectura tisular.

## Lo que introduce

**Sesgo del operador.** Las ROIs las elige una persona mirando el tejido, así que la selección incorpora una hipótesis previa sobre dónde está la biología interesante. Eso es una fortaleza cuando la hipótesis es buena y una limitación cuando lo interesante estaba en otro lado.

## Antecedente

La [[Microdisección por captura láser]] es la versión manual de la misma idea.

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
