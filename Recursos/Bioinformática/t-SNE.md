---
tags: [concepto, bioinformática, single-cell, visualizacion]
area: Bioinformática
aliases: [tSNE, t-distributed stochastic neighbor embedding]
---

# t-SNE

*t-distributed Stochastic Neighbor Embedding*. Método de [[Reducción dimensional]] **no lineal** usado para **visualizar** datos de [[scRNA-seq]] en 2 o 3 dimensiones. Es el antecesor directo del [[UMAP]] en los gráficos de células.

## Qué preserva y qué no

- Preserva la **estructura local**: células parecidas quedan juntas y los grupos se ven como islas separadas.
- **No preserva la estructura global**: la **distancia entre clusters no significa nada**, ni tampoco el tamaño de cada isla.
- Es **estocástico**: dos corridas pueden dar dibujos distintos.

[[UMAP]] preserva mejor la estructura global y escala mejor a millones de células, y por eso lo fue reemplazando ([[Slovin et al 2021 - scRNA-seq analysis a step-by-step overview|Slovin et al. 2021]]).

## Dónde va en el pipeline

La figura de la clase lo deja claro: el [[Clustering]] se hace en el espacio de ~50 componentes del [[PCA]]; t-SNE/UMAP solo se usan en el **paso 6**, para mirar el resultado ("recapitula la organización del espacio de PCs").

> [!warning] Lo que no hay que hacer
> Clusterizar sobre el t-SNE, o interpretar la cercanía entre dos islas como parentesco biológico.

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
- [[Slovin et al 2021 - scRNA-seq analysis a step-by-step overview]] *(lectura)*
- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
- [[Asgari and Mofrad 2015 - Continuous distributed representation of biological sequences]] *(lectura)*
- [[Heinzinger et al 2019 - SeqVec]] *(lectura)*
