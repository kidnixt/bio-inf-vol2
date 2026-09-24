---
tags: [concepto, bioinformática, quimioinformática]
area: Bioinformática
aliases: [activity cliffs, acantilado de actividad]
---

# Activity cliff

El contraejemplo permanente a la hipótesis de [[Similitud química|similitud]]: **pequeña diferencia estructural, gran cambio biológico**.

El ejemplo de la clase:

| Estructura | Actividad |
|---|---|
| Molécula A | **12 nM** |
| Molécula A **+ CH₃** | **8,4 µM** |

Un solo metilo empeora la actividad **~700 veces**.

## Por qué importa

Un modelo de [[Diseño basado en ligandos|LBDD]] —[[QSAR]], modelo de [[Machine Learning|ML]], búsqueda por similitud— asume implícitamente que el paisaje estructura–actividad es **suave**: moléculas cercanas, actividades parecidas. Un activity cliff es un acantilado en ese paisaje, y el modelo lo **suaviza**: predice actividad intermedia donde en realidad hay una caída.

Es además el caso donde el modelo se equivoca **justo donde parece más seguro** — la molécula nueva se parece mucho a un activo conocido, así que el score es alto y la confianza también.

Las causas suelen ser físicas: un choque estérico en el sitio de unión, la pérdida de un puente de hidrógeno, un cambio de conformación. Es decir, cosas que un modelo basado en 2D no puede ver, y que sí pueden aparecer en [[Docking molecular|docking]] o [[Dinámica molecular|MD]] — otro argumento a favor de combinar las dos rutas del [[Diseño de fármacos asistido por computadora|CADD]].

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
