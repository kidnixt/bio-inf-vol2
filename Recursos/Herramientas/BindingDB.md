---
tags: [herramienta, base-de-datos, bioactividad]
area: Herramientas
aliases: [Binding DB]
---

# BindingDB

Base de datos de **afinidades proteína–ligando medidas**, de la Universidad de California en San Diego (equipo de **Michael Gilson**).

| | |
|---|---|
| Tipo de registro | Compuestos con datos de unión |
| Tamaño (corte) | **1.440.011** (descarga 202609, actualizada 30/08/2026) |
| Qué ofrece | Afinidades medidas, estructuras químicas, proteínas, condiciones experimentales y referencias |
| Consulta típica | *¿Qué afinidades se han medido para esta familia de ligandos?* |

## Su rol

Es la fuente para modelos de **afinidad** y **selectividad**: a diferencia de [[ChEMBL]] —que cubre bioactividad en sentido amplio, incluyendo ensayos celulares y fenotípicos—, BindingDB se concentra en la **unión** medida entre una proteína y un ligando, con las condiciones del experimento.

Comparte datos con [[ChEMBL]], así que hay que tener cuidado al combinarlas para no inflar artificialmente un conjunto de entrenamiento con los mismos registros dos veces.

Cuando además hace falta la **estructura 3D del complejo** asociada a la medida, la base es [[PDBbind]] — que es dos órdenes de magnitud más chica.

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
