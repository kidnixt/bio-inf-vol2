---
tags: [concepto, bioinformática, fármacos]
area: Bioinformática
aliases: [VS, cribado virtual, virtual screening jerárquico, VS jerárquico, LBVS, SBVS]
---

# Virtual screening

> El **Virtual Screening (VS)** es una herramienta utilizada en el proceso moderno de descubrimiento de fármacos para **identificar nuevos *leads*** y moléculas similares a los fármacos para las intervenciones terapéuticas.

Es la aplicación a escala de los métodos del [[Diseño de fármacos asistido por computadora|CADD]]: en vez de evaluar una molécula, se evalúan millones y se ordenan.

## El embudo jerárquico

La idea central: **cada nivel aplica un filtro más caro sobre menos moléculas**.

| Nivel | Moléculas |
|---|---|
| Biblioteca ([[ZINC]], REAL Space) | **10⁸–10¹⁰** |
| [[Docking molecular\|Docking]] rápido | 10⁵ |
| *Rescoring* | 10³ |
| **Ensayo experimental** | **10–100** |

Siete a nueve órdenes de magnitud entre lo que se puede enumerar y lo que se puede medir. Todo el diseño del pipeline consiste en **no descartar demasiado temprano lo que importa**.

## Sus dos sabores

- **LBVS** (basado en ligandos): [[Similitud química]], [[Farmacóforo|farmacóforos]], modelos [[QSAR]].
- **SBVS** (basado en estructura): [[Docking molecular|docking]] y [[Función de puntuación|scoring]] contra el sitio de unión.

En la práctica se combinan: farmacóforo y QSAR **reducen** la biblioteca, el docking **examina la pose** y el ensayo **confirma la actividad**.

## Los casos de escala

- **DRD4** (2019): 138 millones de moléculas dockeadas → 81 quimiotipos nuevos, 30 activos submicromolares, un agonista optimizado a 180 pM.
- **V-SYNTHES2** (2026): **3,8 M de dockings aproximados** para representar un espacio de **36 mil millones**, mediante enumeración jerárquica y selección geométrica de fragmentos.
- **Halicina** (2020): >107 M de moléculas evaluadas virtualmente con un modelo entrenado sobre solo 2.335.

Ver [[Casos de éxito del diseño computacional de fármacos]] y [[Cribado virtual inverso]] (el problema al revés: buscar el blanco de una molécula).

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
- [[Fahim 2026 - Structure-based design of antiviral and antihypertensive drugs]] *(lectura)*
- [[Fang et al 2026 - A comprehensive review of AI in drug design]] *(lectura)*
- [[Nazarova et al 2026 - V-SYNTHES2]] *(lectura)*
- [[Wang et al 2024 - Active learning in drug discovery]] *(lectura)*
