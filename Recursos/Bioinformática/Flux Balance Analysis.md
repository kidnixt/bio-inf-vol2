---
tags: [concepto, bioinformática, modelado, optimización]
area: Bioinformática
aliases: [FBA, análisis de balance de flujos]
---

# Flux Balance Analysis

Método (1993) que, dentro del [[Espacio de flujos factible]], elige la distribución de flujos que **maximiza una función objetivo**:

```
max  z = w · v          (típicamente: max v_bio)
s.a. S · v = 0
     l_i ≤ v_i ≤ u_i
```

## Cómo funciona

1. Se parte de la [[Matriz estequiométrica]] de un [[Modelo metabólico a escala genómica]].
2. Se imponen las restricciones del [[Modelado basado en restricciones|modelado basado en restricciones]].
3. Se define el objetivo, casi siempre el flujo de la [[Reacción de biomasa]] (crecimiento).
4. Se resuelve como un problema de **programación lineal**.

Geométricamente, la solución es un vértice del poliedro: la flecha naranja de la diapositiva.

## El supuesto

Que el organismo, moldeado por la evolución, opera cerca de su máximo de crecimiento en las condiciones dadas. Es razonable para microorganismos en cultivo, y es lo que permite predecir sin parámetros cinéticos.

## Qué da y qué no da

| Da | No da |
|---|---|
| Tasa de crecimiento predicha | Concentraciones de metabolitos |
| Una distribución de flujos óptima | Dinámica temporal ni regulación |
| Efecto predicho de un KO (se fija el flujo en 0 y se re-optimiza) | Una solución única: suele haber muchos óptimos equivalentes |

## FBA vs diseño de cepas

FBA pregunta *"¿qué hace la célula?"*. El [[Diseño computacional de cepas]] pregunta *"¿qué le tengo que hacer a la célula para que solo pueda hacer lo que yo quiero?"*: no optimiza dentro del espacio, lo **remodela**.

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
- [[Maarleveld et al 2013 - Basic concepts of stoichiometric modeling of metabolic networks]] *(lectura)*
- [[Schneider et al 2022 - StrainDesign]] *(lectura)*
