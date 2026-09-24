---
tags: [concepto, bioinformática, fármacos]
area: Bioinformática
aliases: [RVS, reverse virtual screening, target fishing, inverse docking, búsqueda de blancos]
---

# Cribado virtual inverso

El problema **al revés** del [[Virtual screening]]: en vez de tener un blanco y buscar moléculas, se tiene **una molécula activa** y se busca **contra qué blanco actúa**. Los nombres en la literatura: *reverse virtual screening* (RVS), *target fishing*, *inverse docking*.

## Para qué sirve

- **Explicar un hit fenotípico**: una molécula que mata al parásito pero no se sabe por qué.
- **Anticipar off-targets** y por lo tanto toxicidad y selectividad.
- **[[Reposicionamiento de fármacos|Reposicionar]]** un fármaco conocido hacia otra indicación.

## El pipeline del caso de la clase

Del trabajo de [[Andrés Ballesteros]] sobre 2,7-diarilpirazolo[1,5-a]pirimidinas con actividad antitumoral (*Eur. J. Med. Chem. Reports*, 2022). Es un embudo, igual que el VS directo, pero de **proteínas** en vez de moléculas:

```
PharmMapper                                      → 379 PDB
  Filtro 1: blanco común (75 % de las moléculas) → 178 PDB
  Filtro 2: Docking XP + MM-GBSA
  Filtro 3: 30 % top score                       →  45 proteínas
  Filtro 4: blanco común (75 %)                  →  18 proteínas
  Control con moléculas inactivas + evidencia biológica → 7 proteínas
```

Dos detalles de diseño que vale la pena retener:

- El criterio de **"blanco común"**: se queda con las proteínas que aparecen para el **75 % de las moléculas activas** de la serie. Un blanco que explica solo a una molécula probablemente sea ruido.
- El **control con moléculas inactivas**: si un blanco también aparece para los compuestos que *no* funcionan, no explica la actividad. Es el control negativo que convierte una lista de scores en una hipótesis.

Con los blancos candidatos ya caracterizados, el trabajo sigue del otro lado: caracterización de los sitios de unión y **crecimiento de ligandos** (*growth of ligands*) para proponer moléculas nuevas.

Mejores scores del ejemplo: Glide_XP entre −10,7 y −14,0, con MM-GBSA entre −67,8 y −114,0 kcal/mol.

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
