---
tags: [concepto, bioinformática, análisis]
area: Bioinformática
aliases: [trayectorias, pseudotime, trajectory inference, inferencia de trayectorias]
---

# Pseudotiempo y trayectorias

> **Ordenar las células a lo largo de una trayectoria de desarrollo o diferenciación basada en cambios de expresión génica.**

## La idea

Un experimento de [[scRNA-seq]] es una **foto**: todas las células se capturan en el mismo instante. Pero si un tejido contiene células en distintos puntos de un proceso continuo (progenitores, estadios intermedios, células maduras), esa foto contiene implícitamente la película.

El pseudotiempo asigna a cada célula una posición sobre esa trayectoria inferida a partir de la similitud transcriptómica. No es tiempo real: es **orden a lo largo del proceso**.

```
Progenitor ──────────────────────────► Célula madura
   pseudotiempo 0                        pseudotiempo 1
```

## Ejemplo típico

La diferenciación de OPCs a [[Oligodendrocito|oligodendrocitos]] mielinizantes: los datos muestran un continuo, no clusters bien separados. Es justamente el caso donde el [[Clustering]] discretiza mal la biología.

## Supuestos que hay que vigilar

- Que exista realmente un proceso continuo, y no dos poblaciones estables que el método une igual.
- Que estén representados los estadios intermedios (si el tránsito es rápido, hay pocas células ahí).
- Que la variación dominante en los datos sea la del proceso de interés, y no un [[Batch effect]].

El método **siempre devuelve una trayectoria**, exista o no. La validación biológica es indispensable.

## Métodos relacionados

RNA velocity usa la proporción de lecturas intrónicas (ARN no procesado) vs exónicas para inferir la **dirección** del cambio, algo que el pseudotiempo por sí solo no determina.

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
