---
tags: [concepto, bioinformática, fármacos, historia]
area: Bioinformática
aliases: [zanamivir, DRD4, halicina, nirmatrelvir, casos de éxito CADD]
---

# Casos de éxito del diseño computacional de fármacos

Los cuatro casos con los que la clase [[Métodos para el diseño computacional de fármacos|de diseño computacional]] argumenta que **el método fue parte de un sistema**, nunca la explicación completa.

| Año | Caso | Ruta | Qué se hizo |
|---|---|---|---|
| **1993** | **Zanamivir** | [[Diseño basado en estructura\|SBDD]] | Diseño racional sobre la **neuraminidasa** de influenza (von Itzstein et al.) |
| **2019** | **DRD4** | SBDD + [[Virtual screening\|VS]] | Docking de **138 millones** de moléculas; nuevos quimiotipos (Lyu et al., *Nature*) |
| **2020** | **Halicina** | [[Diseño basado en ligandos\|LBDD]] + [[Inteligencia Artificial\|IA]] | Modelo fenotípico y validación antibacteriana (Stokes et al., *Cell*) |
| **2021** | **Nirmatrelvir** | SBDD + química | Inhibidor oral de **Mpro** del SARS-CoV-2 (Owen et al.) |

> **Éxito = hipótesis computacional + química + ensayo + desarrollo.**

## Zanamivir (1993)

El caso fundacional del diseño racional: a partir de la estructura cristalográfica del sitio activo de la neuraminidasa se diseñó una molécula complementaria. Es el ejemplo de manual de que conocer la estructura permite **proponer un mecanismo 3D**.

## DRD4 (2019)

El receptor dopaminérgico D4, con cribado ultragrande:

| | |
|---|---|
| **138 M** | moléculas dockeadas |
| **81** | quimiotipos nuevos |
| **30** | activos submicromolares |
| **180 pM** | agonista optimizado |

Lo interesante no es solo el número de activos sino los **quimiotipos nuevos**: estructuras químicas que ningún programa de LBDD habría propuesto, porque no se parecen a los ligandos conocidos. Es el argumento a favor de empezar el embudo con cientos de millones en vez de decenas de miles.

## Halicina (2020)

Ver [[Reposicionamiento de fármacos]]. LBDD + [[Deep Learning|deep learning]] sin estructura ni mecanismo: 2.335 moléculas de entrenamiento, >107 M evaluadas, un candidato inesperado validado experimentalmente.

## Nirmatrelvir (2021)

El componente activo de Paxlovid, inhibidor de la proteasa principal (Mpro) del SARS-CoV-2. Diseño basado en estructura combinado con química medicinal intensiva, en tiempo récord — y un recordatorio de que la parte lenta rara vez es el cálculo.

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
- [[Fahim 2026 - Structure-based design of antiviral and antihypertensive drugs]] *(lectura)*
