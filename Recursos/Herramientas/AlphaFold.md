---
tags: [herramienta, IA, estructura, deep-learning]
area: Herramientas
aliases: [AlphaFold2, AlphaFold3, AF2, AF3, ColabFold]
---

# AlphaFold

Sistema de **predicción de estructura de proteínas** basado en redes neuronales, de Google DeepMind. Es el método de IA que cambió la disponibilidad estructural en biología.

| Versión | Año | Qué aportó |
|---|---|---|
| **AlphaFold2** | 2021 (Jumper et al., *Nature*) | Amplió el acceso a **modelos de proteínas** con calidad cercana a la experimental |
| **AlphaFold3** | 2024 (Abramson et al., *Nature*) | Abordó **complejos** con ligandos, ácidos nucleicos e iones |

## AlphaFold3 y los complejos biomoleculares

Las predicciones de AlphaFold3 sobre cómo las proteínas se unen a ligandos **coinciden estrechamente con los datos experimentales**. Su arquitectura combina búsqueda de templados y de secuencias, un módulo de MSA, el *Pairformer* (48 bloques) y un **módulo de difusión**, con *recycling*.

| Fortalezas | Precauciones |
|---|---|
| Predicción **conjunta** de los componentes | Dependencia del entrenamiento |
| Mejor desempeño en varios *benchmarks* (frente a AutoDock Vina, RoseTTAFold All-Atom, AF-M 2.3) | **Estados biológicos alternativos** |
| Confianza **por región e interfaz** | **La afinidad todavía es difícil** |

Esa última precaución es la bisagra: predecir *dónde* y *cómo* se une algo no es lo mismo que predecir *cuán fuerte* se une. Ver [[Energía libre de unión]].

## Su lugar en las dos clases del módulo

- En [[Métodos para el diseño computacional de fármacos|la clase 6]] aparece como la respuesta a *"¿y si la estructura no está en el [[PDB]]?"*, junto a [[Modelado por homología]] y [[Threading]]; y como uno de los modelos de [[Cofolding|co-plegado]].
- En [[Modelos de lenguaje de proteínas y embeddings proteicos|la clase 9]] aparece como **punto de comparación** de [[ESMFold]], que predice estructura **sin [[Alineamiento múltiple de secuencias|MSA]]** y mucho más rápido, a costa de algo de precisión.

Sus predicciones masivas viven en [[AlphaFold DB]].

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
