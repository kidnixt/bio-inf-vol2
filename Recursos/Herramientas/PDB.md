---
tags: [herramienta, base-de-datos, estructura]
area: Herramientas
aliases: [Protein Data Bank, RCSB PDB, PDBe, PDBj, wwPDB]
---

# PDB

El **Protein Data Bank**: el archivo de estructuras macromoleculares **determinadas experimentalmente**. Lo mantiene el wwPDB, con portales en RCSB PDB (Rutgers y UC San Diego), PDBe (EMBL-EBI) y PDBj.

| | |
|---|---|
| Tipo de registro | Estructuras experimentales |
| Tamaño (corte 09/09/2026) | **259.747** |
| Qué ofrece | Coordenadas 3D, ligandos, método experimental y validación estructural |
| Consulta típica | *¿Hay estructuras experimentales del blanco con ligandos unidos?* |

## Su rol

Es la condición de posibilidad del [[Diseño basado en estructura|SBDD]]: sin estructura del blanco no hay [[Docking molecular|docking]]. Las estructuras llegan por [[Cristalografía de rayos X|cristalografía de rayos X]], **RMN** o **Cryo-EM**, y el método condiciona qué se puede hacer con ellas (resolución, presencia de aguas, estado conformacional).

> [!warning] La advertencia de la clase
> **Una entrada es *una* estructura. Una proteína puede aparecer en muchos complejos.** Contar entradas no es contar proteínas, y elegir *cuál* de las estructuras de un blanco usar (con qué ligando, en qué estado) es una decisión de modelado, no un trámite.

Cuando el blanco **no está** en el PDB, las alternativas son [[Modelado por homología]], [[Threading]] o [[AlphaFold]]. Y cuando además se necesita una **afinidad** asociada al complejo, la base es [[PDBbind]].

En el análisis bibliométrico de la clase es la base con la **historia más larga y estable**: menciones consistentes desde el año 2000, mientras las demás despegan recién después de 2015.

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
