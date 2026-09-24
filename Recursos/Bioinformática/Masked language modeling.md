---
tags: [concepto, bioinformática, IA, deep-learning]
area: Bioinformática
aliases: [masked, MLM, enmascarado, máscara, autorregresivo, bidireccional, modelado de lenguaje enmascarado]
---

# Masked language modeling

La tarea de entrenamiento que usan casi todos los [[Modelo de lenguaje de proteínas|PLMs]]: **tapar un símbolo y predecirlo** a partir de todo el resto.

Es una de las tres formas de leer una secuencia, y cuál se elija **define para qué sirve el modelo**.

## Las tres arquitecturas

La misma secuencia `MLVAGRR`, tres maneras de procesarla. Cambia **qué puede ver cada residuo**:

| | Cómo lee | Para qué sirve | Modelos |
|---|---|---|---|
| **A · Autorregresiva** | Una sola dirección: p(xₜ \| x₁…xₜ₋₁). Solo mira lo anterior | **Generar** — inventar secuencias nuevas | ProtGPT2, ProGen |
| **B · Bidireccional** | Dos pasadas *independientes* que después se concatenan. Ve izquierda y derecha, pero en **dos recorridos separados** | **Etiquetar cada residuo** — estructura secundaria, accesibilidad al solvente, sitios activos | [[ELMo y SeqVec\|ELMo, SeqVec]] |
| **C · Masked** | Toda la secuencia a la vez; se tapa un residuo y se predice. Cada posición ve **todo el resto en una sola pasada** | **Representar** — [[Embedding\|embeddings]] de alta calidad para clasificar | BERT, [[ESM-1b y ESM-2\|ESM]], [[ProtT5 y ProtBERT\|ProtBERT]] |

> ¿Querés **entender** una proteína que ya existe? → **C** (o **B** si te importa cada residuo). ¿Querés **inventar** una nueva? → **A**.

## Por qué funciona como pretexto

Igual que en [[Word2vec]], **la predicción se descarta y los vectores se quedan**. Predecir el residuo tapado es un **problema ficticio**: a nadie le interesa la respuesta. Lo que importa es que, para acertar, el modelo **tiene que** descubrir qué residuos se condicionan mutuamente — y eso es, de hecho, la estructura y la función.

Por eso el entrenamiento tapa **un sector distinto en cada paso**: así el modelo se ve obligado a aprender todas las dependencias, no solo las locales. Las últimas capas ocultas terminan **reescribiendo el vector de cada aminoácido según toda la secuencia**: entra un símbolo, sale un **vector situado**.

[[ESM3]] lleva la idea al extremo: enmascara las tres modalidades (secuencia, estructura y función) y rellena posición por posición — lo que convierte el mismo mecanismo en una herramienta **generativa**.

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
