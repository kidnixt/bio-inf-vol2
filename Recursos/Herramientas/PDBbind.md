---
tags: [herramienta, base-de-datos, estructura, bioactividad]
area: Herramientas
aliases: [PDB bind]
---

# PDBbind

Base que une **estructura y afinidad**: complejos proteína–ligando del [[PDB]] con su medida de afinidad experimental asociada. Del equipo de **Renxiao Wang** (Fudan University), con portal en TopScience.

| | |
|---|---|
| Tipo de registro | Complejos proteína–ligando |
| Tamaño (corte) | **29.001** (v2025, publicada 08/02/2026) |
| Qué ofrece | Complejos 3D asociados a afinidades experimentales y archivos procesados |
| Consulta típica | *¿Qué complejos 3D disponen de una afinidad experimental asociada?* |

## Por qué es la base más importante y la más chica

Es el único recurso que responde la pregunta que el [[Diseño basado en estructura|SBDD]] necesita: *dada esta geometría, ¿cuán fuerte es la unión?*. Por eso es el conjunto de entrenamiento y evaluación estándar de:

- Las [[Función de puntuación|funciones de puntuación]] clásicas y aprendidas.
- Los modelos de **predicción de afinidad**.
- Casi todos los modelos de predicción de pose que lista la clase (DiffDock, KarmaDock, CarsiDock, Uni-Mol, EquiBind, E3Bind, SurfDock, NeuralPLexer…).

Y es **la base más chica de todas**: 2,9·10⁴ complejos, frente a 10⁶ compuestos con actividad medida y 10¹⁰ moléculas enumerables. Esa escasez es la razón estructural de por qué **[[Energía libre de unión|la afinidad sigue siendo difícil]]** incluso para modelos que ya predicen geometría muy bien.

> [!warning] Las advertencias de la clase
> **La estructura, el ligando y la medida deben corresponder** — no siempre el complejo cristalizado es el que se midió. Y **las versiones recientes tienen acceso de pago**, lo que complica la reproducibilidad de los benchmarks.

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
- [[Fang et al 2026 - A comprehensive review of AI in drug design]] *(lectura)*
