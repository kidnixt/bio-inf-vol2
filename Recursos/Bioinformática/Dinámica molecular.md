---
tags: [concepto, bioinformática, simulación, física]
area: Bioinformática
aliases: [MD, molecular dynamics, trayectoria, simulación de dinámica molecular]
---

# Dinámica molecular

Simulación del **movimiento** de un sistema molecular en el tiempo, integrando las ecuaciones de movimiento con un campo de fuerzas. En el [[Diseño de fármacos asistido por computadora|CADD]] es lo que convierte una foto en una película.

## El contraste con el docking

El ejemplo de la clase es deliberadamente minimalista: **metanol (CH₃OH)** en un sitio de unión.

| | [[Docking molecular\|Docking]] | Dinámica molecular |
|---|---|---|
| Qué muestra | Una pose seleccionada | La misma molécula en distintos tiempos (t₀, t₁ … tₙ) |
| Resultado | **Pose + puntuación** | **Trayectoria temporal** |
| Qué describe | Una configuración | **Movimiento y cambios** en las interacciones |

Un detalle que la figura subraya: en la MD **el solvente y los residuos del sitio también cambian de posición**. No es solo el ligando el que se mueve — el sitio de unión respira.

> El docking **sugiere** una pose; la dinámica molecular **evalúa cómo cambia con el tiempo**.

## Para qué se usa

- **Validar poses**: una pose que se desarma en los primeros nanosegundos de simulación probablemente sea un artefacto del scoring.
- **Muestrear estados**: generar el *ensemble* conformacional que después se usa en docking flexible (ver **flexibilidad del receptor** en [[Docking molecular]]).
- **Estimar afinidades**: los métodos rigurosos de [[Energía libre de unión]] se construyen sobre trayectorias de MD.

En los casos del curso aparece como **el paso de confirmación** antes del bioensayo: en el estudio de α-glucosidasa, los 4 compuestos activos se estudian mediante MD; en el de las *p*-quinonas, la MD acompaña los cálculos cuánticos.

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
