---
tags: [lectura, modulo-2, modelos-metabolicos, fba]
area: Lecturas
tipo: review
autores: Timo R. Maarleveld, Ruchir A. Khandelwal, Brett G. Olivier, Bas Teusink, Frank J. Bruggeman
año: 2013
revista: Biotechnology Journal 8, 997–1008
doi: 10.1002/biot.201200291
aliases: [Maarleveld 2013, Maarleveld et al. 2013, Basic concepts and principles of stoichiometric modeling of metabolic networks]
---

# Maarleveld et al. (2013) — *Basic concepts and principles of stoichiometric modeling of metabolic networks*

> [!info] Ficha de la lectura
> **Tipo:** review didáctica — *Biotechnology Journal* (número especial *Metabolic Modeling and Simulation*)
> **Autores:** Maarleveld, Khandelwal, Olivier, Teusink y Bruggeman (Systems Bioinformatics, VU Amsterdam)
> **Clase asociada:** [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]] (clase 5)
> **PDF:** [[Maarleveld et al 2013 - Basic concepts of stoichiometric modeling of metabolic networks.pdf]]

## En una frase

La base matemática de la sección 4 de la clase ("de la red a los flujos"): cómo todo el modelado basado en restricciones sale de **una sola matriz**, la [[Matriz estequiométrica]], y qué significa cada objeto derivado de ella —espacio nulo, modos de flujo, FBA, FVA— en términos de **rutas de la red**.

## Por qué leerla después de la clase

La clase presenta `S·v = 0`, los límites de flujo, el [[Espacio de flujos factible|poliedro factible]], el [[Análisis de modos elementales]] y el [[Flux Balance Analysis|FBA]] en una sola diapositiva. Este paper los desarrolla uno por uno sobre una **red de juguete** (26 reacciones, 23 metabolitos) y sobre el modelo de *[[Escherichia coli]]* **iAF1260**, con interpretación biológica. Suma además dos herramientas que la clase no menciona: **FVA** y los **precios sombra**.

> [!note] Notación
> El paper llama **N** a la matriz estequiométrica y **J** al vector de flujos en estado estacionario (la clase usa **S** y **v**).

---

## 1. Balance de masa: todo empieza en la matriz

- Cada reacción conserva átomos y carga. La tasa de cambio de cada metabolito es la suma de las reacciones que lo producen menos las que lo consumen: **dx/dt = N · v**.
- **N** tiene *m* filas (metabolitos) y *r* columnas (reacciones). Entrada negativa = sustrato, positiva = producto.
- Los metabolitos **de borde** (concentración fija, p. ej. nutrientes del medio) **no** entran en N: son parámetros.
- La cinética enzimática queda dentro de **v**; el modelado estequiométrico la deja afuera a propósito.

## 2. Conservación de restos químicos (*moiety conservation*)

Algunos metabolitos solo se **reciclan** (ATP, NAD(P)H, coenzima A): su total es constante, p. ej. `A_T = ATP + ADP + AMP`. Eso crea **dependencias lineales entre filas** de N (se obtienen del espacio nulo izquierdo) → el número de metabolitos **independientes** es el **rango** de N. En los GEMs, la [[Reacción de biomasa]] "drena" estos restos, así que formalmente desaparecen, pero siguen siendo importantes para la dinámica porque el recambio de ATP es mucho más rápido que su síntesis → ver [[Cofactores energéticos]].

## 3. Estado estacionario y modos de flujo

- En estado estacionario **N·J = 0**. Hay más flujos que ecuaciones (*r* > *m₀*): el sistema está **subdeterminado** → no hay un flujo único, hay un **espacio de soluciones**, el **espacio nulo derecho** (matriz *kernel* K).
- Número de flujos independientes = *r* − rango(N). En la red de juguete: 26 − 19 = **7** modos de flujo.
- Cada columna de K es un **modo de flujo**: una ruta de la red en la que todos los metabolitos internos están balanceados — necesariamente un **ciclo** o un **camino de fuente a sumidero**.
- Problema: K no es única y puede violar la termodinámica (flujos negativos en reacciones irreversibles). De ahí las definiciones que siguen.

## 4. Flux Balance Analysis (FBA)

- Achica el espacio eligiendo los flujos que **optimizan un objetivo** biológico (biomasa, ATP), con programación lineal: `max Z = c·J` sujeto a `N·J = 0` y `J_min ≤ J ≤ J_max`.
- Los límites pueden venir de mediciones experimentales o de la termodinámica (irreversibilidad).
- En *E. coli* iAF1260 en medio mínimo con glucosa (8 mmol/g/h) y O₂ (18,5 mmol/g/h): tasa de crecimiento predicha **0,73 h⁻¹**, y solo **18 %** de las reacciones llevan flujo.
- La solución óptima **no suele ser única**: hay todo un espacio de soluciones óptimas.

## 5. [[Flux Variability Analysis]] (FVA)

Fijado el óptimo de FBA, **maximiza y minimiza cada flujo** por separado → rango (*span*) de cada reacción dentro del espacio óptimo.

| Span | Interpretación |
|---|---|
| 0 y flujo ≠ 0 | Reacción **esencial** para el óptimo |
| 0 y flujo = 0 | Reacción inactiva (usarla daría una solución subóptima) |
| Finito | Hay rutas alternativas equivalentes |
| Infinito (o enorme) | La reacción participa de un **ciclo** sin conversión neta |

En iAF1260, **94 %** de los flujos quedan fijos en el óptimo y solo **6 %** pueden variar; la mitad de esos variables tiene span infinito por ciclos.

> [!tip] Conexión con StrainDesign
> [[StrainDesign]] usa FVA en su preprocesamiento para detectar reacciones esenciales para el fenotipo protegido y descartarlas como blancos de *knock-out* → [[Schneider et al 2022 - StrainDesign]].

## 6. Sensibilidades de la solución de FBA

- **Costo reducido**: cuánto cambia el objetivo si aumento un flujo. En los flujos de captación indica qué nutriente **limita** el crecimiento y cuál convendría agregar al medio.
- **Precio sombra**: cuánto cambia el objetivo si relajo una restricción (si agrego un metabolito).

## 7. Modos elementales (EFMs) y rutas extremas (ExPas)

Caracterizan el espacio **sin** suponer un objetivo (a diferencia de FBA), solo con la estequiometría → ver [[Análisis de modos elementales]].

| | Condiciones | Relación |
|---|---|---|
| **EFM** | (i) estado estacionario, (ii) termodinámicamente factible, (iii) **no descomponible** (ningún subconjunto cumple i y ii) | Cualquier flujo estacionario es combinación convexa de EFMs |
| **ExPa** | Las tres anteriores + reconfiguración de la red (reversibles partidas en dos) + independencia sistémica | Las ExPas son un **subconjunto** de los EFMs: las aristas del cono de flujos |

Tipos de EFMs: **I** rutas de rendimiento óptimo, **II** subóptimo, **III** ciclos internos. La red de juguete tiene 28 EFMs (24 + 1 + 3); sin los tres ciclos tendría solo 5 → los ciclos son los que **disparan** la cantidad. Enumerarlos es **NP-hard**, por eso no escalan a GEMs completos.

## 8. El espacio óptimo como poliedro: CoPE-FBA

El conjunto de soluciones óptimas de FBA es un poliedro con **vértices** (rutas óptimas), **rayos** (ciclos irreversibles) y **linealidades** (ciclos reversibles). CoPE-FBA lo resume en pocas **subredes** independientes: en iAF1260 hay ~**1,7 millones de vértices**, pero solo **4 subredes** (≈5 % de las reacciones) explican toda la variabilidad óptima.

## 9. Supuestos y límites (lo que conviene recordar)

- **Estado estacionario**: justificado por la separación de escalas de tiempo (metabolismo rápido, regulación génica lenta).
- **Optimalidad**: FBA en realidad optimiza un **rendimiento** (objetivo / entrada limitante), no una **tasa**; seleccionar por rendimiento solo tiene sentido sin competencia por nutrientes. Puede haber varios objetivos en conflicto (**óptimo de Pareto**).
- Extensiones: FBA dinámico, restricciones de espacio o recursos, FBA multiespecie — coherente con las limitaciones que señala la clase (**sin cinética ni regulación**).

## Conceptos del vault

[[Modelado basado en restricciones]] · [[Matriz estequiométrica]] · [[Espacio de flujos factible]] · [[Flux Balance Analysis]] · [[Flux Variability Analysis]] · [[Análisis de modos elementales]] · [[Reacción de biomasa]] · [[Modelo metabólico a escala genómica]] · [[Cofactores energéticos]] · [[Escherichia coli]] · [[SBML]] · [[StrainDesign]]

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
- [[Módulo 2 - MOC]]
