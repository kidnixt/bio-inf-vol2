---
tags: [herramienta, plataforma, espacial, imagen]
area: Herramientas
aliases: [Xenium In Situ, 10x Xenium]
---

# Xenium

Plataforma comercial de [[10x Genomics]] de transcriptómica espacial **por imagen**, lanzada en **2022** (junto a [[CosMx SMI]] en la línea de tiempo de la clase). Pertenece a la familia de **secuenciación in situ (ISS) / amplificación in situ**, no a la de captura + secuenciación como [[Visium]].

## Cómo funciona

- Sondas *padlock* que se circularizan sobre el blanco y se amplifican por **círculo rodante (RCA)** dentro del tejido → productos muy brillantes ("rolonies").
- La identidad del gen se lee por **rondas de hibridación e imagen** con barcodes, como en otros [[Métodos basados en sondas]].
- **No destructiva** con el tejido: permite detectar **ARN y proteína en el mismo corte** ([[Yue et al 2023 - A guidebook of spatial transcriptomics technologies|Yue et al. 2023]]).
- Resolución **subcelular**, panel dirigido, compatible con muestras de patología (FFPE).

## Por qué importa en el análisis

Su adopción motivó **benchmarks** sistemáticos de rendimiento, [[Segmentación celular]], control de calidad y "derrame" de transcriptos entre células vecinas ([[Li and Zhou 2026 - Imaging-based Spatial transcriptomics|Li & Zhou 2026]]). [[SpatialData]] incluye un lector nativo para sus datos.

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
- [[Li and Zhou 2026 - Imaging-based Spatial transcriptomics]] *(lectura)*
- [[Yue et al 2023 - A guidebook of spatial transcriptomics technologies]] *(lectura)*
