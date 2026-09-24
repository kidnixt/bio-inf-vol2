---
tags: [concepto, bioinformática, estructura]
area: Bioinformática
aliases: [3Di, alfabeto estructural, secuencia de forma, token 3Di]
---

# Alfabeto 3Di

La idea de **escribir la forma de una proteína con letras**, inventada para [[Foldseek]] (van Kempen et al., 2024).

## Cómo se discretiza

1. **10 rasgos geométricos** por residuo.
2. Se agrupan en **20 estados**.
3. **Un símbolo por residuo** → una **"secuencia" de forma**.

Lo que describe cada símbolo es **el contacto entre un residuo y el más cercano en el espacio** — no su vecino en la cadena. Es decir: el 3Di codifica justamente la información **terciaria** que la secuencia de aminoácidos no lleva.

## Por qué 20 letras

No es casualidad. Con **20 símbolos**, un [[Modelo de lenguaje de proteínas|PLM]] puede leer una secuencia 3Di **sin cambiar de arquitectura** — el mismo tokenizador, el mismo tamaño de vocabulario que ya usaba para aminoácidos. Eso es lo que permite [[ProstT5]]: traducir en los dos sentidos entre los dos alfabetos.

## Por qué importa

> **Dos proteínas pueden tener secuencias totalmente distintas y aun así la misma forma.** Comparando forma se detectan parentescos que la secuencia sola ya no ve ([[Homología remota]]).

Y la consecuencia práctica: comparar estructuras deja de ser un problema de geometría 3D —caro— y pasa a ser un problema de **alineamiento de secuencias**, optimizado durante décadas. De ahí las aceleraciones de 10⁴–10⁵× de Foldseek.

Los casos que se construyen sobre esta idea: [[ProstT5]] (predecir el 3Di sin calcular la estructura, ×1000 más rápido) y [[Phold]] (anotar genomas de fagos por forma).

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
