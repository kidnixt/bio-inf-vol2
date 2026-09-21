---
tags: [concepto, bioinformática, algoritmo]
area: Bioinformática
aliases: [MCS, gMCS, Generalized Minimal Cut Sets, cut sets mínimos, conjuntos de corte mínimos, PROTECT, SUPPRESS]
---

# Minimal Cut Sets

Un **cut set** es un conjunto de reacciones que, al eliminarse, hace imposible un cierto comportamiento de la red (por ejemplo, producir un metabolito o crecer en cierta condición). Es **mínimo** si ningún subconjunto propio alcanza: cada intervención es imprescindible.

## La versión generalizada

Los **Generalized Minimal Cut Sets** (gMCS), el algoritmo detrás de [[StrainDesign]], extienden la idea en dos direcciones:

| Extensión | Qué permite |
|---|---|
| **Regiones a SUPRIMIR (*SUPPRESS*)** | Definir comportamientos indeseados como regiones del [[Espacio de flujos factible]] que tienen que quedar vacías |
| **Regiones a PROTEGER (*PROTECT*)** | Exigir que ciertos comportamientos deseados sigan siendo posibles después de las intervenciones |
| **Knock-ins además de knock-outs** | Las intervenciones no solo cortan reacciones: también pueden agregar reacciones candidatas ([[Knock-out y knock-in]]) |
| **Costos** | Cada intervención tiene un costo y se acota el costo total |

El resultado son **conjuntos de intervenciones irreducibles** que mantienen factible el fenotipo deseado y vuelven infactibles los indeseados.

## En el caso de la clase

| Elemento | Configuración |
|---|---|
| SUPPRESS | 9 módulos: crecer con un solo azúcar, con un par de azúcares o con captación marginal de algún azúcar |
| PROTECT | 1 módulo: crecer consumiendo los tres azúcares |
| Costo máximo de intervención | 55 |
| Mínimo encontrado | 13 intervenciones |

## El límite

El número de soluciones posibles es combinatorio: *es computacionalmente imposible enumerarlas todas*. Las 30 corridas de la clase dan **una muestra** del espacio de soluciones, no el conjunto completo.

Es el concepto dual del [[Análisis de modos elementales]]: los modos elementales describen las rutas, los cut sets describen cómo bloquearlas.

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
- [[Schneider et al 2022 - StrainDesign]] *(lectura)*
