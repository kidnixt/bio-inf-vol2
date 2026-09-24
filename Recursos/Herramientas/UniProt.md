---
tags: [herramienta, base-de-datos, proteínas]
area: Herramientas
aliases: [UniProtKB, Swiss-Prot, TrEMBL]
---

# UniProt

Base de datos de **secuencias y funciones de proteínas**, mantenida por el consorcio UniProt (**EMBL-EBI**, **SIB** y **PIR**). Es la referencia de identidad para cualquier proteína.

| | |
|---|---|
| Tipo de registro | Secuencias en UniProtKB |
| Tamaño (corte) | **150.006.383** (release 2026_03, 02/09/2026) |
| Qué ofrece | Secuencias, funciones, dominios, variantes y referencias cruzadas |
| Consulta típica | *¿Qué secuencia, función y variantes corresponden a este blanco?* |

## Su doble rol en el curso

1. **Identificar blancos** — en el [[Diseño de fármacos asistido por computadora|CADD]], es el punto de partida para pasar de "esta enfermedad" a "esta proteína, con esta secuencia y estos dominios" ([[Blanco terapéutico]]).
2. **Entrenar modelos de secuencias** — los [[Modelo de lenguaje de proteínas|PLMs]] de la clase 9 se entrenan sobre subconjuntos de UniProt (UniRef50, UniRef90): los nombres de modelos como `esm2_t33_650M_**UR50D**` llevan el conjunto de entrenamiento en el nombre.

Un dato del corte de setiembre de 2026 que vale la pena retener: **[[AlphaFold DB]] tiene más modelos indexados (261 M) que secuencias hay en UniProtKB (150 M)**, porque el índice incluye también complejos.

Ver también [[PDB]] (estructuras experimentales) y [[AlphaFold DB]] (estructuras predichas).

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
