---
tags: [concepto, bioinformática, evolución]
area: Bioinformática
aliases: [MSA, multiple sequence alignment, información evolutiva, perfil de secuencia]
---

# Alineamiento múltiple de secuencias

Un **MSA** alinea muchas secuencias homólogas a la vez, columna por columna. De ahí sale la **información evolutiva**: qué posiciones están conservadas, cuáles varían y —sobre todo— **qué pares de posiciones covarían**.

Esa covariación es la señal clásica de contacto estructural: si dos residuos están en contacto en el espacio, una mutación en uno tiende a compensarse con una mutación en el otro. Métodos como CCMpred explotan justamente eso para predecir [[Mapa de contactos|mapas de contactos]].

Ver también [[Alineamiento de secuencias]] (el caso de dos secuencias).

## Por qué aparece tanto en la clase 9

Porque el MSA es **lo que los PLMs vinieron a reemplazar**. Es la afirmación central de toda la familia:

> **Sin alineamientos.** La información evolutiva que los métodos clásicos sacaban de un MSA, el modelo **la aprende de haber visto millones de secuencias**.

| Modelo | ¿Necesita MSA? |
|---|---|
| Métodos clásicos, [[Modelado por homología]] | Sí |
| [[AlphaFold]] 2 | **Sí** |
| [[ProtT5 y ProtBERT]], [[ESM-1b y ESM-2\|ESM]] | No |
| [[ESMFold]] | **No** |
| [[ProstT5]], [[Phold]] | No |

## Por qué importa prescindir de él

- **Velocidad:** construir un MSA por secuencia es el paso lento. Sin él, [[ESMFold]] tarda 14,2 s para 384 residuos — y eso es lo que hizo posible el [[ESM Atlas]].
- **Cobertura:** un MSA necesita **homólogos**. Para una proteína metagenómica sin parientes conocidos no hay de dónde sacar señal, y ahí los métodos basados en MSA simplemente no funcionan. El PLM, en cambio, aporta lo que aprendió del resto del universo de proteínas.

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
- [[Métodos para el diseño computacional de fármacos]]
