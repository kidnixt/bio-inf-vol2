---
tags: [bioinformática, genómica, variantes]
area: Bioinformática
aliases: [SV, structural variants, variantes, variantes genómicas]
---

# Variantes estructurales

Cambios genómicos que involucran **segmentos grandes** de ADN: inserciones, deleciones, duplicaciones, inversiones, translocaciones y variaciones de número de copia.

## Por qué son el caso emblemático de las lecturas largas

Con [[Secuenciación de segunda generación|lecturas cortas]] las variantes estructurales se **infieren indirectamente**, a partir de señales como cobertura anómala o pares de lecturas que mapean a distancias inesperadas. Es reconstrucción por evidencia circunstancial, y falla justo donde más importa: dentro de regiones repetidas, que es donde suelen ocurrir.

Con [[Secuenciación de tercera generación|lecturas largas]] una sola lectura **atraviesa el evento completo** y lo muestra directamente. Se pasa de inferir a observar.

## En la clase

Aparecen en la primera consideración final, como una de las tres dimensiones de información que se obtienen simultáneamente de la misma molécula:

> Con la secuenciación de nanoporos se pueden observar, en una misma molécula de ADN, varias dimensiones de la información biológica: **secuencia, variantes estructurales, [[Metilación del ADN|metilación]]**.

En genómica microbiana esto se traduce en la resolución de **elementos móviles** y [[Plásmido|plásmidos]] — exactamente lo que permitió, en los casos de [[Vigilancia genómica hospitalaria|vigilancia hospitalaria]], demostrar la transmisión de un plásmido de resistencia entre especies distintas.

También son una de las familias de análisis (junto con SNPs) que hubo que rediseñar para lecturas largas, con su propio software.

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
