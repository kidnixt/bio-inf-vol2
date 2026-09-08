---
tags: [técnica, secuenciación]
area: Técnicas
aliases: [NGS, secuenciación de nueva generación, lecturas cortas, short reads, 454, Ion Torrent, Solexa, next generation sequencing]
---

# Secuenciación de segunda generación

También llamada **NGS** (*next generation sequencing*) o **secuenciación de lectura corta**. Punto de referencia: **2005**.

## Qué cambió

El salto respecto de [[Secuenciación Sanger|Sanger]] no fue de química sino de **arquitectura**: alto rendimiento por **paralelización masiva** de las reacciones de secuenciación. Millones de reacciones ocurriendo simultáneamente sobre una superficie.

| Plataformas | 454, Solexa / [[Illumina]], Ion Torrent |
|---|---|
| Longitud | ~50–500 pb |
| Fortaleza | Exactitud por base y volumen |
| Debilidad | Fragmentos cortos: repeticiones, [[Plásmido\|plásmidos]], elementos móviles y [[Variantes estructurales\|variantes estructurales]] quedan sin resolver |

## Su huella en la bioinformática

Casi toda la caja de herramientas bioinformática clásica —alineadores, ensambladores, *variant callers*— fue diseñada asumiendo lecturas cortas y de muy alta exactitud. Cuando llegó la [[Secuenciación de tercera generación|tercera generación]], gran parte de ese software **dejó de ser directamente aplicable**, y hubo que rediseñar los métodos.

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
