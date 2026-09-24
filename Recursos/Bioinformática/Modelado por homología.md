---
tags: [concepto, bioinformática, estructura]
area: Bioinformática
aliases: [homology modeling, modelado comparativo]
---

# Modelado por homología

Predecir la estructura 3D de una proteína **comparando su secuencia con proteínas de estructura conocida** e infiriendo la estructura a partir de esas similitudes.

Es el método clásico para responder la pregunta *"¿y si la estructura no está en el [[PDB]]?"*, junto con [[Threading]] y los [[AlphaFold|métodos basados en IA]].

## Cómo funciona

1. Buscar en el PDB proteínas con secuencia similar (**templados**).
2. Alinear la secuencia objetivo contra el templado ([[Alineamiento de secuencias]]).
3. Copiar las coordenadas de las regiones conservadas.
4. Modelar los *loops* y las cadenas laterales que difieren, y refinar para eliminar choques.

Funciona bien cuando hay un templado con identidad de secuencia alta y se degrada rápido cuando no lo hay — su límite es estructural: **si no hay homólogo con estructura, no hay modelo**.

## Su lugar hoy

[[AlphaFold]] no lo volvió obsoleto pero sí lo desplazó del centro: con [[AlphaFold DB]] hay un modelo para casi cualquier proteína conocida, y con mejor calidad en el régimen de baja identidad, que era justamente donde el modelado por homología fallaba.

Queda sin embargo una continuidad conceptual interesante con la clase 9: tanto el modelado por homología como AlphaFold2 se apoyan en **información evolutiva** (homólogos, [[Alineamiento múltiple de secuencias|MSA]]). Lo que hace distinto a [[ESMFold]] es prescindir de ella — la señal sale del [[Modelo de lenguaje de proteínas|modelo de lenguaje]], no de los parientes de la proteína.

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
