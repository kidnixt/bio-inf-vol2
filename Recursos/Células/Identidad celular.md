---
tags: [concepto, células, desafío]
area: Biología celular
---

# Identidad celular

> **¿Cómo definir a una célula y cómo nombrarla?**

Es uno de los cinco desafíos bioinformáticos que se enumeran en la clase, y probablemente el más conceptual de todos.

## El criterio molecular

La respuesta operativa que da la clase es: una célula se define **en función de conocer qué genes expresa**. Eso convierte a la [[Expresión génica]] en la medida de identidad y es lo que hace posible todo el pipeline de [[Clustering]] + [[Anotación de tipos celulares]].

## Por qué sigue siendo un problema abierto

1. **La resolución define el resultado.** Con más células y más profundidad aparecen más subdivisiones. ¿3000 tipos en el cerebro son 3000 tipos, o son 4 tipos en 3000 estados? Ver [[Tipo celular]] vs [[Estado celular]].
2. **El límite entre clusters es una decisión, no un hecho.** Cambiar la resolución del algoritmo cambia cuántos "tipos" hay.
3. **La nomenclatura no está unificada.** El mismo tipo celular recibe nombres distintos en laboratorios distintos, lo que complica la comparación entre estudios y motiva los [[Atlas celulares]].
4. **La identidad puede depender del contexto.** Una célula puede ser lo que es por dónde está — argumento central de la [[Biología espacial - mapeando la expresión génica a su entorno|biología espacial]].

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
