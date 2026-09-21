---
tags: [técnica, espacial, secuenciacion]
area: Técnicas
aliases: [spatial enhanced resolution omics-sequencing, STOmics]
---

# Stereo-seq

*Spatial Enhanced Resolution Omics-sequencing*, de [[BGI]]. Técnica de [[Métodos basados en secuenciación|captura + secuenciación]] que aparece en la línea de tiempo de la clase en **2021**.

## Qué la distingue

- La superficie de captura son **DNA nanoballs** (DNB) ordenadas sobre un chip de silicio fabricado por litografía; cada una lleva un [[Barcode espacial]].
- **Resolución:** puntos de captura de **~500 nm** — del orden subcelular. Entre ST (2016, 100 µm) y Stereo-seq, la resolución de las técnicas NGS mejoró unas 200 veces.
- **Área:** secciones de hasta **13,2 × 13,2 cm** — la más grande de las técnicas revisadas por [[Yue et al 2023 - A guidebook of spatial transcriptomics technologies|Yue et al. (2023)]], lo que permite analizar **embriones y órganos enteros**.

Combina así lo que en otras plataformas es un trade-off: **área × resolución** con transcriptoma completo (sin panel). El precio es el de toda la familia: baja eficiencia de captura por punto, lo que obliga a agrupar puntos (*binning*) o [[Segmentación celular|segmentar]].

## En la clase

El atlas de **embriones humanos** (estadios de Carnegie CS12–CS23) de Pan et al. (*Nature*, 2026) — el *"Atlas! (!!!)"* de la clase — combina Stereo-seq con snRNA-seq, secuenciados en DNBSEQ-Tx, y produce mapas de ~50 órganos y tejidos en desarrollo → [[Atlas celulares]].

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
- [[Yue et al 2023 - A guidebook of spatial transcriptomics technologies]] *(lectura)*
