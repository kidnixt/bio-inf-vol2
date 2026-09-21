---
tags: [técnica, espacial, imagen]
area: Técnicas
aliases: [multiplexed error-robust FISH, MERSCOPE]
---

# MERFISH

*Multiplexed Error-Robust Fluorescence In Situ Hybridization*. Técnica de [[Métodos basados en sondas|imagen]] que identifica cientos a miles de genes en el tejido leyendo un **código binario con corrección de errores** a lo largo de varias rondas de hibridación. Aparece en la línea de tiempo de la clase en **2016**, asociada a [[Vizgen]] (que la comercializa como **MERSCOPE**).

## Cómo funciona

1. Cada ARN blanco recibe **muchas sondas** que llevan secuencias de lectura (*readout*).
2. En cada ronda se hibridan sondas fluorescentes contra un subconjunto de esas secuencias → cada molécula está **encendida (1) o apagada (0)**.
3. Tras N rondas, cada punto tiene un código de N bits que se busca en un **codebook**.
4. El codebook se diseña con **distancia de Hamming** mínima: si se pierde o se agrega un bit (por [[Photobleaching]] o hibridación incompleta), el código sigue siendo reconocible o se descarta, pero **no se confunde con otro gen**.

Es la misma lógica que la clase muestra para [[CosMx SMI]], cuya sonda se inspira en el diseño de MERFISH ([[Yue et al 2023 - A guidebook of spatial transcriptomics technologies|Yue et al. 2023]]).

## Números y variantes

- Eficiencia de detección ~**80 %** (seqFISH ~84 %).
- En la tabla de Stuart & Satija (2019): 100–1.000 ARN, 100–40.000 células por experimento.
- **MERFISH con expansión** (gel que separa físicamente las moléculas) para combatir el [[Optical crowding]]; **MERFISH 3D** en cortes gruesos de hasta ~200 µm.
- Se usó para un **atlas de cerebro de ratón completo**, integrado con [[scRNA-seq]] (CCA + vecinos más cercanos) y registrado a un marco de coordenadas anatómico común ([[Li and Zhou 2026 - Imaging-based Spatial transcriptomics|Li & Zhou 2026]]) → [[Atlas celulares]].

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
- [[Li and Zhou 2026 - Imaging-based Spatial transcriptomics]] *(lectura)*
- [[Longo et al 2021 - Integrating single-cell and spatial transcriptomics]] *(lectura)*
- [[Stuart and Satija 2019 - Integrative single-cell analysis]] *(lectura)*
- [[Yue et al 2023 - A guidebook of spatial transcriptomics technologies]] *(lectura)*
