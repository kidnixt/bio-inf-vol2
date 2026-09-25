---
tags: [concepto, bioinformática, IA, embeddings]
area: Bioinformática
aliases: [embeddings, representación vectorial, vector denso, espacio de embeddings, mean pooling]
---

# Embedding

La traducción literal sería *"incrustación"*: el concepto se **incrusta** en un espacio de muchas dimensiones. Pero se usa **"representación vectorial"**, que describe mejor lo que hace: **representar algo con una lista de números**.

## De dónde viene: el problema del one-hot

Un modelo solo manipula números, así que cada ítem necesita su lugar. El [[One-hot encoding|one-hot]] le da uno: un vector con un 1 en la posición propia y 0 en todas las demás.

> **El problema:** todos los 1s están **a la misma distancia**. En el ejemplo de la clase (una app con 5.000 comidas), *borscht* y *shawarma* quedan igual de lejanos que *borscht* y *pizza*. Y son vectores de 5.000 números casi todos 0s: **enormes y vacíos**.

El embedding es lo que viene después: **comprime eso y aprende qué se parece a qué**.

## Cómo se obtiene

Con una tarea inventada —tapar un ítem y adivinarlo por su contexto—, repetida millones de veces. El error es la señal: las conexiones que llevaron al error se debilitan, las que acercaban a la respuesta se refuerzan.

> **El salto:** one-hot solo sabe **contar**. El embedding sale de millones de intentos: cada ítem termina con una **posición**, y quedar cerca o lejos **significa algo**.

## Las dimensiones son rasgos que nadie diseña

Con **un eje** (la *"sandwicheidad"* del ejemplo), los ítems se ordenan en una línea. Con **dos** (+ *"postreidad"*), el mapa se vuelve un plano:

- **Cada eje captura un rasgo**, no una categoría cerrada.
- **La posición es el significado**: la distancia ya es información.
- **Nadie diseña los ejes.** En un embedding real hay cientos o miles, y **las descubre el modelo**.

> Una dimensión ordena en una línea; dos arman un mapa; **N** dimensiones permiten comparar parecidos que ningún eje solo podría describir.

## Las relaciones son direcciones

En un espacio de embeddings, **una relación es una dirección**: `rey → reina` es el mismo vector que `hombre → mujer`; `Chile → Santiago` el mismo que otros once países con su capital. El modelo **nunca vio la palabra "capital"**: aprendió la dirección, y la dirección generaliza. Ver [[Word2vec]].

## Embeddings de proteínas

En un [[Modelo de lenguaje de proteínas|PLM]], la salida es **un vector por residuo** (1280 números en ESM-2). De ahí hay dos formas de usarla:

| Forma | Para qué |
|---|---|
| **Por residuo** | Predecir posición por posición: estructura secundaria, accesibilidad al solvente, sitios activos |
| **Promedio** (*mean pooling*, media por fila) | Clasificar la proteína entera: localización subcelular, familia, función |

Y una distinción que organiza toda la clase 9: los embeddings **estáticos** ([[Word2vec]], [[ProtVec]]) asignan siempre el mismo vector al mismo símbolo; los **contextuales** ([[ELMo y SeqVec|SeqVec]], [[Transformer|transformers]]) lo **reescriben según el entorno**.

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
- [[Asgari and Mofrad 2015 - Continuous distributed representation of biological sequences]] *(lectura)*
- [[Bouras et al 2026 - Phold]] *(lectura)*
- [[Elnaggar et al 2021 - ProtTrans]] *(lectura)*
- [[Elnaggar et al 2023 - Ankh]] *(lectura)*
- [[Hayes et al 2025 - Simulating 500 million years of evolution]] *(lectura)*
- [[Heinzinger et al 2019 - SeqVec]] *(lectura)*
- [[Heinzinger et al 2024 - ProstT5]] *(lectura)*
- [[Mikolov et al 2013 - Efficient estimation of word representations]] *(lectura)*
- [[Rives et al 2021 - Biological structure and function emerge from scaling]] *(lectura)*
