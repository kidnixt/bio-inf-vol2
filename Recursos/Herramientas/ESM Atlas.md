---
tags: [herramienta, base-de-datos, estructura, metagenómica]
area: Herramientas
aliases: [ESM Metagenomic Atlas, esmatlas, materia oscura de las proteínas, lado oscuro de las proteínas]
---

# ESM Atlas

El **ESM Metagenomic Atlas** (Meta AI, 2022): la predicción masiva de estructuras de proteínas metagenómicas con [[ESMFold]]. `esmatlas.com`

| | |
|---|---|
| Estructuras | **más de 600 millones** |
| Tamaño relativo | **3×** la mayor base anterior |
| Cómputo | 2 semanas en un clúster de ~2.000 GPUs |
| Con alta confianza | solo el **~10 %** — el resto es exploración |

## El "lado oscuro"

Son proteínas de microbios **del suelo, del océano y de nuestro cuerpo**. No se parecen a nada conocido, así que no había forma de estudiarlas: sin homólogos no hay [[Alineamiento múltiple de secuencias|MSA]], sin MSA no había estructura, y sin estructura no había hipótesis de función. Ahora **cada una tiene una estructura**.

> **El cambio de método:** la escala no es solo "más datos". Cambia **cómo se investiga** — antes se elegía *una* proteína interesante y se le dedicaba un doctorado; ahora se predice el catálogo entero y **después** se busca qué mirar.

Es el mismo desplazamiento que produjo la [[Metagenómica clínica|metagenómica]] del lado de las secuencias, llevado a las estructuras.

## Consecuencia directa

Con [[AlphaFold DB]] (214 M de modelos) y el ESM Atlas (617 M) juntos, el problema dejó de ser *tener* estructuras y pasó a ser **compararlas**. Eso es lo que resuelve [[Foldseek]] con el [[Alfabeto 3Di|alfabeto 3Di]], y lo que [[ProstT5]] después aprende a predecir directamente de la secuencia.

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
- [[Heinzinger et al 2019 - SeqVec]] *(lectura)*
- [[Lin et al 2023 - Evolutionary-scale prediction with a language model]] *(lectura)*
- [[van Kempen et al 2024 - Foldseek]] *(lectura)*
