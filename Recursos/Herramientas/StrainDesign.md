---
tags: [herramienta, software, ingeniería-metabólica]
area: Herramientas
aliases: [strain design tool, Schneider et al. 2022]
---

# StrainDesign

Herramienta de [[Diseño computacional de cepas]] publicada por **Schneider et al. (2022)**, y el eje de la segunda mitad de la clase.

> **StrainDesign: a systematic way to find these interventions.**

## Cómo funciona

1. Usa el algoritmo de **[[Minimal Cut Sets|Generalized Minimal Cut Sets]]**.
2. El usuario **codifica el fenotipo deseado como regiones del [[Espacio de flujos factible]] a PROTEGER (*PROTECT*) o SUPRIMIR (*SUPPRESS*)**.
3. La herramienta **encuentra conjuntos de intervenciones irreducibles** ([[Knock-out y knock-in|KO y KI]]) que dejan factible lo deseado e infactible lo indeseado.

El dibujo de la clase muestra el poliedro original, las regiones **P** (*growth on glucose*) y **S** (*growth on bananas*, deliberadamente absurdo para dejar claro que las regiones las define el usuario), y el espacio resultante donde S desapareció.

## Configuración del caso de estudio

| Parámetro | Valor |
|---|---|
| Modelo | [[Yeast9]] |
| Módulos SUPPRESS | 9 |
| Módulo PROTECT | 1 |
| Corridas independientes | 30 |
| Límite de tiempo | 30 min por corrida |
| Recursos | 32 núcleos de CPU, 128 GB de memoria |
| Costo máximo de intervención | 55 |

Resultado: 729 diseños aeróbicos y 158 anaeróbicos; **13 intervenciones alcanzan** para forzar el [[Co-consumo de azúcares|co-consumo]].

## Otras aplicaciones

> **¡Cualquiera que se nos ocurra!** Pasos: lista de reacciones → agregarlas al modelo → definir los fenotipos deseados → correr el modelo.

Ejemplo mencionado: **fijación de CO₂ en *[[Escherichia coli|E. coli]]***, con una proyección del espacio de flujos (`BIOMASS_Ecoli_core_w_GAM` vs `EX_14bdo_e`) donde se ven las regiones coloreadas del espacio.

## El diagnóstico

> **Flexible but underused framework.**

Es potente y general, pero no llega a los ingenieros metabólicos experimentales. Esa brecha es la que intenta cerrar [[PECA]].

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
