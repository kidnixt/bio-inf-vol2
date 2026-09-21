---
tags: [concepto, técnica, metodología]
area: Técnicas
aliases: [DBTL, Design-Build-Test-Learn, ciclo de diseño, design build test learn]
---

# Ciclo DBTL

El ciclo iterativo estándar de la [[Biología sintética]] y la [[Ingeniería metabólica]]. La clase lo usa para ubicar dónde entran los modelos metabólicos.

| Fase | Qué incluye |
|---|---|
| **Design** | Definir el problema · selección del hospedero (*host selection*) · selección de vías (*pathway selection*) · diseño de experimentos (promotores, RBS, enzimas) · **modelado** |
| **Build** | Ensamblado de partes · modificación del hospedero · ensamblado combinatorio · automatización |
| **Test** | Química analítica · screening · automatización |
| **Learn** | Análisis de vías · reglas de diseño · rediseño de experimentos |

## Dónde viven los modelos

- En **Design**: un [[Modelo metabólico a escala genómica]] permite proponer intervenciones antes de tocar una pipeta; el [[Diseño computacional de cepas]] lo hace de forma sistemática.
- En **Learn**: los resultados experimentales se usan para corregir el modelo y las reglas de diseño, y arranca otra vuelta.

Que el ciclo sea iterativo es importante para leer los resultados del caso de estudio: los diseños que produce [[StrainDesign]] son **hipótesis** que hay que construir y testear, no cepas terminadas.

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
