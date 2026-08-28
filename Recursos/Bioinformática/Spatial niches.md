---
tags: [concepto, bioinformática, espacial, análisis]
area: Bioinformática
aliases: [nichos espaciales, nicho]
---

# Spatial niches (nichos espaciales)

Microambientes **funcionales** definidos por la composición celular local y por lo que ocurre en ellos. Es el nivel más interpretativo de los tres que presenta la clase: si el [[Spatial domains|dominio]] es una región y el [[Neighborhoods|vecindario]] es una composición, el nicho es un vecindario **con un significado biológico**.

## El ejemplo de la clase

El nicho glial alrededor de las **placas amiloides** en modelos de enfermedad de Alzheimer. Alrededor de una placa se organiza una respuesta estereotipada: [[Microglía]] reactiva en contacto directo, [[Astrocito|astrocitos]] reactivos en la corona exterior, neuritas distróficas atravesando la estructura.

Referencias citadas en la clase: Chen and Lu & Fiers and De Strooper, *Cell* (2020); A. Mallach & M. Zielonka et al., *Cell Reports* (2024); M. Goedert et al., *Brain* (2017).

## Por qué es el argumento decisivo de la biología espacial

Una microglía reactiva **junto a una placa** y una microglía reactiva **en tejido sano** pueden tener perfiles transcriptómicos parecidos. En un [[UMAP]] de [[scRNA-seq]] caen en el mismo cluster. Pero no significan lo mismo.

> El contexto es parte del fenotipo. El [[Estado celular]] no se explica sólo por la célula: se explica por la célula **y su entorno**.

## Qué habilita

- Identificar programas de expresión que dependen de la distancia a una estructura.
- Estudiar comunicación celular con evidencia de proximidad física real, y no sólo de co-expresión de ligando y receptor.
- Definir unidades funcionales del tejido que no coinciden con ningún tipo celular.

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
