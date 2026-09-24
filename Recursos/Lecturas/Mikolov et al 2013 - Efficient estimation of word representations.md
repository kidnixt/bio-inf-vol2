---
tags: [lectura, modulo-3, embeddings, NLP]
area: Lecturas
tipo: preprint (arXiv)
autores: Tomas Mikolov, Kai Chen, Greg Corrado, Jeffrey Dean
año: 2013
revista: arXiv:1301.3781 (ICLR 2013 workshop)
doi: 10.48550/arXiv.1301.3781
aliases: [Mikolov 2013, Mikolov et al. 2013, word2vec paper, "Efficient Estimation of Word Representations in Vector Space"]
---

# Mikolov et al. (2013) — *Efficient Estimation of Word Representations in Vector Space*

> [!info] Ficha de la lectura
> **Tipo:** preprint de arXiv (Google Inc., Mountain View)
> **Autores:** Mikolov, Chen, Corrado y Dean
> **Clase asociada:** [[Modelos de lenguaje de proteínas y embeddings proteicos]] (clase 9)
> **PDF:** [[Mikolov et al 2013 - Efficient estimation of word representations.pdf]]

## En una frase

El paper de **[[Word2vec]]**: dos arquitecturas baratas para aprender vectores de palabras a partir de corpus enormes, y la demostración de que las **relaciones semánticas emergen como direcciones** en ese espacio.

## Por qué leerla después de la clase

La clase lo presenta como *"el origen de todo"* y usa su Tabla 3 para justificar por qué la familia de proteínas se apoya en **Skip-gram**. Leerlo sirve para ver que el argumento del paper **no es sobre calidad sino sobre costo**: el título dice *efficient estimation*, no *better representations*.

---

## 1. El problema que ataca

> "Many current NLP systems treat words as **atomic units** — there is no notion of similarity between words, as these are represented as indices in a vocabulary."

Esa frase es exactamente el problema del [[One-hot encoding]] que la clase ilustra con las 5.000 comidas. El paper argumenta que los modelos simples sobre datos enormes ya no alcanzan para tareas donde los datos relevantes son limitados, y que hace falta una representación **distribuida**.

## 2. Las dos arquitecturas

| Modelo | Qué predice | Costo | Fuerte en |
|---|---|---|---|
| **CBOW** (*continuous bag-of-words*) | La palabra del medio, a partir del contexto | Más barato | **Sintaxis** (64 %) |
| **Skip-gram** | El contexto, a partir de la palabra | Más caro | **Semántica** (55 % vs. 24 %) |

La clave arquitectónica: **ninguna tiene capa oculta no lineal**. Esa simplificación es lo que hace posible entrenar sobre 1.600 millones de palabras en menos de un día, y es de donde sale la observación de la clase de que *"la matriz de pesos **es** la tabla: buscar una palabra es buscar su fila"*.

## 3. El resultado que quedó en la cultura

El test de analogías: `rey − hombre + mujer ≈ reina`. Lo notable no es el ejemplo sino la **generalización**: la dirección que separa un país de su capital sirve para los doce países probados, y el modelo **nunca vio la palabra "capital"**.

Es la base conceptual de todo lo que sigue: si una relación es una dirección en el espacio, entonces la **posición es el significado** — la idea que [[ProtVec]] traslada a proteínas y que los modelos contextuales ([[ELMo y SeqVec]], [[Transformer|transformers]]) después refinan.

> [!note] El matiz que la clase subraya bien
> **La tarea es un pretexto.** Predecir la palabra tapada es un problema ficticio; lo que se guarda son los pesos internos. Diez años después, [[Masked language modeling]] en [[ESM-1b y ESM-2|ESM]] hace exactamente lo mismo con aminoácidos.

## 4. Qué aporta respecto de la clase

- **La tabla de CBOW vs. Skip-gram con sus números** (24/64 contra 55/59), que en la clase aparece resumida — verla en contexto muestra que la diferencia es de *tipo de tarea*, no de calidad general.
- **El argumento de costo**: el paper compite contra redes neuronales previas (NNLM, RNNLM) en *accuracy por hora de cómputo*, no en accuracy absoluta. Esa lógica —modelo más simple, más datos— es la que después habilita escalar PLMs.
- **La limitación que hereda toda la familia de embeddings estáticos**: una palabra, un vector, siempre el mismo. El paper ni la plantea como problema; hizo falta [[ELMo y SeqVec|ELMo]] para nombrarla.

## Conceptos del vault

[[Word2vec]] · [[Embedding]] · [[One-hot encoding]] · [[Modelo de lenguaje de proteínas]] · [[ProtVec]] · [[Transformer]]

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
- [[Módulo 3 - MOC]]
