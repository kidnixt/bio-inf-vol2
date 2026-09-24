---
tags: [lectura, modulo-3, PLM, generativo, multimodal]
area: Lecturas
tipo: research article
autores: Thomas Hayes, Roshan Rao, Halil Akin, Nicholas J. Sofroniew, Deniz Oktay, Zeming Lin, Robert Verkuil, et al., Alexander Rives
año: 2025
revista: Science
doi: 10.1126/science.ads0018
aliases: [Hayes 2025, ESM3 paper, esmGFP, "Simulating 500 million years of evolution with a language model"]
---

# Hayes et al. (2025) — *Simulating 500 million years of evolution with a language model*

> [!info] Ficha de la lectura
> **Tipo:** research article — *Science* (el PDF del vault es el preprint de bioRxiv, doi 10.1101/2024.07.01.600583)
> **Autores:** EvolutionaryScale, con el Arc Institute y UC Berkeley
> **Clase asociada:** [[Modelos de lenguaje de proteínas y embeddings proteicos]] (clase 9)
> **PDF:** [[Hayes et al 2025 - Simulating 500 million years of evolution.pdf]]
> **Código:** `github.com/evolutionaryscale/esm`

## En una frase

El paper de **[[ESM3]]**: un modelo que razona sobre **secuencia, estructura y función** en un mismo vocabulario de tokens, y que generó **esmGFP**, una proteína fluorescente a 58 % de identidad de cualquier GFP natural.

## Por qué leerla después de la clase

La clase muestra la Figura 1B (las tres pistas fusionándose), la Figura 4 (esmGFP) y la Figura 2A (fidelidad al prompt). El paper es donde está el **argumento sobre qué significa "simular evolución"**, que es la parte más fácil de malinterpretar.

---

## 1. La tesis

> "Más de tres mil millones de años de evolución han producido una imagen de la biología codificada en el espacio de las proteínas naturales. Acá mostramos que los modelos de lenguaje entrenados sobre tokens generados por la evolución **pueden actuar como simuladores evolutivos** para generar proteínas funcionales lejanas de las conocidas."

El paper se apoya en el consenso que [[Rives et al 2021 - Biological structure and function emerge from scaling|Rives et al.]] ayudó a construir: que bajo las secuencias hay un **lenguaje fundamental de la biología de proteínas**.

## 2. La arquitectura

Tres modalidades como **tokens discretos** en un espacio latente común:

| Secuencia | Estructura | Función |
|---|---|---|
| Las 20 letras | Coordenadas 3D tokenizadas | Palabras clave, sitios catalíticos |

Con **atención geométrica** en el primer bloque, que permite condicionar por coordenadas atómicas. **98.000 millones de parámetros**, más de 10²⁴ FLOPS — un orden de magnitud sobre [[ESM-1b y ESM-2|ESM-2]].

El entrenamiento enmascara **todo** y rellena posición por posición, así que el mismo mecanismo sirve para representar y para **generar**, y el diseño se puede guiar dando parte de cualquiera de las tres pistas ([[Inverse folding]]).

## 3. esmGFP

Se le dio **solo la estructura de los residuos del núcleo** de una GFP natural —los que forman y catalizan el cromóforo—. El modelo generó el resto, razonó en cadena a lo largo de **96 generaciones**, y las proteínas resultantes **fluorescen de verdad**, medido en lisado de *E. coli*.

Desde el pocillo B8 (57 % de identidad) la cadena siguió hasta C10: **esmGFP**, con **58 % de identidad** y **96 mutaciones sobre 229 aminoácidos**. Los autores estiman el equivalente a unos **500 millones de años** de evolución natural.

> [!warning] El matiz que la clase subraya
> **No es que el modelo "sepa" biología.** Simula evolución porque predecir el token enmascarado **lo obliga** a aprender cómo se mueve la evolución en el espacio de proteínas posibles. Es una afirmación sobre la geometría del espacio aprendido, no sobre comprensión.

## 4. Qué aporta respecto de la clase

- **La Figura 2A leída con cuidado**, que es donde el paper es más útil y menos citado: la fidelidad al prompt **depende mucho de qué se promptea**. Promptear por **estructura** funciona muy bien (cRMSD bajo con pTM alto); **SASA** es bimodal y **palabras clave** se concentra en los dos extremos. Es decir: las tres modalidades **no son igual de gobernables**.
- **La escala de cómputo**, que vuelve concreto el cierre de la clase sobre la barrera de entrada.
- Que exista una versión abierta de 1.4B con licencia MIT, que es lo que hace el modelo usable fuera de un laboratorio grande.

> [!tip] Conexión con la tesis de Johny
> El capítulo 1 de la tesis pregunta **qué mide** la evaluación de un PLM generativo. Este paper es el caso extremo del problema: la validación de esmGFP **no** es un score in silico, es fluorescencia medida en placa. Es el estándar contra el que se juzga cualquier proxy.

## Conceptos del vault

[[ESM3]] · [[ESM-1b y ESM-2]] · [[Masked language modeling]] · [[Inverse folding]] · [[Modelo de lenguaje de proteínas]] · [[Transformer]] · [[Embedding]]

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
- [[Módulo 3 - MOC]]
