---
tags: [concepto, bioinformática, evolución]
area: Bioinformática
aliases: [homología remota, remote homology, zona crepuscular, twilight zone]
---

# Homología remota

Parentesco evolutivo entre proteínas **tan divergentes que la secuencia ya no lo muestra**. Comparten un ancestro común y, en general, la forma y la función — pero el porcentaje de identidad de secuencia cae por debajo de lo que un [[Alineamiento de secuencias|alineamiento]] puede distinguir del azar (la clásica *twilight zone*, ~20–30 % de identidad).

## Por qué existe

La evolución conserva **la función y la forma**, no las letras. Una proteína puede acumular sustituciones durante cientos de millones de años y seguir plegándose igual: cada cambio individual es tolerable mientras el plegamiento se mantenga. Al final, dos homólogos verdaderos parecen no tener nada que ver.

Es el tercer caso de la tabla de **ediciones al texto** de la clase: no es un error, es **divergencia desde un ancestro común** — *el texto cambió y la función se conservó*.

## Cómo se detecta

| Vía | Método |
|---|---|
| **Perfiles de secuencia** | PSI-BLAST, HMMs ([[Alineamiento múltiple de secuencias\|MSA]]), PyHMMER |
| **Estructura** | Alineadores estructurales clásicos (TM-align, Dali, CE), [[Threading]] |
| **Estructura como texto** | [[Foldseek]] con el [[Alfabeto 3Di\|3Di]] — 10⁴–10⁵× más rápido |
| **Desde la secuencia, sin estructura** | [[ProstT5]]: predice el 3Di y lo busca con Foldseek |

El resultado más fuerte de ProstT5 es exactamente este: el 3Di **predicho** detecta homología remota **casi al nivel de usar estructuras experimentales**, sin MSA y sin calcular coordenadas.

## Dónde importa

En organismos de evolución rápida, donde es la norma y no la excepción. El caso de [[Phold]]: **más del 65 % de las proteínas de bacteriófagos no se pueden anotar por homología de secuencia** — y anotar por forma sube la cobertura de 34,7 % a 49,4 %.

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
- [[Bouras et al 2026 - Phold]] *(lectura)*
- [[Heinzinger et al 2019 - SeqVec]] *(lectura)*
- [[Heinzinger et al 2024 - ProstT5]] *(lectura)*
- [[Lin et al 2023 - Evolutionary-scale prediction with a language model]] *(lectura)*
- [[Rives et al 2021 - Biological structure and function emerge from scaling]] *(lectura)*
- [[van Kempen et al 2024 - Foldseek]] *(lectura)*
