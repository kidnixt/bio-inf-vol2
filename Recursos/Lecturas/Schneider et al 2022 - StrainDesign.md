---
tags: [lectura, modulo-2, diseno-de-cepas, software]
area: Lecturas
tipo: application note (software)
autores: Philipp Schneider, Pavlos Stephanos Bekiaris, Axel von Kamp, Steffen Klamt
año: 2022
revista: Bioinformatics 38(21), 4981–4983
doi: 10.1093/bioinformatics/btac632
aliases: [Schneider 2022, Schneider et al. 2022, "StrainDesign: a comprehensive Python package for computational design of metabolic networks"]
---

# Schneider et al. (2022) — *StrainDesign: a comprehensive Python package for computational design of metabolic networks*

> [!info] Ficha de la lectura
> **Tipo:** *Applications Note* — *Bioinformatics* (acceso abierto)
> **Autores:** Schneider, Bekiaris, von Kamp y Klamt (Max Planck Institute for Dynamics of Complex Technical Systems, Magdeburgo)
> **Clase asociada:** [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]] (clase 5)
> **PDF:** [[Schneider et al 2022 - StrainDesign.pdf]]
> **Código:** `github.com/klamt-lab/straindesign` (también en PyPI, Anaconda y en la interfaz gráfica de CNApy)

## En una frase

El paper de la herramienta que [[Ingrid Persitz]] usó en su tesis: **un solo paquete de Python** que reúne los principales algoritmos de [[Diseño computacional de cepas|diseño de cepas]] basados en programación lineal entera mixta (MILP), incluidos los [[Minimal Cut Sets]], y permite **combinarlos**.

## Por qué leerla después de la clase

En la clase, [[StrainDesign]] aparece como "el método de Schneider et al. (2022)" con las regiones **PROTECT / SUPPRESS**, y cierra con *"flexible but underused framework"*. Este paper explica qué hay debajo: qué algoritmos integra, cómo se especifica un problema y qué hace el preprocesamiento para que escale a modelos genómicos.

---

## 1. El problema que resuelve

- Desde **OptKnock** (2003, el primer método de diseño con MILP basado en **producción acoplada al crecimiento**) aparecieron muchísimos métodos, pero **dispersos** en herramientas distintas: COBRA Toolbox y CellNetAnalyzer (MATLAB), OptFlux (Java), COBRApy, cameo, MEWpy, OptCouple (Python)…
- Cada una implementa uno o pocos métodos; **ninguna** combinaba optimización bi-nivel (OptKnock, RobustKnock, OptCouple) con el enfoque general de MCS.

## 2. Qué integra

| Módulo | Idea |
|---|---|
| **OptKnock** | Bi-nivel: maximizar el producto suponiendo que la célula maximiza su crecimiento |
| **RobustKnock** | Versión robusta: garantiza producción incluso en el peor caso dentro del óptimo de crecimiento |
| **OptCouple** | Busca acoplar producción y crecimiento |
| **MCS** ([[Minimal Cut Sets]]) | Conjuntos mínimos de intervenciones que **suprimen** fenotipos indeseados y **protegen** los deseados — el enfoque más general |

Lo novedoso es poder **combinar** módulos: por ejemplo, OptKnock para maximizar producción + una región "suprimir" tipo MCS que elimina soluciones con baja producción al crecimiento máximo → producción acoplada **garantizada** (algo que OptKnock clásico no asegura). Otro ejemplo del paper: encontrar **letales sintéticos** como un problema MCS puro (mínimo número de *knock-outs* que vuelven inviable a la célula).

Con esto se pueden emular otros métodos: gMCS, cRegMCS, FOCAL, OptKnock con objetivo inclinado, ModCell2.

## 3. Tipos de intervención y opciones

- Intervenciones sobre **reacciones o genes** — con genes, se integran las **reglas GPR** (gen–proteína–reacción) comprimidas dentro de la red.
- **Adiciones** de reacciones o genes (*knock-ins*, p. ej. vías heterólogas) tratadas como "*knock-outs* inversos" → exactamente lo que usa el caso de estudio de la clase → [[Knock-out y knock-in]].
- Intervenciones **regulatorias** (vía pseudo-reacciones).
- Número de soluciones, tamaño máximo del conjunto de intervenciones, y admitir soluciones no mínimas para acelerar.

## 4. El preprocesamiento (lo que lo hace escalar)

1. Compresión de GPR y de la red (técnicas adaptadas de **efmtool**) → problema más chico.
2. **[[Flux Variability Analysis|FVA]]** para identificar reacciones esenciales del fenotipo protegido → se descartan como blancos → ver FVA en [[Maarleveld et al 2013 - Basic concepts of stoichiometric modeling of metabolic networks|Maarleveld et al. (2013)]].
3. Construcción automática del MILP a partir de un mínimo de input del usuario.

## 5. Implementación

- Trabaja sobre modelos de **COBRApy** (ecosistema [[openCOBRA]]).
- Solvers: **GLPK** (incluido, para problemas chicos), **CPLEX**, **Gurobi** y **SCIP**. Las *indicator constraints* de estos solvers evitan problemas numéricos y aceleran.
- Herramientas de análisis: gráficos 2D/3D de flujos o rendimientos (p. ej. envolventes de producción vs crecimiento).
- Interfaz gráfica en **CNApy** para no programadores, con visualización de las intervenciones sobre el mapa de la red.

> [!note] Relación con la clase y el resumen del docente
> El resumen de la clase lista como herramientas **COBRApy**, CBMPy, PySCeS, Escher y los solvers **Gurobi** y **CPLEX** — StrainDesign se apoya justamente en COBRApy y en esos solvers. Y la limitación que menciona Persitz ("la búsqueda combinatoria de intervenciones requiere alta capacidad de cómputo y límites de tiempo por simulación") es la contracara de resolver MILPs sobre un GEM completo como [[Yeast9]].

## Conceptos del vault

[[StrainDesign]] · [[Diseño computacional de cepas]] · [[Minimal Cut Sets]] · [[Knock-out y knock-in]] · [[Modelado basado en restricciones]] · [[Flux Balance Analysis]] · [[Flux Variability Analysis]] · [[Espacio de flujos factible]] · [[Modelo metabólico a escala genómica]] · [[openCOBRA]] · [[Ingeniería metabólica]]

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
- [[Módulo 2 - MOC]]
