---
tags: [concepto, bioinformática, estructura, simulación]
area: Bioinformática
aliases: [docking, acoplamiento molecular, pose, poses, Glide]
---

# Docking molecular

El método central del [[Diseño basado en estructura|SBDD]]: predecir **cómo se acomoda** un ligando dentro del sitio de unión de una proteína.

## Es un problema de búsqueda

Se plantea en dos mitades:

| Generar poses | Ordenar poses |
|---|---|
| Explorar **traslación**, **rotación** y **torsiones** del ligando | **Agrupamiento** (*clustering*) y **clasificación** con una [[Función de puntuación\|función de puntuación]] |

El espacio de búsqueda crece con los grados de libertad: cada enlace rotable del ligando multiplica las conformaciones posibles, y si además se permite que el receptor se mueva, crece mucho más.

## Flexibilidad del receptor

| Tratamiento | Costo | Qué representa |
|---|---|---|
| **Rígido** | Rápido | Un estado |
| ***Side chains*** | Intermedio | Ajuste local |
| ***Ensemble*** | Mayor costo | Estados discretos |
| ***Induced fit*** | Costoso | Cambio acoplado |

> **Más flexibilidad aumenta la precisión y el espacio de búsqueda.** Es el compromiso permanente del docking.

## Qué devuelve, y qué no

El resultado es **una pose + una puntuación**, es decir **una configuración**. No dice cómo evoluciona en el tiempo (eso es [[Dinámica molecular|MD]]) ni cuál es la afinidad real (eso es [[Energía libre de unión]]).

> [!warning] El score no es ΔG
> La puntuación sirve como **ranking dentro del protocolo**. No equivale automáticamente a la ΔG experimental.

## La versión con IA

La clase lista la familia de modelos que aprendieron a predecir o generar poses: **DiffDock** (difusión), **KarmaDock** y **CarsiDock** (GNN + MDN, transformers), **Uni-Mol**, **EquiBind**, **E3Bind**, **SurfDock**, **NeuralPLexer**, **[[AlphaFold|AlphaFold3]]** y **RoseTTAFold All-Atom** — casi todos entrenados sobre [[PDBbind]] y evaluados sobre PoseBusters, CASF-2016 o DEKOIS. Y el paso siguiente, [[Cofolding|co-plegar]] proteína y ligando de una sola vez.

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
