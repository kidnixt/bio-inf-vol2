---
tags: [herramienta, modelo, PLM, transformer]
area: Herramientas
aliases: [ESM, ESM-1b, ESM-2, ESM-C, ESM2, evolutionary scale modeling]
---

# ESM-1b y ESM-2

La familia de [[Modelo de lenguaje de proteínas|modelos de lenguaje de proteínas]] de Meta AI / EvolutionaryScale, entrenados con [[Masked language modeling|masked language modeling]] sobre secuencias de [[UniProt]]. Son los modelos de referencia del campo.

## ESM-1b: la estructura está adentro

Rives et al. (2021), *PNAS* 118(15), *Biological structure and function emerge from scaling unsupervised learning*.

**El hallazgo que cambió la percepción de estos modelos: nadie le enseñó estructura, y sin embargo quedó codificada.** La atención de un residuo **apunta a residuos lejanos en la secuencia pero cercanos en el espacio**, y del modelo se puede recuperar un [[Mapa de contactos]] competitivo con el método clásico CCMpred.

> [!note] Hace falta una sonda
> La información **está** en las representaciones, pero para leerla hace falta una **sonda entrenada** — una proyección lineal o un clasificador chico. Nadie le pasó un solo contacto durante el entrenamiento: los aprendió de **rellenar máscaras**.

## ESM-2: más escala, más estructura

Lin et al. (2023), *Science* 379:1123–1130. La misma receta llevada al extremo: de **8 millones a 15.000 millones** de parámetros.

| Métrica | Efecto de la escala |
|---|---|
| Perplejidad | **10,45 → 6,37** (el azar sería ~20) |
| Precisión de contactos | Mejora **en todos los tramos** |

El modelo de trabajo habitual es `facebook/esm2_t33_650M_UR50D`: **1280 dimensiones, 33 capas**. Y su **vocabulario son 33 tokens**, no 20: los 13 extra son símbolos de control (inicio, fin, relleno, la máscara, `X` para desconocidos y aminoácidos ambiguos).

De ESM-2 sale [[ESMFold]], y de escalar la idea a tres modalidades sale [[ESM3]].

## ESM-C

La generación siguiente de encoders (EvolutionaryScale, `huggingface.co/EvolutionaryScale`), en tamaños 300m y 600m. En el trabajo de tesis de **Juan Diego Puglia** (ORT) que presenta la clase, **ESM-C 300m fue el mejor de los tres modelos probados** —por encima de ESM-C 600m y de [[ProstT5]]— alcanzando 96,02 % de F1 ponderado con un SVM sobre embeddings congelados. Un recordatorio de que **más grande no siempre es mejor** (ver también Ankh, en [[Modelo de lenguaje de proteínas]]).

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
