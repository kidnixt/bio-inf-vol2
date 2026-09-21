---
tags: [concepto, bioinformática, formato]
area: Bioinformática
aliases: [Systems Biology Markup Language, COBRA JSON, formato SBML, formatos de modelos metabólicos]
---

# SBML

Formato estándar basado en XML para intercambiar modelos de biología de sistemas, incluidos los [[Modelo metabólico a escala genómica|modelos metabólicos a escala genómica]].

## Formatos que aparecen en la clase

| Formato | Extensión | Dónde aparece |
|---|---|---|
| **SBML** | `.xml` | Descarga de [[BiGG Models]]; carga de modelos propios en [[PECA]] |
| **JSON** (COBRA JSON) | `.json` | Descarga de BiGG; carga en PECA |
| **MAT** | `.mat` | Descarga de BiGG (formato de MATLAB, para el COBRA Toolbox) |

Los tres codifican lo mismo: metabolitos, reacciones con su estequiometría (la [[Matriz estequiométrica]]), límites de flujo, compartimentos y reglas gen-proteína-reacción. BiGG los ofrece bajo el rótulo *"Download COBRA model"*, porque son los formatos que leen las herramientas del ecosistema [[openCOBRA]].

## Por qué importa

Tener un formato estándar es lo que permite que un modelo construido con una herramienta ([[ModelSEED y KBase|KBase o ModelSEED]]) se analice con otra ([[openCOBRA]], [[StrainDesign]]) y se comparta en repositorios. En la interfaz de [[PECA]], los modelos precargados (`PECA_toy.xml`, `iMM904.xml`, `yeast9_anaerobic_biggids.xml`) son todos archivos SBML.

BiGG además enlaza a **Memote**, un validador de calidad de modelos en estos formatos.

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
