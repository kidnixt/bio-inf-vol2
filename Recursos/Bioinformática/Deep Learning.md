---
tags: [concepto, bioinformática, IA]
area: Bioinformática
aliases: [aprendizaje profundo, redes neuronales profundas]
---

# Deep Learning

Subconjunto del [[Machine Learning]] basado en redes neuronales de muchas capas, capaces de aprender representaciones jerárquicas directamente de datos crudos y de alta dimensión.

## Por qué encaja con datos de single cell

Los datos de [[scRNA-seq]] tienen exactamente el perfil donde el deep learning rinde: [[Alta dimensionalidad]], muchísimas observaciones, relaciones no lineales entre variables, y estructura latente de baja dimensión escondida en un espacio enorme.

Aplicaciones típicas:

- **Autoencoders variacionales (VAE)**: aprenden un espacio latente de la [[Matriz de conteo]] que sirve simultáneamente para [[Reducción dimensional]], corrección de [[Batch effect]] e imputación de [[Sparsity]].
- **Modelos de segmentación** basados en redes convolucionales para [[Segmentación celular]] en imágenes de [[Transcriptómica espacial]].
- **Modelos de fundación** entrenados sobre decenas de millones de células de los [[Atlas celulares]], que buscan una representación general de "célula" transferible a tareas nuevas.

## La precaución

Estos modelos **siempre devuelven un resultado suave y plausible**. En imputación y denoising, eso significa que pueden crear estructura que no estaba en los datos, y la estructura inventada es indistinguible de la real a simple vista en un [[UMAP]].

## Conexión con el curso

[[Módulo 3 - MOC|Módulo 3: Inteligencia Artificial aplicada a Bioinformática]].

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
