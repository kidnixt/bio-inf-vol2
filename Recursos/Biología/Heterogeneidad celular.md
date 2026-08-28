---
tags: [concepto, biología]
area: Biología celular
---

# Heterogeneidad celular

> **La mayoría de los tejidos son heterogéneos: son comunidades de células diferentes.**

Es la premisa que justifica toda la biología de célula única. Un tejido no es una masa uniforme sino una mezcla de [[Tipo celular|tipos celulares]] distintos, cada uno en un [[Estado celular]] particular, en proporciones variables.

## El problema que genera

Cuando se mide un tejido entero con [[Bulk RNA-seq]], el resultado es un **promedio ponderado** por la abundancia de cada población. Ese promedio puede no corresponder a ninguna célula real. Se pierden:

- Los distintos [[Tipo celular|tipos celulares]]
- Los [[Estado celular|estados y estadíos celulares]]
- Las subpoblaciones
- Las **células raras** — que a menudo son las biológicamente decisivas (una población tumoral resistente, un progenitor, una microglía reactiva)

Un cambio real en una subpoblación del 2% es indetectable en un promedio.

## Dos ejes de heterogeneidad

1. **Composicional**: qué tipos de células hay y en qué proporción → lo resuelve el [[scRNA-seq]].
2. **Espacial**: dónde está cada una y con quién → lo resuelve la [[Transcriptómica espacial]].

Ver el ejemplo canónico en [[Tejido cerebral]].

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
- [[Biología espacial - mapeando la expresión génica a su entorno]]
