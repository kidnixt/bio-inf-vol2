---
tags: [bioinformática, calidad, secuenciación]
area: Bioinformática
aliases: [Q-score, Qscore, phred, phred score, Q20, Q30, exactitud de lectura, calidad de base]
---

# Calidad Phred

La escala logarítmica con la que se expresa la confianza en cada base llamada. Un valor **Q** corresponde a una probabilidad de error:

$$Q = -10 \cdot \log_{10}(P_{error})$$

| Q | Probabilidad de error | Exactitud | Equivale a |
|---|---|---|---|
| Q20 | 1% | 99% | 1 error cada 100 bases |
| **Q26** | ~0,25% | 99,75% | 1 error cada **400** bases |
| **Q30** | 0,1% | 99,9% | 1 error cada **1.000** bases |
| Q33 | 0,05% | 99,95% | 1 error cada 2.000 bases |
| Q38 | ~0,016% | 99,984% | ~1 error cada 6.000 bases |

Cada 10 puntos de Q dividen el error por diez: la escala comprime diferencias enormes en números que parecen cercanos.

## Las plataformas en esta escala

| Plataforma | Calidad |
|---|---|
| [[Illumina]] | Q30 como benchmark |
| [[PacBio]] HiFi | Q30–Q33 |
| ONT R10.4.1 + [[Dorado]] v5 simplex | **Q26** (99,75%) |
| ONT [[Secuenciación dúplex\|dúplex]] (Kit 14 + SUP) | **Q30–Q31** (>99,9%) |
| [[Sequencing by Expansion\|Roche SBX]] | ~Q38 |

Con la química R10.4.1 + V14, ONT reporta como rendimiento típico **Q20+ en simplex y Q30+ en dúplex**, dependiendo de la química, el modelo y las condiciones experimentales.

## Lectura individual vs consenso

Es la distinción que más conviene tener presente: los valores de arriba son **por lectura individual**. La [[Secuencia consenso|exactitud del consenso]] es otra cosa y depende de la cobertura y el [[Pulido de secuencias|pulido]] — un ensamblado bacteriano con buena cobertura alcanza calidades muy superiores a las de cualquiera de sus reads.

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
