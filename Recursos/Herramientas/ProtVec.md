---
tags: [herramienta, modelo, PLM, embeddings]
area: Herramientas
aliases: [Prot2Vec]
---

# ProtVec

La **primera traducción** de la idea de [[Word2vec]] a proteínas (Asgari & Mofrad, 2015, *PLoS ONE* 10(11):e0141287). Es el punto de partida de la familia de [[Modelo de lenguaje de proteínas|modelos de lenguaje de proteínas]].

## Cómo funciona

- Parte la secuencia en **[[K-mer|3-meros]]**: `MKV`, `KVL`, `VLA`… en **tres marcos superpuestos**.
- Cada 3-mero es una **"palabra"**.
- Aprende **un vector por palabra**, con el mismo truco de word2vec.

La secuencia se vuelve una **bolsa de palabras**: la misma jugada que en lenguaje natural, contar vecinos frecuentes.

## Sus dos límites

> [!warning] Por qué no alcanza
> 1. **El vector de `MKV` es siempre el mismo**, aparezca donde aparezca. **No hay contexto** — y el contexto es justamente lo que distingue una [[Homología|divergencia homóloga]] de una mutación puntual destructiva.
> 2. **Una ventana de 3 residuos es demasiado corta para ver estructura.** La **estructura terciaria** conecta posiciones separadas por decenas o cientos de residuos; un 3-mero no puede verla.

Todo lo que viene después en la clase es responder a esos dos límites: [[ELMo y SeqVec|SeqVec]] agrega contexto local y lee la secuencia completa; el [[Transformer]] conecta posiciones arbitrariamente lejanas en un solo paso.

En los benchmarks sirve como **línea de base**: en predicción de membrana, ProtVec da 77,6 donde SeqVec da 92,3.

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
