---
tags: [concepto, bioinformática, IA]
area: Bioinformática
aliases: [one-hot, codificación one-hot, vector disperso, representación dispersa]
---

# One-hot encoding

La forma más simple de convertir una categoría en números: un vector con **un 1 en la posición propia y 0 en todas las demás**.

Con 5.000 comidas (el ejemplo de la clase), cada una es un vector de 5.000 posiciones: un 1 en la suya y 0 en las otras 4.999.

## Sus dos problemas

1. **No codifica parecido.** Todos los 1s están **a la misma distancia** entre sí, así que *borscht* y *shawarma* quedan igual de lejanos que *borscht* y *pizza*. La representación sabe **contar** —cuántos 1s y dónde— pero nunca dice *"parecido"*.
2. **Es enorme y vacía.** 50.000 posiciones casi todas en cero para representar una palabra; la dimensión crece con el vocabulario y la información por número es mínima.

## La alternativa

El [[Embedding]]: de **50.000 números casi todos 0** a **100–300 números todos con valor**. Misma palabra, **167 veces menos números**, y ahora con información — porque la posición en el espacio denso *significa* algo.

En proteínas el contraste es menos dramático en tamaño (el vocabulario son 20 aminoácidos, o [[ESM-1b y ESM-2|33 tokens en ESM-2]] contando los símbolos de control), pero el problema conceptual es idéntico: one-hot dice que la lisina y la arginina son **tan distintas** como la lisina y el triptófano, cuando bioquímicamente no lo son. Un embedding aprende esa diferencia sin que nadie se la explicite.

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
- [[Mikolov et al 2013 - Efficient estimation of word representations]] *(lectura)*
