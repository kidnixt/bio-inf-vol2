---
tags: [bioinformática, calidad, secuenciación]
area: Bioinformática
aliases: [error de secuenciación, tasa de error, errores sistemáticos, indels]
---

# Perfil de error

No alcanza con saber **cuánto** se equivoca una plataforma: importa **cómo** se equivoca. El perfil de error —qué tipo de error, en qué contextos, con qué correlación entre lecturas— es lo que determina qué herramientas bioinformáticas sirven.

## Comparación de plataformas

| Plataforma | Tipo de lectura | Exactitud oficial | Error equivalente | Longitud |
|---|---|---|---|---|
| [[Illumina]] | short read | Q30 benchmark (~99,9%) | ≤0,1% | 150–300 pb |
| [[PacBio]] HiFi | long read HiFi | 99,9%; hasta 99,95% (Q33) | ~0,1–0,05% | hasta 25 kb |
| **ONT R10.4.1 + [[Dorado]] v5 simplex** | long read | 99,75% (**Q26**) | ~0,25% | ultra-long posible |
| **ONT [[Secuenciación dúplex\|dúplex]] (Kit 14 + SUP)** | long read duplex | ~Q30–Q31 (>99,9%) | ~0,1–0,08% | long reads |

Illumina se equivoca sobre todo por **sustituciones** distribuidas casi al azar; ONT se equivoca sobre todo por **indels dependientes del contexto de secuencia**. Esa diferencia cualitativa, y no solo la tasa, es la razón por la que las herramientas de lectura corta dejaron de ser aplicables.

## Los siete factores que lo determinan

La clase los agrupa en tres bloques, y el agrupamiento es útil porque **cada bloque se corrige en un lugar distinto del flujo**.

### A. Plataforma y basecalling → afectan la lectura individual

| # | Factor | Detalle |
|---|---|---|
| 1 | **Poro y química** | R10.4.1/E8.2 mejora la resolución y reduce errores frente a R9.4.1 |
| 2 | **Modelo de basecalling** | SUP > HAC >> FAST: mayor capacidad del modelo, menor error |
| 3 | **Versión de [[Dorado]]** | Rebasecallear con modelos más nuevos puede mejorar la exactitud |
| 4 | **Modo de lectura** | [[Secuenciación dúplex\|Dúplex]] reduce errores al combinar ambas hebras |

### B. Contexto molecular de la muestra → errores residuales específicos de contexto

| # | Factor | Detalle |
|---|---|---|
| 5 | **Contexto de secuencia** | [[Homopolímeros\|Homopolímeros]], STR y regiones de baja complejidad aumentan sobre todo los **indels** |
| 6 | **Bases modificadas** | 5mC, 6mA y otras [[Metilación del ADN\|modificaciones]] alteran la señal y pueden inducir errores puntuales |

### C. Análisis posterior → afecta el consenso, no cada read

| # | Factor | Detalle |
|---|---|---|
| 7 | **Cobertura y posprocesamiento** | Más cobertura + corrección y [[Pulido de secuencias\|pulido]] mejoran la exactitud de la [[Secuencia consenso\|secuencia consenso]] |

La [[Preparación de bibliotecas de secuenciación|preparación de la biblioteca]] atraviesa los tres bloques: define el contexto molecular disponible y si habrá o no lecturas dúplex.

*Sanderson et al., Microbial Genomics 2024 · Hall et al., eLife · Purushothaman et al., BMC Medical Genomics 2026*

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
