---
tags: [herramienta, software, interfaz]
area: Herramientas
aliases: [Pathway Engineering & Co-consumption Assistant, Pathway Engineering and Co-consumption Assistant, PECA assistant]
---

# PECA

**Pathway Engineering & Co-consumption Assistant**: la interfaz que la clase presenta como respuesta al problema de la brecha entre métodos computacionales y laboratorio.

> **These type of methods do not reach the experimental metabolic engineers. There is a gap to bridge.**

La idea es que un ingeniero metabólico experimental pueda correr un flujo de [[Diseño computacional de cepas]] sin escribir código: un asistente paso a paso sobre [[StrainDesign]].

## Los cinco pasos

| Paso | Qué se configura |
|---|---|
| **1 · Host** | Modelo hospedero: precargados (`PECA_toy.xml`, `iMM904.xml`, `yeast9_anaerobic_biggids.xml`) o subir uno propio en [[SBML]] `.xml` o COBRA JSON `.json`. *"El modelo define todas las reacciones y genes disponibles"* |
| **2 · Sugars** | Qué azúcares entran en juego |
| **3 · Candidates** | Candidatos [[Knock-out y knock-in\|KI]] (reacciones) y KO (por defecto, *all gene rules*: todas las reglas gen-reacción) |
| **4 · Settings** | Solver (*backend*: **glpk**), costo máximo y número de soluciones (p. ej. 10 / 10) |
| **5 · Run** | Correr y ver el estado |

El panel lateral muestra en todo momento la configuración actual (modelo, azúcares, candidatos, solver, estado). La mascota es un pulpo científico con un guiño a la IA.

## Por qué existe

Porque el cuello de botella dejó de ser puramente computacional. El método funciona ([[StrainDesign]] encuentra diseños que fuerzan el [[Co-consumo de azúcares|co-consumo]]); lo que falta es que sea **usable** por quien después va a construir la cepa en la fase *Build* del [[Ciclo DBTL]].

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
