---
tags: [lectura, modulo-3, fármacos, IA]
area: Lecturas
tipo: review
autores: Yi Fang, Xiaoyong Pan, Hong-Bin Shen
año: 2026
revista: Digital Discovery 5, 3178–3197
doi: 10.1039/d5dd00549c
aliases: [Fang 2026, AIDD review, "A comprehensive review of artificial intelligence in drug design - methods, applications, and challenges"]
---

# Fang et al. (2026) — *A comprehensive review of artificial intelligence in drug design: methods, applications, and challenges*

> [!info] Ficha de la lectura
> **Tipo:** review — *Digital Discovery* (RSC, CC-BY-NC)
> **Autores:** Shanghai Jiao Tong University
> **Clase asociada:** [[Métodos para el diseño computacional de fármacos]] (clase 6)
> **PDF:** [[Fang et al 2026 - A comprehensive review of AI in drug design.pdf]]

## En una frase

La revisión de la que sale la diapositiva *"Mapa de la IA en descubrimiento"* de la clase (el DOI `10.1039/d5dd00549c` está impreso ahí): un recorrido por representaciones, bases de datos, las tres subtareas del **AIDD** y —lo más valioso— **cómo se evalúan**.

## Por qué leerla después de la clase

Porque es el mapa completo del que la clase muestra una figura. Y porque su sección 7 es la que no existe en ninguna otra lectura del módulo: **un panorama sistemático de las métricas de evaluación**, que es justamente donde la clase advierte que hay que tener cuidado.

---

## 1. La estructura de la revisión

| § | Tema |
|---|---|
| 2 | [[Representaciones moleculares]]: strings, grafos, fingerprints |
| 3 | Bases de datos públicas para construir modelos |
| 4–6 | Las tres subtareas del AIDD (abajo) |
| **7** | **Métricas de evaluación** |
| 8 | Limitaciones y direcciones futuras |

## 2. Las tres subtareas

| Subtarea | Qué hace |
|---|---|
| **Cribado virtual con IA** | Integra estrategias basadas en ligando y en estructura, con modelos discriminativos y generativos |
| **Diseño *de novo* con IA** | Modelos generativos que navegan el espacio químico, superando las limitaciones de datos de las bases existentes |
| **Optimización de propiedades** | Refinamiento **multiobjetivo**: [[ADMET]], QED (*quantitative estimate of druglikeness*), SAscore (accesibilidad sintética), logP |

## 3. La asimetría de datos, otra vez

El paper la pone en tres números:

| | |
|---|---|
| Escala de las bases moleculares | ~10⁹ |
| Moléculas bioactivas | ~10⁶ |
| Fármacos de molécula pequeña aprobados por la FDA | **~2.000** |

Es la misma pirámide que la clase arma con [[ZINC]] → [[ChEMBL]] → [[PDBbind]], y el argumento es idéntico: **cribar es necesario porque medir no escala**.

## 4. La sección de métricas (lo más útil)

El foco de la evaluación **cambia según la subtarea**:

| Subtarea | Qué se prioriza |
|---|---|
| Cribado virtual | Afinidad de unión y propiedades [[ADMET]] |
| Optimización de propiedades | QED, SAscore, logP, energía |
| Generación *de novo* | Un abanico amplio: métricas 2D topológicas **y** 3D geométricas |

Las clasifica en cuatro grupos: **2D**, **3D**, basadas en propiedades, y de **potencia in vitro**. Y advierte lo que hay que mirar en las 3D: como muchos enfoques generativos modelan todos los átomos explícitamente, **los enlaces tienen que inferirse de distancias euclídeas** y los criterios de estabilidad atómica son **más estrictos** que en 2D.

> [!tip] Conexión con la tesis de Johny
> Este es el paper del módulo más cercano al capítulo 1 de la tesis, pero **del lado de las moléculas pequeñas**: la afirmación de que la selección de métricas alineadas con el objetivo de la tarea *"es significativa"* y que entenderlas es *"fundamental para el benchmarking efectivo"* es la misma tesis, aplicada a otro dominio. Buen material para la introducción del informe del curso.

## 5. Una limitación que el paper reconoce

En optimización multiobjetivo, muchos algoritmos convierten varios objetivos en uno solo por **suma ponderada**. Eso ignora las correlaciones implícitas entre propiedades, y el desempeño queda **muy sensible a los pesos**. Además, propiedades computadas como QED y SAscore **no funcionan bien para todas las moléculas**.

Es decir: la métrica que se usa para optimizar es, ella misma, un proxy discutible.

## Conceptos del vault

[[Diseño de fármacos asistido por computadora]] · [[Representaciones moleculares]] · [[Virtual screening]] · [[ADMET]] · [[Reglas de drug-likeness]] · [[Función de puntuación]] · [[Docking molecular]] · [[Deep Learning]] · [[Inteligencia Artificial]] · [[ChEMBL]] · [[ZINC]] · [[PDBbind]]

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
- [[Módulo 3 - MOC]]
