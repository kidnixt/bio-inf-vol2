---
tags: [técnica, espacial, imagen]
area: Técnicas
aliases: [FISH, smFISH, single-molecule FISH, hibridación in situ fluorescente, ISH]
---

# FISH y smFISH

**FISH** (*fluorescence in situ hybridization*): sondas complementarias marcadas con fluoróforos se hibridan a una secuencia de ARN (o ADN) **en el tejido fijado**, y se ven al microscopio. Es el punto de partida de toda la familia de [[Métodos basados en sondas]].

**smFISH** (*single-molecule* FISH): muchas sondas cortas sobre **el mismo transcripto** hacen que cada molécula individual se vea como un **punto** limitado por la difracción → se pueden **contar** moléculas y ver su posición subcelular, sin amplificación.

## En la línea de tiempo de la clase

| Año | Hito |
|---|---|
| 1980 | FISH |
| 1992 | smFISH |
| 2012 | seqFISH (hibridación **secuencial**) |
| 2016 | [[MERFISH]] |

## Fortalezas y límite

- Se lo considera el **"gold standard" de sensibilidad** y hay variantes que se acercan al 100 % de eficiencia de detección ([[Yue et al 2023 - A guidebook of spatial transcriptomics technologies|Yue et al. 2023]]; [[Stuart and Satija 2019 - Integrative single-cell analysis|Stuart & Satija 2019]]).
- Límite: con fluoróforos distintos solo se separan **pocos genes a la vez**. La solución fue leer la identidad del gen como un **código a lo largo de varias rondas** de hibridación: con F fluoróforos y N rondas, hasta **Fᴺ** genes ([[Li and Zhou 2026 - Imaging-based Spatial transcriptomics|Li & Zhou 2026]]). De ahí salen seqFISH, seqFISH+, [[MERFISH]] y el esquema de [[CosMx SMI]].
- **osmFISH** toma el camino opuesto: pocos genes por ciclo, sin códigos, más robusto en tejido denso.

## Usos en integración

Antes de las plataformas de alto plex, se medían por FISH unos pocos **genes *landmark*** con patrón espacial conocido y se usaban para **ubicar** en el tejido las células de un [[scRNA-seq]] → [[Integración de datos single cell y spatial]].

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
- [[Li and Zhou 2026 - Imaging-based Spatial transcriptomics]] *(lectura)*
- [[Longo et al 2021 - Integrating single-cell and spatial transcriptomics]] *(lectura)*
- [[Stuart and Satija 2019 - Integrative single-cell analysis]] *(lectura)*
- [[Yue et al 2023 - A guidebook of spatial transcriptomics technologies]] *(lectura)*
