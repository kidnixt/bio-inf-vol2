---
tags: [concepto, bioinformática, modelado]
area: Bioinformática
aliases: [feasible flux space, espacio factible, espacio de soluciones de flujo, poliedro de flujos]
---

# Espacio de flujos factible

El conjunto de **todas las distribuciones de flujos** que cumplen las restricciones de un [[Modelado basado en restricciones|modelo basado en restricciones]]: estado estacionario (`S·v = 0`) y límites en los flujos (`l ≤ v ≤ u`).

## La intuición geométrica

- Cada reacción es un eje; una distribución de flujos es **un punto** en un espacio de tantas dimensiones como reacciones.
- Las restricciones recortan ese espacio hasta dejar un **poliedro convexo** (un cono acotado, en los dibujos de la clase).
- Cada punto del poliedro es un **fenotipo metabólico posible** según el modelo.

## Qué se hace con él

| Operación | Qué pregunta responde |
|---|---|
| [[Flux Balance Analysis\|FBA]] | ¿Cuál es el punto de máximo crecimiento? (un vértice) |
| [[Análisis de modos elementales\|Modos elementales]] | ¿Cuáles son las rutas mínimas que lo generan? (las aristas) |
| [[Diseño computacional de cepas]] | ¿Qué intervenciones **cambian su forma** para que ciertos fenotipos queden adentro y otros afuera? |

## En la clase

La frase que resume la segunda mitad:

> **Computational strain design reshapes the feasible flux space.**

Un [[Knock-out y knock-in|knock-out]] fija un flujo en 0 y **recorta** el poliedro; un knock-in agrega un eje nuevo y lo **expande**. [[StrainDesign]] marca regiones del espacio a **proteger** y a **suprimir**, y busca las intervenciones que dejan el espacio resultante con la forma deseada.

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
