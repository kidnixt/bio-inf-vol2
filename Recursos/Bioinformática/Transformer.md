---
tags: [concepto, bioinformática, IA, deep-learning]
area: Bioinformática
aliases: [transformers, self-attention, atención, multi-head attention, Attention Is All You Need]
---

# Transformer

La arquitectura que está detrás de **todos** los modelos que siguen —en texto y en proteínas— y también de los LLMs actuales (Vaswani et al., 2017, Google, *Attention Is All You Need*, arXiv:1706.03762).

## El problema que resolvió

Los modelos previos (RNN, LSTM, ver [[ELMo y SeqVec]]) leían **en orden**, símbolo por símbolo. Eso los hacía:

- **Lentos** — no se podían paralelizar.
- **Olvidadizos** — la posición 5 y la 500 apenas se conectaban.

## La idea: self-attention

> Cada posición **mira a todas las demás a la vez** y decide cuánto le importa cada una. Sin leer en orden, sin recurrencia.

La distancia entre dos posiciones cualesquiera pasa a ser **un solo paso** (en una RNN eran hasta *n* pasos).

| Pieza | Qué hace |
|---|---|
| **Q · K · V** | Cada símbolo se proyecta en *consulta*, *clave* y *valor*. El parecido entre consulta y clave decide **cuánto se mezcla cada valor** |
| **Multi-head** (8 cabezas) | Ocho atenciones en paralelo, cada una mirando un **tipo de relación distinto**. Se concatenan al final |
| **Posición explícita** | Como no hay orden implícito, la posición se **suma** al vector: senos y cosenos de distinta frecuencia |

*(Configuración original: 6 capas, 512 dimensiones, 8 cabezas.)*

## Por qué importa en biología

> **El Transformer no sabe de biología, solo de secuencias y relaciones a distancia.** Es exactamente el problema de la estructura terciaria: **posiciones lejanas en la cadena que están cerca en el espacio**.

| RNN / LSTM | Transformer |
|---|---|
| Leen de a un elemento | Mira toda la secuencia |
| Lo lejano se desvanece | Lo lejano en 1D puede estar **cerca en 3D** |
| No se paraleliza | Se paraleliza → **escala** |

Que la arquitectura resuelva *por casualidad* el problema central de la estructura proteica es lo que explica el hallazgo de [[ESM-1b y ESM-2|ESM-1b]]: **la estructura emerge sin que nadie la enseñe**, porque la atención tiene que descubrir qué residuos se condicionan mutuamente para poder rellenar máscaras.

Y la paralelización es lo que habilitó la escala: [[ProtT5 y ProtBERT]], [[ESM-1b y ESM-2|ESM-2]] (15.000 M de parámetros), [[ESM3]] (98.000 M).

Ver [[Masked language modeling]] para las tres formas de leer una secuencia con esta arquitectura.

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
