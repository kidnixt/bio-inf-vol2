---
tags: [concepto, bioinformática, modelos-metabolicos]
area: Bioinformática
aliases: [FVA, análisis de variabilidad de flujos]
---

# Flux Variability Analysis (FVA)

Complemento del [[Flux Balance Analysis|FBA]]: una vez encontrado el valor óptimo del objetivo (p. ej. crecimiento máximo), **maximiza y minimiza cada flujo por separado** manteniendo ese óptimo. El resultado es el **rango (*span*)** que puede tomar cada reacción sin que la célula deje de ser óptima.

## Por qué hace falta

La solución de FBA casi nunca es única: dentro del [[Espacio de flujos factible]] hay todo un **conjunto de soluciones óptimas**. FVA describe ese conjunto reacción por reacción.

## Cómo se lee

| Span | Interpretación |
|---|---|
| 0, con flujo ≠ 0 | Reacción **esencial** para el óptimo (no hay alternativa) |
| 0, con flujo = 0 | Reacción inactiva en el óptimo |
| Finito | Existen rutas alternativas equivalentes |
| Infinito (o enorme) | La reacción participa de un **ciclo** sin conversión neta |

Ejemplo de [[Maarleveld et al 2013 - Basic concepts of stoichiometric modeling of metabolic networks|Maarleveld et al. (2013)]] con el modelo de *[[Escherichia coli]]* iAF1260 creciendo en glucosa: **94 %** de los flujos quedan fijos en el óptimo y solo **6 %** pueden variar; la mitad de esos variables lo hace por ciclos.

## Uso en diseño de cepas

[[StrainDesign]] corre FVA en el preprocesamiento para detectar las reacciones **esenciales para el fenotipo que se quiere proteger** y excluirlas como blancos de *knock-out* → [[Schneider et al 2022 - StrainDesign]], [[Diseño computacional de cepas]].

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
- [[Maarleveld et al 2013 - Basic concepts of stoichiometric modeling of metabolic networks]] *(lectura)*
- [[Schneider et al 2022 - StrainDesign]] *(lectura)*
