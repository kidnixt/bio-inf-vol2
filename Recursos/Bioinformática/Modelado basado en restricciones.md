---
tags: [concepto, bioinformática, modelado]
area: Bioinformática
aliases: [constraint-based modeling, constraint-based model, estado estacionario, steady state, flux bounds, límites en los flujos]
---

# Modelado basado en restricciones

En lugar de intentar predecir **el** estado exacto de la célula (lo que exigiría conocer todas las cinéticas enzimáticas), se definen **restricciones** que cualquier estado válido tiene que cumplir, y se estudia el conjunto de estados que las cumplen.

## Las restricciones

| Restricción | Nombre | Qué impone |
|---|---|---|
| `S · v = 0` | **Estado estacionario** (*steady state*) | Cada metabolito interno se produce al mismo ritmo que se consume |
| `v_j ≥ 0` | Irreversibilidad | Las reacciones irreversibles solo van en un sentido |
| `l_i ≤ v_i ≤ u_i` | **Límites en los flujos** (*flux bounds*) | Capacidad máxima, disponibilidad de sustratos en el medio, reacciones apagadas (`l = u = 0`) |

Donde `S` es la [[Matriz estequiométrica]] y `v` el vector de flujos.

## Lo que se obtiene

Un poliedro convexo en el espacio de flujos: el [[Espacio de flujos factible]]. Sobre él se aplican distintos análisis:

- [[Flux Balance Analysis]]: optimizar un objetivo (típicamente la [[Reacción de biomasa]]).
- [[Análisis de modos elementales]]: enumerar las rutas mínimas.
- [[Diseño computacional de cepas]]: modificar el poliedro con [[Knock-out y knock-in|KO/KI]] ([[Minimal Cut Sets]], [[StrainDesign]]).

## La ventaja

No necesita parámetros cinéticos, que casi nunca se conocen a escala genómica. Solo requiere la estequiometría (que sale del genoma anotado) y algunos límites. Por eso es el enfoque que escala a modelos de miles de reacciones.

El ecosistema de software asociado se llama COBRA (*COnstraint-Based Reconstruction and Analysis*); ver [[openCOBRA]].

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
