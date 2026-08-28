---
tags: [concepto, bioinformática, desafío]
area: Bioinformática
aliases: [sparsidad, dispersión, dropout, ceros]
---

# Sparsity

> **Gran cantidad de ceros.**

Es el primero de los cinco desafíos bioinformáticos que enumera la clase. En una [[Matriz de conteo]] de [[scRNA-seq]], típicamente **el 80–95% de las celdas son cero**.

## Dos tipos de cero, indistinguibles en los datos

| Tipo | Significado |
|---|---|
| **Cero biológico** | El gen realmente no se expresa en esa célula |
| **Cero técnico (*dropout*)** | El gen se expresa, pero la molécula no fue capturada, retrotranscrita o secuenciada |

El problema es que la matriz no dice cuál es cuál. Un gen ausente puede ser información biológica valiosa o simplemente mala suerte de muestreo.

## Por qué ocurre

- La eficiencia de captura del ARN de una célula es baja (del orden del 10%).
- La [[Profundidad de secuenciación]] por célula es limitada.
- El [[Rango dinámico]] es enorme: los genes de baja abundancia son justamente los que caen bajo el umbral de detección — y son los marcadores más informativos.

En [[scATAC-seq]] la sparsity es aún **más extrema**: sólo hay 2 copias de cada locus por célula diploide, así que la matriz es prácticamente binaria.

## Qué se hace al respecto

- **Normalización y transformación** adecuadas para datos de conteo.
- **Agregación**: sumar células similares para recuperar señal — ésa es la lógica del [[Pseudobulk]].
- **Imputación** o *denoising*: estimar los valores faltantes a partir de células vecinas. Es un terreno donde los métodos de [[Machine Learning]] y [[Deep Learning]] aportan soluciones, con el riesgo de inventar estructura que no estaba.
- **No sobreinterpretar un cero.**

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
