---
tags: [herramienta, modelo, NLP, embeddings]
area: Herramientas
aliases: [word2vec, CBOW, Skip-gram, skipgram]
---

# Word2vec

El modelo que inventó los [[Embedding|embeddings]] modernos de palabras (**Mikolov et al., 2013, Google**, arXiv:1301.3781). No es un modelo de proteínas, pero es el origen de toda la familia: [[ProtVec]], [[ELMo y SeqVec|SeqVec]] y [[ProtT5 y ProtBERT|ProtT5]] resuelven variantes del mismo truco.

## El truco

> **Era un truco, no un objetivo.** Nadie quería predecir palabras: es un **problema ficticio**, inventado como excusa para obligar a la red a aprender algo útil en el camino.

1. **La tarea inventada** — tapar una palabra y adivinarla por las que la rodean.
2. **Lo que aprende** — para acertar, la red tiene que descubrir qué palabras van juntas.
3. **El premio real** — se descarta la salida y **se guardan los pesos internos**: eso es el embedding.

Esta lógica —tarea artificial, premio en las representaciones— es exactamente la del [[Masked language modeling|masked language modeling]] que usan [[ESM-1b y ESM-2|ESM]] y [[ProtT5 y ProtBERT|ProtBERT]] una década después.

## Dos arquitecturas

| Modelo | Cómo | Significado | Forma |
|---|---|---|---|
| **CBOW** | Tapa el medio, adivina por el contexto. Rápido | 24 % | **64 %** |
| **Skip-gram** | Con una palabra, adivina qué la rodea. Más lento | **55 %** | 59 % |

*(acierto en el test de relaciones, Mikolov et al. 2013, Tabla 3)*

**Skip-gram más que duplica a CBOW en significado**, y por eso es el que hereda la familia de proteínas: en una proteína importa el significado, no la forma superficial.

## Los dos hallazgos

- **La escala:** 6.000 millones de palabras, vocabulario de 1 millón, entrenado en **menos de un día**. La red **no tiene capa oculta** — la matriz de pesos *es* la tabla de embeddings, y buscar una palabra es buscar su fila. Esa simpleza es lo que permitió la escala.
- **La aritmética del significado:** las relaciones **emergen** del entrenamiento sin que nadie las etiquete, y se generalizan a pares que el modelo nunca vio juntos. `rey → reina` es la misma dirección que `hombre → mujer`; `Chile → Santiago` la misma que doce países con sus capitales.

Y la compresión: de **50.000** posiciones casi todas en cero a **100–300** números con valor. 167 veces menos números, y ahora con información.

> **Su límite** —el que hereda [[ProtVec]]— es que los vectores son **fijos**: la misma palabra ocupa siempre el mismo lugar, aparezca donde aparezca. Ver [[Embedding]] y [[Transformer]].

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
