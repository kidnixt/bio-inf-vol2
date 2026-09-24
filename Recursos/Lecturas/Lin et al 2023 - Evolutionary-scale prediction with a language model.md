---
tags: [lectura, modulo-3, PLM, estructura]
area: Lecturas
tipo: research article
autores: Zeming Lin, Halil Akin, Roshan Rao, Brian Hie, Zhongkai Zhu, Wenting Lu, Nikita Smetanin, Robert Verkuil, Ori Kabeli, Yaniv Shmueli, Allan dos Santos Costa, Maryam Fazel-Zarandi, Tom Sercu, Salvatore Candido, Alexander Rives
año: 2023
revista: Science 379(6637), 1123–1130
doi: 10.1126/science.ade2574
aliases: [Lin 2023, ESM-2 paper, ESMFold paper, "Evolutionary-scale prediction of atomic-level protein structure with a language model"]
---

# Lin et al. (2023) — *Evolutionary-scale prediction of atomic-level protein structure with a language model*

> [!info] Ficha de la lectura
> **Tipo:** research article — *Science*
> **Autores:** Meta AI (Fundamental AI Research, Protein Team)
> **Clase asociada:** [[Modelos de lenguaje de proteínas y embeddings proteicos]] (clase 9)
> **PDF:** [[Lin et al 2023 - Evolutionary-scale prediction with a language model.pdf]]

## En una frase

El paper de **[[ESM-1b y ESM-2|ESM-2]]** y **[[ESMFold]]**: escalar el modelo de lenguaje hasta 15.000 millones de parámetros hace emerger una imagen de la estructura a **resolución atómica**, y eso permite predecir estructura **sin [[Alineamiento múltiple de secuencias|MSA]]**, un orden de magnitud más rápido.

## Por qué leerla después de la clase

La clase muestra la arquitectura (ESM-2 → *Folding Trunk* → *Structure Module*, con *recycling*), la tabla contra AlphaFold 2 y las figuras de comparación. El paper aporta **por qué** la velocidad importa: es la condición de posibilidad del [[ESM Atlas]].

---

## 1. El resultado central

> "A medida que los modelos de lenguaje de proteínas se escalan hasta 15 mil millones de parámetros, **emerge en las representaciones aprendidas una imagen de la estructura proteica a resolución atómica**."

Dos números que la clase reporta y que vale la pena tener a mano:

| Métrica | ESM-2 8M → 15B |
|---|---|
| Perplejidad | **10,45 → 6,37** (el azar sería ~20) |
| Precisión de contactos | mejora en **todos** los tramos |

## 2. De dónde sale la aceleración

El costo dominante de [[AlphaFold]] 2 y RoseTTAFold no es la red: es **construir el MSA**. El paper lo dice explícitamente — las *pipelines* de alta sensibilidad son una parte significativa del costo incluso con las versiones rápidas y de menor sensibilidad. Al eliminar ese paso, la aceleración es de **uno a dos órdenes de magnitud**.

En números concretos: **14,2 s** para 384 residuos en una V100.

| | AlphaFold 2 | ESMFold |
|---|---|---|
| ¿Necesita MSA? | Sí | **No** |
| Velocidad | Lento | **Muy rápido** |
| De dónde sale la señal | De los homólogos | Del **PLM** |

## 3. Lo que habilita: el ESM Metagenomic Atlas

Con esa velocidad se predijeron estructuras para **más de 617 millones** de secuencias metagenómicas, de las cuales **más de 225 millones** con alta confianza. Ver [[ESM Atlas]].

El argumento que el paper hace y la clase recoge: la última década expandió el conocimiento de secuencias hacia la inmensa diversidad microbiana de la Tierra vía metagenómica, y las bases crecieron exponencialmente. **Caracterizar eso estructuralmente solo era posible si predecir era barato.**

## 4. Qué aporta respecto de la clase

- **El *recycling* explicado**: el resultado se vuelve a pasar por la red, refinándose sobre su propio borrador. La clase lo menciona en una línea.
- **El caso de la proteína metagenómica** que ESMFold acierta y que "no se parecía a nada conocido" — el escenario donde un MSA **no tendría de dónde sacar señal**, y por lo tanto donde la ventaja del PLM no es de velocidad sino de **cobertura**. Es el mismo argumento de [[Heinzinger et al 2019 - SeqVec|SeqVec]] sobre el *Dark Proteome*, cuatro años después y con evidencia.
- **El costo del atlas**: 2 semanas en ~2.000 GPUs. Útil para la discusión final de la clase sobre usar vs. entrenar.

## Conceptos del vault

[[ESMFold]] · [[ESM-1b y ESM-2]] · [[ESM Atlas]] · [[AlphaFold]] · [[Alineamiento múltiple de secuencias]] · [[Modelo de lenguaje de proteínas]] · [[Transformer]] · [[Homología remota]]

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
- [[Módulo 3 - MOC]]
