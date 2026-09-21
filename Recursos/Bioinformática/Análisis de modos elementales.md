---
tags: [concepto, bioinformática, modelado]
area: Bioinformática
aliases: [EMA, elementary modes, Elementary Modes Analysis, modos elementales, elementary flux modes, EFM]
---

# Análisis de modos elementales

Enfoque (1994) de análisis de redes metabólicas que enumera los **modos elementales**: las rutas mínimas de flujo que pueden operar en estado estacionario por sí solas.

## Qué es un modo elemental

Una distribución de flujos que:

- cumple `S·v = 0` y la irreversibilidad de las reacciones;
- es **mínima**: si se apaga cualquiera de sus reacciones, deja de ser una ruta viable.

Geométricamente, los modos elementales son las **aristas** (rayos extremos) del cono de flujos: cualquier punto del [[Espacio de flujos factible]] es una combinación de ellos. En la diapositiva aparecen como los puntos rojos en los vértices del poliedro.

## Comparación con los otros enfoques de la clase

| Enfoque | Año | Qué produce |
|---|---|---|
| [[Modelado basado en restricciones\|Constraint-based model]] | — | El poliedro de flujos posibles |
| **Elementary Modes Analysis** | 1994 | Todas las rutas mínimas (una descripción completa del poliedro) |
| [[Flux Balance Analysis]] | 1993 | Un solo punto óptimo |

## El problema de escala

El número de modos elementales crece de forma combinatoria con el tamaño de la red, y en modelos a escala genómica es intratable enumerarlos todos. Es la misma familia de problema que aparece en el caso de estudio de la clase, donde **es computacionalmente imposible enumerar todas las soluciones** de [[StrainDesign]] y solo se obtiene una muestra.

El concepto dual, los [[Minimal Cut Sets|cut sets mínimos]] (qué reacciones cortar para bloquear un conjunto de modos), es la base algorítmica de StrainDesign.

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
- [[Maarleveld et al 2013 - Basic concepts of stoichiometric modeling of metabolic networks]] *(lectura)*
