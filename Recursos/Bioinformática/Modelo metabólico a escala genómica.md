---
tags: [concepto, bioinformática, biología-de-sistemas, modelado]
area: Bioinformática
aliases: [GEM, GEMs, GSMM, genome-scale metabolic model, genome scale metabolic models, modelo metabólico, modelos metabólicos]
---

# Modelo metabólico a escala genómica

> **Un mapa metabólico formalizado matemáticamente para un organismo en particular.**

Un GEM reúne **todas** las reacciones metabólicas que permite el genoma de un organismo, con su estequiometría, sus compartimentos y la asociación con los genes que codifican cada enzima. Es la pieza central de la clase de [[Ingrid Persitz]] y la herramienta que permite pasar de la [[Ingeniería metabólica]] "de a una pieza" a razonar sobre la red completa.

## Cómo se construye

| Paso | Qué se obtiene | Recursos mencionados |
|---|---|---|
| 1 | Secuencia de ADN → **genoma anotado** | — |
| 2 | Funciones enzimáticas → **red metabólica** (reacciones, metabolitos, compartimentos) | [[KEGG]], [[ModelSEED y KBase\|KBase, ModelSEED]] |
| 3 | Red → **modelo estequiométrico** `dc/dt = S·v` (1986) | [[Matriz estequiométrica]] |
| 4 | Análisis: [[Modelado basado en restricciones\|restricciones]], [[Análisis de modos elementales\|modos elementales]] (1994), [[Flux Balance Analysis\|FBA]] (1993) | [[openCOBRA]] |

Los compartimentos importan: un mismo metabolito en citosol y en mitocondria son dos filas distintas de la matriz, y moverlo entre ellos es una reacción de transporte más.

## Dónde conseguirlos

En repositorios de modelos curados como [[BiGG Models]], que distribuye los modelos en [[SBML]], JSON o MAT. Ejemplos de la clase:

| Modelo | Organismo | Tamaño |
|---|---|---|
| **iML1515** | *[[Escherichia coli]]* K-12 MG1655 | 1877 metabolitos · 2712 reacciones · 1516 genes |
| [[Yeast9]] | *[[Saccharomyces cerevisiae]]* | Usado en el caso de co-consumo |
| **iMM904** | *S. cerevisiae* | Precargado en [[PECA]] |
| *E. coli core* | *E. coli* (versión reducida) | Ejemplo de [[StrainDesign]] |

## Para qué sirven

- Predecir el crecimiento y los flujos con [[Flux Balance Analysis|FBA]].
- Delimitar todo lo que el organismo *puede* hacer: el [[Espacio de flujos factible]].
- Buscar intervenciones genéticas ([[Knock-out y knock-in|KO y KI]]) con [[Diseño computacional de cepas|diseño computacional de cepas]].

## Limitación de fondo

El modelo es tan bueno como su reconstrucción: una reacción que falta o una anotación errónea cambia el espacio factible y, por lo tanto, las predicciones. Por eso los diseños que salen del modelo necesitan validación experimental dentro del [[Ciclo DBTL]].

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
- [[Maarleveld et al 2013 - Basic concepts of stoichiometric modeling of metabolic networks]] *(lectura)*
- [[Schneider et al 2022 - StrainDesign]] *(lectura)*
