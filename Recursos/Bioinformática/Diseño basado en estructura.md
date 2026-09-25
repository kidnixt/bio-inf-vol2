---
tags: [concepto, bioinformática, fármacos, estructura]
area: Bioinformática
aliases: [SBDD, Structure-Based Drug Design, diseño basado en estructura del blanco]
---

# Diseño basado en estructura

La rama del [[Diseño de fármacos asistido por computadora|CADD]] que **diseña dentro del sitio de unión** de un blanco cuya forma tridimensional se conoce o se predice.

## El flujo

| 1 · Estructura | 2 · Preparar | 3 · Explorar | 4 · Evaluar |
|---|---|---|---|
| Proteína o complejo | Protonación y aguas | Poses y conformaciones | Score, física, ensayo |

**Pregunta típica:** *¿Cómo podría una molécula reconocer y modular este sitio?*

| Fortaleza | Riesgo |
|---|---|
| Propone un **mecanismo 3D** | **Estructura o score incorrectos** |

El paso 2 no es trámite: qué residuos están protonados y qué aguas se conservan en el sitio cambia el resultado del [[Docking molecular|docking]].

## De dónde sale la estructura

| Experimental | Predicha |
|---|---|
| [[Cristalografía de rayos X]], RMN, Cryo-EM → [[PDB]] | [[Modelado por homología]], [[Threading]], [[AlphaFold]] → [[AlphaFold DB]] |

## Sus métodos

- **[[Docking molecular]]** — generar poses y ordenarlas con una [[Función de puntuación|función de puntuación]].
- **[[Dinámica molecular]]** — tratar el complejo como una trayectoria, no una foto.
- **[[Energía libre de unión]]** — estimar la afinidad con métodos de física estadística.
- **[[Virtual screening]]** jerárquico — aplicar lo anterior en cascada sobre bibliotecas enormes.

## Casos del curso

- **Zanamivir** (1993): diseño racional sobre la neuraminidasa, el caso fundacional.
- **[[Casos de éxito del diseño computacional de fármacos|DRD4]]** (2019): docking de 138 millones de moléculas → 81 quimiotipos nuevos.
- **Nirmatrelvir** (2021): inhibidor oral de Mpro del SARS-CoV-2.

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
- [[Fahim 2026 - Structure-based design of antiviral and antihypertensive drugs]] *(lectura)*
- [[Nazarova et al 2026 - V-SYNTHES2]] *(lectura)*
- [[Wang et al 2024 - Active learning in drug discovery]] *(lectura)*
