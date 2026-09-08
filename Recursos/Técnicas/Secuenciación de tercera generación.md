---
tags: [técnica, secuenciación, lecturas-largas]
area: Técnicas
aliases: [lecturas largas, long reads, secuenciación de lectura larga, tercera generación, molécula única]
---

# Secuenciación de tercera generación

Secuenciación de **lectura larga** sobre **molécula única**, sin amplificación previa obligatoria. Punto de referencia: **2011**. Sus dos representantes son [[PacBio]] HiFi y [[Secuenciación con nanoporos|Oxford Nanopore]].

| | |
|---|---|
| Longitud | Decenas de kb por fragmento en promedio; ultra-long >50 kb N50, reads de hasta >4 Mb |
| Principio | Se lee **una molécula individual** en tiempo real, no un cluster de copias |

## Por qué obligó a rediseñar la bioinformática

Las tecnologías de tercera generación cambiaron **tres cosas a la vez**:

1. el **volumen** de datos,
2. la **longitud** de las lecturas,
3. el **[[Perfil de error]]** asociado (indels y errores dependientes de contexto, en vez de sustituciones aleatorias).

Gran parte de las herramientas diseñadas para [[Secuenciación de segunda generación|lecturas cortas]] dejó de servir, y aparecieron familias nuevas de software: [[Pulido de secuencias|corrección de errores y pulido]], [[Ensamblaje de novo]], y análisis de SNPs y [[Variantes estructurales|variantes]]. El número acumulado de herramientas crece casi verticalmente desde ~2014 (Amarasinghe et al. 2020).

> [!important] La idea central
> La principal consecuencia de las lecturas largas **no fue solamente obtener fragmentos más extensos**: cambió el **tipo de información recuperable**.

Con una lectura que atraviesa entera una región repetida, un plásmido o un operón, se resuelven preguntas que con fragmentos de 150 pb eran computacionalmente ambiguas por construcción.

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
