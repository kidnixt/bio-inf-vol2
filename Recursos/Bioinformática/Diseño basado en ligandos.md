---
tags: [concepto, bioinformática, fármacos]
area: Bioinformática
aliases: [LBDD, Ligand-Based Drug Design, diseño basado en ligando]
---

# Diseño basado en ligandos

La rama del [[Diseño de fármacos asistido por computadora|CADD]] que **aprende de moléculas con actividad conocida**, sin necesidad de la estructura del blanco.

## El flujo

| 1 · Datos | 2 · Representar | 3 · Aprender | 4 · Priorizar |
|---|---|---|---|
| Activos e inactivos | Descriptores o grafos ([[Representaciones moleculares]]) | Regla o modelo | Nuevas moléculas |

**Pregunta típica:** *¿Qué compuestos se parecen a patrones asociados con actividad?*

| Fortaleza | Riesgo |
|---|---|
| Aprovecha los **datos** que ya existen | **Extrapolar fuera del dominio** |

## Sus tres métodos clásicos

- **[[Similitud química]]** — moléculas parecidas tienden a compartir actividad (con el contraejemplo de los [[Activity cliff|activity cliffs]]).
- **[[Farmacóforo]]** — abstraer la molécula como un patrón espacial de interacciones; útil cuando ligandos **distintos** comparten modo de unión.
- **[[QSAR]]** — modelo supervisado que predice actividad a partir de descriptores.

Los datos salen de [[ChEMBL]], [[BindingDB]] y [[PubChem]]; las moléculas a priorizar, de [[ZINC]].

## Casos del curso

- La **[[Casos de éxito del diseño computacional de fármacos|halicina]]** (2020): LBDD + [[Deep Learning|deep learning]] sobre datos fenotípicos, sin estructura ni mecanismo.
- Las ***p*-quinonas contra Chagas** de [[Andrés Ballesteros]]: LBDD donde los descriptores no son fingerprints sino **energías calculadas con química cuántica** (ΔG de semiquinona e hidroquinona, HOMO/LUMO/SUMO).
- Los **inhibidores de α-glucosidasa**: farmacóforo + 3D-QSAR sobre 51 xantonas para filtrar una biblioteca comercial.

En una situación real **se combina con [[Diseño basado en estructura|SBDD]]**: LBDD aporta patrones en datos, SBDD aporta hipótesis de unión, el experimento aporta medición, y la evidencia nueva realimenta ambos modelos.

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
