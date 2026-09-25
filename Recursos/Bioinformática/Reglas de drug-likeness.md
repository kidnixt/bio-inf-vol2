---
tags: [concepto, bioinformática, quimioinformática, filtros]
area: Bioinformática
aliases: [regla de los cinco, regla de Lipinski, Lipinski, drug-likeness, RO5, filtros fisicoquímicos]
---

# Reglas de drug-likeness

Filtros basados en **propiedades fisicoquímicas** que descartan moléculas con baja probabilidad de comportarse como fármacos orales. Son la forma más barata de recortar una biblioteca antes de cualquier cálculo caro.

La más conocida es la **regla de los cinco de Lipinski** (RO5, 1997):

| Propiedad | Límite |
|---|---|
| Peso molecular (MW) | ≤ 500 Da |
| cLogP | ≤ 5 |
| Donores de puente de hidrógeno (HBD) | ≤ 5 |
| Aceptores de puente de hidrógeno (HBA) | ≤ 10 |

La tabla de la clase recoge muchas más, con sus rangos de MW, PSA, HBA, HBD, cLogP, enlaces rotables (RTB), anillos aromáticos (NAR) y carga formal:

| Regla | Referencia |
|---|---|
| Ghose | Ghose et al., 1999 |
| Oprea's drug-like rule | Oprea, 2000 |
| Walters | Walters & Murcko, 2002 |
| Veber | Veber et al., 2002 |
| REOS | Walters & Namchuk, 2003 |
| ***Beyond rule of five*** (bRO5) | Doak et al., 2014 |
| Congreve's rule (RO3, fragmentos) | Congreve et al., 2003 |
| *Herbicide-likeness* · *Insecticide-likeness* | Tice, 2001 |
| Regla de Hao (*pesticide-likeness*) | Hao et al., 2011 |

Dos cosas que vale la pena notar: existen reglas explícitas **más allá** de RO5 (para modalidades como macrociclos y degradadores, con MW ≤ 1000 y PSA ≤ 250), y las mismas ideas se trasladaron a **agroquímicos**, con umbrales distintos.

> Son **filtros heurísticos**, no leyes: muchos fármacos aprobados violan alguna regla. Su función real es **priorizar**, igual que todo lo demás en el [[Diseño de fármacos asistido por computadora|CADD]].

Ver [[Representaciones moleculares]] y [[ADMET]].

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
- [[Fahim 2026 - Structure-based design of antiviral and antihypertensive drugs]] *(lectura)*
- [[Fang et al 2026 - A comprehensive review of AI in drug design]] *(lectura)*
