---
tags: [lectura, modulo-3, fármacos, SBDD]
area: Lecturas
tipo: review
autores: Asmaa M. Fahim
año: 2026
revista: Computational Biology and Chemistry 120, 108663
doi: 10.1016/j.compbiolchem.2025.108663
aliases: [Fahim 2026, "Structure-based drug design - computational strategies in drug discovery, antihypertensive agents, antiviral drugs"]
---

# Fahim (2026) — *Structure-based drug design; computational strategies in drug discovery: antihypertensive agents, antiviral drugs, molecular docking, QSAR*

> [!info] Ficha de la lectura
> **Tipo:** review — *Computational Biology and Chemistry*
> **Autora:** Asmaa M. Fahim (Department of Green Chemistry, National Research Centre, El Cairo)
> **Clase asociada:** [[Métodos para el diseño computacional de fármacos]] (clase 6)
> **PDF:** [[Fahim 2026 - Structure-based design of antiviral and antihypertensive drugs.pdf]]

## En una frase

El recorrido **caso por caso** de fármacos reales diseñados con [[Diseño basado en estructura|SBDD]]: qué se hizo en cada uno, con qué herramienta computacional, y cómo se sintetizó.

## Por qué leerla después de la clase

La clase lista cuatro [[Casos de éxito del diseño computacional de fármacos|casos de éxito]] en una diapositiva (zanamivir, DRD4, halicina, nirmatrelvir). Esta revisión es la versión larga de esa diapositiva: toma una decena de fármacos y para cada uno desarrolla la ruta sintética, el SAR, el docking y el perfil [[ADMET]].

Es la lectura menos "de frontera" del módulo y la más **de oficio**: sirve para ver cómo se ve el trabajo real cuando el cómputo es una parte y no el todo.

---

## 1. Los casos

| Área | Fármacos |
|---|---|
| **Antihipertensivos** | **Captopril** (inhibidor de ECA), **dorzolamide** (inhibidor de anhidrasa carbónica), **aliskiren** (inhibidor directo de renina) |
| **Antivirales — inhibidores de proteasa del VIH** | Saquinavir, ritonavir, indinavir, amprenavir |
| **Influenza** | **Oseltamivir** (Tamiflu) |
| **SARS-CoV-2** | **Nirmatrelvir/ritonavir** (Paxlovid) |

Los dos últimos y el captopril son los que la clase menciona al pasar; acá cada uno tiene su sección con síntesis, SAR y análisis computacional.

## 2. Los temas que atraviesan los casos

- **Síntesis estereoselectiva.** La quiralidad no es un detalle: la actividad depende del enantiómero, y la ruta tiene que producirlo.
- **Farmacóforos quelantes de metales.** El grupo sulfonamida (–SO₂NH₂) de dorzolamide coordinando el zinc de la anhidrasa carbónica, con His94, His119 y His96 — un [[Farmacóforo|farmacóforo]] que existe *porque* hay un metal en el sitio activo.
- **Propiedades moleculares racionales**, en la línea de las [[Reglas de drug-likeness]].
- **Docking + [[Dinámica molecular|MD]] + [[QSAR]] + ADMET** aplicados en conjunto para mejorar selectividad, seguridad y confiabilidad terapéutica.

## 3. Reposicionamiento y cribado virtual

Las secciones finales cubren [[Reposicionamiento de fármacos|reposicionamiento]] y [[Virtual screening|cribado virtual]] como refuerzos del arsenal, con una observación honesta sobre la pandemia: los enfoques computacionales de reposicionamiento **no siempre dieron los resultados clínicos esperados**.

## 4. Qué aporta respecto de la clase

- **Profundidad en los casos** que la clase solo nombra. Si algo faltaba en la diapositiva de casos de éxito era el *cómo*.
- **El vínculo entre química sintética y cómputo.** La clase lo enuncia en su primera parte —*"cómputo y experimento comparten un ciclo"*— y esta revisión lo muestra: cada fármaco tiene su esquema de síntesis al lado de su análisis de docking.
- Refuerza la frase de cierre de la clase: **éxito = hipótesis computacional + química + ensayo + desarrollo.**

> [!warning] Leerla con criterio
> Es una revisión amplia y con redacción despareja, más catálogo que argumento. Lo valioso son los casos y los esquemas; no es la fuente a citar para afirmaciones metodológicas generales — para eso están [[Fang et al 2026 - A comprehensive review of AI in drug design|Fang et al.]] y [[Nazarova et al 2026 - V-SYNTHES2|Nazarova et al.]]

## Conceptos del vault

[[Diseño basado en estructura]] · [[Docking molecular]] · [[QSAR]] · [[ADMET]] · [[Farmacóforo]] · [[Dinámica molecular]] · [[Reposicionamiento de fármacos]] · [[Virtual screening]] · [[Casos de éxito del diseño computacional de fármacos]] · [[Reglas de drug-likeness]] · [[Blanco terapéutico]]

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
- [[Módulo 3 - MOC]]
