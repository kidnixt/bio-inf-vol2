---
tags: [concepto, bioinformática]
area: Bioinformática
aliases: [alineamiento, mapeo, alignment]
---

# Alineamiento de secuencias

Determinar de qué parte del genoma (o del [[Transcriptoma]]) proviene cada lectura secuenciada. Es el tercer desafío del [[scRNA-seq]] según la clase.

## Los problemas de las herramientas clásicas en single cell

La clase enumera tres:

- **Sitios de unión exón–exón**: una lectura que cruza un empalme no mapea de forma contigua sobre el genoma; el alineador debe partirla y buscar los dos exones, lo que es caro.
- **Uso de memoria RAM**: los índices de genoma completo son grandes y el volumen de lecturas en single cell es 10× el del [[Bulk RNA-seq]].
- **Manejo de [[Multimapping|multimappings]]**: lecturas que mapean igual de bien en varios sitios.

Todo esto sobre **200–500 millones de lecturas** por experimento, cuando un experimento de bulk típico tiene ~150 millones en total.

## El cambio de foco

> **No importa dónde mapea la lectura en el gen, ni qué mismatch hay. Sólo importa saber a qué gen corresponde la lectura.**

En [[scRNA-seq]] el producto final es una [[Matriz de conteo]] de genes × células. Las coordenadas exactas no se usan. Renunciar a calcularlas es gratis en términos de información y enorme en términos de costo — ver [[Pseudoalineamiento]].

## Cuándo sí hace falta el alineamiento completo

Cuando el análisis necesita posición: detección de variantes, análisis de isoformas y splicing, o RNA velocity (que distingue lecturas intrónicas de exónicas).

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
