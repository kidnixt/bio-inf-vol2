---
tags: [bioinformática, secuencias, nanoporos]
area: Bioinformática
aliases: [k-mer, k-mers, kmer, kmers]
---

# K-mer

Una subsecuencia de longitud *k* dentro de una secuencia mayor. En [[Secuenciación con nanoporos|nanoporos]] el concepto deja de ser una abstracción de análisis y se vuelve **físico**.

## El k-mer como unidad de señal

> La corriente está determinada por un grupo corto de nucleótidos —un k-mer— **situado simultáneamente en la región sensible del nanoporo**.

Varias bases ocupan la constricción a la vez, y todas contribuyen al bloqueo de corriente. La señal medida no dice "esta base es una C": dice "el contexto que está pasando ahora se parece al contexto X".

## Consecuencias

| Consecuencia | Detalle |
|---|---|
| El [[Basecalling\|basecalling]] es un problema de secuencias | Hay que reconstruir la cadena de contextos más probable, no leer caracteres |
| El espacio de estados es grande | Un modelo con estados de largo 5 maneja 4⁵ = **1024 contextos posibles** — [[Dorado]] los modela con un CRF |
| Los [[Homopolímeros\|homopolímeros]] son el caso difícil | En `AAAAAA`, avanzar una base **no cambia el k-mer**: la corriente se mantiene plana y el largo se estima por duración, no por transiciones |
| La geometría del poro importa | Cuanto más corta la constricción, menos bases contribuyen y mejor la resolución: de ahí α-hemolisina → MspA → CsgG, y R9 → R10.4.1 con doble región sensible |

## En el resto de la bioinformática

El mismo concepto sostiene el [[Pseudoalineamiento]], el ensamblaje por grafos de De Bruijn y la [[Clasificación taxonómica|clasificación taxonómica]] rápida por k-mers (Kraken, Centrifuge).

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
- [[Asgari and Mofrad 2015 - Continuous distributed representation of biological sequences]] *(lectura)*
