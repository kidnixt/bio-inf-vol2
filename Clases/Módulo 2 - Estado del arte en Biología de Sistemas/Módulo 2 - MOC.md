---
tags: [MOC, modulo-2]
---

# Módulo 2 — Estado del arte en Biología de Sistemas

Índice del módulo. Curso **Fronteras y Perspectivas en Bioinformática** — Universidad ORT, 2026.

## Clases

| # | Clase | Docente | Material del curso |
|---|---|---|---|
| 4 | *(sin material todavía)* | — | — |
| 5 | [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]] | [[Ingrid Persitz]] | [[Diapositivas - Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica.pdf\|diapositivas]] · [[Resumen - Modelos metabólicos.pdf\|resumen]] · 2 lecturas |

> [!note] Pendiente
> De la clase 4 (primera del módulo) no hay diapositivas, resumen ni lecturas. Cuando llegue, el material va en `Módulo 2 - Estado del arte en Biología de Sistemas/Clase 4 - <tema>/` y el resumen en esta carpeta.

## Lecturas

| Clase | Lectura | En una línea |
|---|---|---|
| 5 | [[Maarleveld et al 2013 - Basic concepts of stoichiometric modeling of metabolic networks]] | La base matemática del modelado estequiométrico: matriz S, FBA, FVA, modos elementales |
| 5 | [[Schneider et al 2022 - StrainDesign]] | El paper de la herramienta de diseño de cepas que usa la clase |

## El hilo conductor del módulo

Si el [[Módulo 1 - MOC|Módulo 1]] era sobre **generar** datos a escala (célula única, espacio, lecturas largas), este módulo es sobre **modelar el sistema completo**. La clase 5 lo plantea como un salto de escala en la forma de intervenir un organismo:

| Enfoque | Unidad de trabajo | Qué se pierde |
|---|---|---|
| [[Ingeniería metabólica]] clásica | Un gen → una enzima → una [[Vía metabólica\|vía]] | Los efectos en el resto de la red |
| [[Modelo metabólico a escala genómica\|Modelos a escala genómica]] + [[Diseño computacional de cepas\|diseño computacional]] | La red metabólica completa | Cinética, regulación y dinámica temporal |

Y una tensión que la clase deja explícita y que conecta con el resto del curso: los métodos existen, funcionan y **no llegan a quienes hacen los experimentos**. *There is a gap to bridge.*

## Mapa de conceptos del módulo

### Modelado metabólico

[[Modelo metabólico a escala genómica]] · [[Matriz estequiométrica]] · [[Modelado basado en restricciones]] · [[Espacio de flujos factible]] · [[Flux Balance Analysis]] · [[Flux Variability Analysis]] · [[Análisis de modos elementales]] · [[Reacción de biomasa]] · [[SBML]]

### Diseño de cepas

[[Diseño computacional de cepas]] · [[Minimal Cut Sets]] · [[Knock-out y knock-in]] · [[Co-consumo de azúcares]]

### Ingeniería metabólica y biología sintética

[[Ingeniería metabólica]] · [[Biología sintética]] · [[Ciclo DBTL]] · [[Evolución adaptativa de laboratorio]]

### Biología y metabolismo

[[Vía metabólica]] · [[Glucólisis]] · [[Vía de las pentosas fosfato]] · [[Pentosas]] · [[Vías de asimilación de pentosas]] · [[Cofactores energéticos]] · [[Catabolismo y anabolismo]]

### Organismos

[[Saccharomyces cerevisiae]] · [[Escherichia coli]]

### Herramientas, bases de datos y modelos

[[BiGG Models]] · [[KEGG]] · [[MetaCyc]] · [[ModelSEED y KBase]] · [[openCOBRA]] · [[StrainDesign]] · [[Yeast9]] · [[PECA]]

### Personas

[[Ingrid Persitz]]

## Conexiones con el Módulo 1

- El cierre de [[Biología espacial - mapeando la expresión génica a su entorno]] plantea el paso de **datos a conocimiento** vía integración — un GEM es justamente eso: integrar el genoma anotado en un modelo predictivo.
- La [[Integración de datos multiómicos|integración multiómica]] reaparece acá como uno de los avances computacionales que habilitaron la ingeniería metabólica de sistemas.
- [[Machine Learning]] e [[Inteligencia Artificial]] vuelven a aparecer como frente de avance, y son el tema del [[Módulo 3 - MOC|Módulo 3]].

## Navegación

- Curso completo → [[Fronteras y Perspectivas en Bioinformática - MOC]]
- Módulo anterior → [[Módulo 1 - MOC]]
- Siguiente módulo → [[Módulo 3 - MOC]]
