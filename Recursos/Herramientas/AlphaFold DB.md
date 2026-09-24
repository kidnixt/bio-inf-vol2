---
tags: [herramienta, base-de-datos, estructura, IA]
area: Herramientas
aliases: [AlphaFold Protein Structure Database, AlphaFoldDB, AFDB]
---

# AlphaFold DB

Base de **estructuras predichas** por [[AlphaFold]], mantenida por **EMBL-EBI** y **Google DeepMind**.

| | |
|---|---|
| Tipo de registro | Modelos estructurales indexados (monómeros y complejos) |
| Tamaño (corte 09/09/2026) | **261.247.178** |
| Qué ofrece | Modelos de monómeros y complejos, secuencias y **métricas de confianza** |
| Consulta típica | *¿Qué modelo estructural existe y qué regiones tienen mayor confianza?* |

## Lo que cambió

Antes de AlphaFold DB, tener estructura de un blanco era un privilegio: ~2,6·10⁵ estructuras experimentales en el [[PDB]] para ~1,5·10⁸ secuencias en [[UniProt]]. Después, **hay un modelo para casi cualquier proteína conocida** — tres órdenes de magnitud más que el PDB.

Eso desplazó la pregunta: ya no es *"¿existe una estructura?"* sino ***"¿cuánto le creo a esta región de este modelo?"***. De ahí que las métricas de confianza (pLDDT por residuo, PAE entre regiones) sean parte del registro y no un extra.

> [!warning] La advertencia de la clase
> **El índice y las descargas masivas tienen coberturas distintas**, y **la confianza depende del modelo**. Un modelo con pLDDT bajo en el sitio de unión no sirve para [[Docking molecular|docking]] aunque el resto de la proteína esté perfecta.

Junto con el [[ESM Atlas]] (617 M de estructuras metagenómicas) forma el universo de **cientos de millones de estructuras predichas** que hizo necesario a [[Foldseek]]: con tantos modelos, el cuello de botella pasó a ser **compararlos**.

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
