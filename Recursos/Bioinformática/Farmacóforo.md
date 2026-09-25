---
tags: [concepto, bioinformática, quimioinformática]
area: Bioinformática
aliases: [farmacóforos, pharmacophore, modelo farmacofórico]
---

# Farmacóforo

Abstracción de una molécula como un **patrón espacial de interacciones**, en vez de como un conjunto de átomos y enlaces.

## Los rasgos

| Rasgo | Qué representa |
|---|---|
| **Donor** | Donor de puente de hidrógeno |
| **Aceptor** (HBA) | Aceptor de puente de hidrógeno |
| **Hidrófobo** | Zona apolar |
| **LM / ionizable** | Grupo cargado (positivo o negativo) |
| **Aromático** (AR) | Anillo aromático |

Un modelo farmacofórico es esos rasgos **más las distancias entre ellos**.

## El ejemplo de la clase

Del **ácido salicílico** se extrae un triángulo de tres rasgos —aromático (AR), aceptor de H (HBA) e ionizable negativo (NI)— con sus distancias d₁, d₂, d₃. El **ácido acetilsalicílico** (aspirina) cumple ese patrón → ***match***.

## Para qué sirve

> **Útil cuando ligandos distintos comparten un modo de unión.**

Ahí está su ventaja sobre la [[Similitud química|similitud por fingerprints]]: dos moléculas pueden tener estructuras químicas muy diferentes —un Tanimoto bajo— y sin embargo presentar **los mismos rasgos en las mismas posiciones del espacio**. El farmacóforo las reconoce como equivalentes; el fingerprint no.

En un pipeline de [[Virtual screening]], el farmacóforo suele ser uno de los **primeros filtros**: es barato de evaluar y reduce mucho la biblioteca antes de llegar al [[Docking molecular|docking]]. Así se usa, por ejemplo, en el caso de los inhibidores de α-glucosidasa (farmacóforo → [[QSAR|3D-QSAR]] → docking → ensayo) y en el pipeline de VS + ML sobre MAO.

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
- [[Fahim 2026 - Structure-based design of antiviral and antihypertensive drugs]] *(lectura)*
