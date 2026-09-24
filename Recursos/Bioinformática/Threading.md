---
tags: [concepto, bioinformática, estructura]
area: Bioinformática
aliases: [fold recognition, reconocimiento de plegamiento, enhebrado]
---

# Threading

Método de predicción estructural que **alinea la secuencia objetivo con estructuras de proteínas de referencia**, "encajándola" en un marco estructural conocido para predecir su conformación.

La diferencia con el [[Modelado por homología]] es de qué se compara: el modelado por homología busca **secuencias parecidas**; el threading busca **plegamientos compatibles**, evaluando qué tan bien encaja cada residuo de la secuencia en cada posición de un plegamiento candidato, con funciones de energía basadas en el entorno (enterrado/expuesto, contactos, estructura secundaria).

Eso le permite funcionar donde el modelado por homología no llega: dos proteínas pueden compartir plegamiento **sin similitud de secuencia detectable** — el fenómeno que la clase 9 llama [[Homología remota|homología remota]].

## El eco en la clase 9

Ese mismo problema —detectar parentescos estructurales que la secuencia ya no muestra— es el que resuelven, dos décadas después y por otra vía, [[Foldseek]] y [[ProstT5]]: en vez de encajar la secuencia en plegamientos candidatos, **escriben la forma con letras** ([[Alfabeto 3Di|3Di]]) y la comparan como texto.

El pipeline típico de threading (búsqueda de estructura → re-ensamblado → alineamiento TM-align → modelo final → predicción de función) aparece en la diapositiva junto al modelado por homología y a [[AlphaFold]], como las tres alternativas cuando el blanco no está en el [[PDB]].

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
