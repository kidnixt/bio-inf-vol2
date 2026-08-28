---
tags: [concepto, bioinformática, IA]
area: Bioinformática
aliases: [aprendizaje automático, ML]
---

# Machine Learning

Familia de métodos que aprenden patrones a partir de datos en lugar de seguir reglas escritas a mano. La clase lo menciona como una de las vías de solución a los cinco desafíos bioinformáticos del single cell.

## Dónde aparece en el pipeline de single cell

| Tarea | Tipo de método |
|---|---|
| [[Anotación de tipos celulares]] automatizada | Clasificación supervisada, entrenada sobre atlas anotados |
| [[Clustering]] | Aprendizaje no supervisado sobre grafos |
| [[Reducción dimensional]] ([[UMAP]], autoencoders) | Aprendizaje de representaciones |
| Corrección de [[Batch effect]] | Alineamiento de espacios latentes |
| Imputación / denoising de [[Sparsity]] | Modelos generativos |
| [[Segmentación celular]] en datos espaciales | Visión por computadora |

## La precaución

Un modelo supervisado sólo puede reconocer lo que había en su entrenamiento. En [[Anotación de tipos celulares]] eso significa que **un tipo celular nuevo se etiqueta como el más parecido conocido** y desaparece del análisis. Y en imputación, un modelo generativo puede producir estructura plausible que no estaba en los datos.

## Conexión con el curso

Es el tema central del [[Módulo 3 - MOC|Módulo 3: Inteligencia Artificial aplicada a Bioinformática]]. Ver también [[Deep Learning]] e [[Inteligencia Artificial]].

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
