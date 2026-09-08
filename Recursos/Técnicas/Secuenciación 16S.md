---
tags: [técnica, microbiología, metagenómica, clínica]
area: Técnicas
aliases: [16S, gen ARNr 16S, 16S rRNA, ONT-16S, 16S Nanopore, amplicón 16S]
---

# Secuenciación 16S

Identificación bacteriana por amplificación y secuenciación del gen que codifica la subunidad **16S del ARN ribosomal**. Es un gen presente en todas las bacterias, con regiones muy conservadas (que permiten diseñar cebadores universales) alternadas con regiones variables (que permiten distinguir taxones).

## Qué aporta ONT

La ventaja específica de la [[Secuenciación con nanoporos|secuenciación con nanoporos]] es que una sola lectura cubre el **gen completo (~1,5 kb)**, mientras que las plataformas de [[Secuenciación de segunda generación|lectura corta]] secuencian solo algunas regiones variables. Más gen leído = mejor resolución taxonómica, sobre todo a nivel de especie.

Se prepara con el *Microbial Amplicon Barcoding Kit* ([[Preparación de bibliotecas de secuenciación]]), que cubre 16S completo e ITS, para bacterias, arqueas y hongos.

## Su nicho clínico

El 16S ONT **no compite con el cultivo en general**: compite en un escenario concreto y frecuente —

> cultivo **negativo**, o paciente **ya bajo antibióticos**.

Ahí el cultivo pierde sensibilidad y el 16S detecta la bacteria **directamente en la muestra**, reduciendo la incertidumbre etiológica y permitiendo convertir tratamiento empírico en dirigido.

## Los tres estudios de la clase (2026)

| Estudio | Diseño | Resultado central |
|---|---|---|
| **7 hospitales NHS**, Cheshire y Merseyside (Cunningham-Oakes et al.) | 218 casos, sitios estériles, turnaround 24–72 h | **56,9%** de los casos aportaron información útil para *antimicrobial stewardship*; mayor impacto en inmunosuprimidos |
| **Insel Gruppe, Suiza** (Geers et al.) | 101 muestras, 43 tipos, ONT vs [[Illumina]] | Concordancia **93,5%**, kappa 0,81; ONT **~50 h más rápido** y **35 vs 155 CHF** por muestra |
| **Bélgica** (Van de Gaer et al.) | 54 muestras prospectivas, 53 pacientes | Género >98% y especie >85% correctos; **aumenta la recuperación de patógenos no detectados por cultivo** |

## Su límite

> Su fortaleza es la **detección rápida y amplia**; su límite es que **no reemplaza el cultivo, el antibiograma ni la interpretación clínica**.

No da fenotipo de [[Resistencia antimicrobiana|resistencia]], no distingue viable de no viable, y en muestras polimicrobianas la interpretación se complica.

El pipeline de referencia para procesar estos datos es [[Porefile]].

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
