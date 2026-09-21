---
tags: [herramienta, base-de-datos, modelado]
area: Herramientas
aliases: [BiGG, bigg models, Memote]
---

# BiGG Models

Repositorio público de [[Modelo metabólico a escala genómica|modelos metabólicos a escala genómica]] curados, con identificadores estandarizados de metabolitos y reacciones (los *BiGG ids*).

`http://bigg.ucsd.edu`

## Qué ofrece por modelo

El ejemplo de la clase, **iML1515**:

| Campo | Valor |
|---|---|
| Organismo | *[[Escherichia coli]]* str. K-12 substr. MG1655 |
| Genoma | NC_000913.3 |
| Metabolitos | 1877 |
| Reacciones | 2712 |
| Genes | 1516 |
| Descarga ("COBRA model") | [[SBML]] `.xml` · JSON `.json` · MAT `.mat` |

La interfaz también incluye **Advanced Search**, **Data Access** y un enlace al **Memote Validator**, una herramienta externa que puntúa la calidad y completitud de un modelo metabólico.

## Por qué importa el "id estandarizado"

Que dos modelos distintos llamen igual al mismo metabolito es lo que permite comparar modelos, transferir reacciones de uno a otro y armar listas de candidatos [[Knock-out y knock-in|KI]] reutilizables. En [[PECA]], uno de los modelos precargados se llama `yeast9_anaerobic_biggids.xml` justamente porque está traducido a identificadores BiGG.

Responde la pregunta *"¿dónde están los modelos?"* de la clase, junto a [[ModelSEED y KBase]] (que los **construyen**) y [[KEGG]] / [[MetaCyc]] (que aportan el conocimiento bioquímico de base).

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
