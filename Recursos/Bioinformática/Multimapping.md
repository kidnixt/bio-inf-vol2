---
tags: [concepto, bioinformática]
area: Bioinformática
aliases: [multimappings, multireads, lecturas multimapeadas]
---

# Multimapping

Una lectura **multimapeada** es la que alinea igual de bien en más de un lugar del genoma o del [[Transcriptoma]]. La clase lo menciona como uno de los tres problemas de las herramientas clásicas de [[Alineamiento de secuencias]] aplicadas a [[scRNA-seq]].

## Por qué ocurre

- **Familias de genes y parálogos** con secuencias muy similares.
- **Pseudogenes**, que son copias degeneradas de genes reales.
- **Regiones repetitivas** del genoma.
- **Isoformas del mismo gen** que comparten exones — una lectura que cae en un exón común es compatible con todas ellas.
- **Lecturas cortas**: cuanto más corta la lectura, más sitios compatibles.

## Qué se hace

| Estrategia | Consecuencia |
|---|---|
| Descartar los multimappers | Se pierde señal real, sesgada contra familias génicas |
| Asignar al azar a uno de los sitios | Introduce ruido |
| Repartir proporcionalmente (EM) | Es lo que hacen los métodos de [[Pseudoalineamiento]] modernos |

El último enfoque estima la abundancia de cada transcripto de forma iterativa y reparte las lecturas ambiguas según esa estimación. Es más correcto, pero implica que un conteo no es un número entero de moléculas observadas sino una estimación.

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
