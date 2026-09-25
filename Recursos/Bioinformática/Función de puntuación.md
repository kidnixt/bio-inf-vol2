---
tags: [concepto, bioinformática, fármacos]
area: Bioinformática
aliases: [scoring function, score, scoring, rescoring, funciones de puntuación]
---

# Función de puntuación

La función que le pone un número a una pose de [[Docking molecular|docking]], para poder **ordenarlas**.

## Los términos que combina

| Término | Qué captura |
|---|---|
| **Estérico** | Complementariedad de forma; choques |
| **Electrostático** | Interacciones entre cargas |
| **Puente de hidrógeno** | Donores y aceptores bien orientados |
| **Hidrofobia** | Contacto entre superficies apolares |
| **Desolvatación** | Costo de sacar el agua del sitio y del ligando |

El resultado es un **score**, que la clase define con precisión: ***ranking* dentro del protocolo**.

> [!warning] La advertencia central
> **No equivale automáticamente a la [[Energía libre de unión|ΔG]] experimental.**
>
> Sirve para comparar moléculas **entre sí**, evaluadas con **el mismo protocolo** (mismo software, misma preparación del receptor, misma caja de docking). Comparar scores entre protocolos, o leerlos como afinidades absolutas, no es válido.

Es la segunda de las **cinco reglas para interpretar resultados** con las que cierra la clase.

## Rescoring

En el [[Virtual screening|VS jerárquico]], el segundo nivel del embudo (10⁵ → 10³) es justamente **rescoring**: volver a puntuar las mejores poses con una función más cara y presumiblemente más precisa. Es un reconocimiento explícito de que la función rápida se usa para **descartar**, no para decidir.

Las funciones aprendidas con [[Machine Learning|ML]] sobre [[PDBbind]] son hoy una alternativa a las clásicas basadas en términos físicos — con la limitación de que heredan los sesgos de ese conjunto de entrenamiento.

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
- [[Fang et al 2026 - A comprehensive review of AI in drug design]] *(lectura)*
- [[Nazarova et al 2026 - V-SYNTHES2]] *(lectura)*
