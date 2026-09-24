---
tags: [concepto, bioinformática, fármacos]
area: Bioinformática
aliases: [CADD, Computer-Aided Drug Design, diseño asistido por computadora, diseño computacional de fármacos]
---

# Diseño de fármacos asistido por computadora

El **CADD** (*Computer-Aided Drug Design*) es el conjunto de métodos computacionales que **ordenan y priorizan** moléculas candidatas antes de sintetizarlas y ensayarlas. Es el objeto de la clase [[Métodos para el diseño computacional de fármacos]].

## El problema que resuelve

> **¿Qué molécula sintetizaríamos mañana?**

Hay del orden de **10⁶ moléculas** candidatas frente a **10 experimentos** posibles. La computadora **ordena y prioriza**; el laboratorio **determina qué hipótesis son viables**.

## Las dos rutas

| | [[Diseño basado en ligandos\|LBDD]] | [[Diseño basado en estructura\|SBDD]] |
|---|---|---|
| Idea | Aprende de ligandos conocidos | Usa la estructura del blanco |
| Métodos | [[Similitud química]] · [[Farmacóforo]] · [[QSAR]] · [[Virtual screening\|VS]] | [[Docking molecular]] · [[Dinámica molecular\|MD]] · [[Energía libre de unión\|energía libre]] |

> **No es una competencia entre métodos: es una decisión condicionada por evidencia.** Si hay ligandos activos → LBDD. Si hay estructura 3D → SBDD. Si hay ambos → combinación. Si no hay nada → generar evidencia (biología, cribado, medición).

## Aportes y límites

| Aportes | Límites |
|---|---|
| Prioriza blancos y moléculas | Depende de datos y supuestos |
| Compara hipótesis **antes de sintetizar** | Puede **extrapolar fuera de dominio** |
| Integra señales de escalas distintas | Necesita controles y **medición experimental** |

## Dónde interviene

En el [[Descubrimiento y desarrollo de fármacos|desarrollo de un medicamento]], el CADD trabaja sobre todo en las tres primeras etapas: identificación del blanco, identificación de *hits* y optimización de *leads*. **Cada resultado puede obligar a volver a una etapa anterior.**

Su versión con [[Inteligencia Artificial|IA]] no reemplaza nada de esto: **IA-driven no significa "IA sola", significa un ciclo de decisión guiado por aprendizaje** (ver [[Aprendizaje activo]]).

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
