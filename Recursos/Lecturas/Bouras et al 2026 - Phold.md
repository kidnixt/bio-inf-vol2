---
tags: [lectura, modulo-3, anotación, virus, estructura]
area: Lecturas
tipo: data resources and analyses
autores: George Bouras, Susanna R. Grigson, Milot Mirdita, Michael Heinzinger, Bhavya Papudeshi, Vijini Mallawaarachchi, Renee Green, Rachel Seongeun Kim, Victor Mihalia, Alkis James Psaltis, Peter-John Wormald, Sarah Vreugde, Martin Steinegger, Robert A. Edwards
año: 2026
revista: Nucleic Acids Research 54, gkaf1448
doi: 10.1093/nar/gkaf1448
aliases: [Bouras 2026, Phold paper, "Protein structure-informed bacteriophage genome annotation with Phold"]
---

# Bouras et al. (2026) — *Protein structure-informed bacteriophage genome annotation with Phold*

> [!info] Ficha de la lectura
> **Tipo:** *Data Resources and Analyses* — *Nucleic Acids Research* (acceso abierto)
> **Autores:** Universidad de Adelaida y Flinders University (Australia), Seoul National University y TUM — con **Heinzinger** ([[Heinzinger et al 2024 - ProstT5|ProstT5]]), **Mirdita** y **Steinegger** ([[van Kempen et al 2024 - Foldseek|Foldseek]]) entre los autores
> **Clase asociada:** [[Modelos de lenguaje de proteínas y embeddings proteicos]] (clase 9)
> **PDF:** [[Bouras et al 2026 - Phold.pdf]]
> **Código:** `github.com/gbouras13/phold`

## En una frase

El paper de **[[Phold]]**: combinar [[ProstT5]] (secuencia → [[Alfabeto 3Di|3Di]]) y [[Foldseek]] (buscar por forma) para anotar genomas de [[Bacteriófago|bacteriófagos]], superando a los métodos basados en homología de secuencia **sin perder velocidad ni interpretabilidad**.

## Por qué leerla después de la clase

Es el cierre práctico del arco de la clase: las dos piezas de las diapositivas anteriores, puestas a resolver un problema real. La clase da los números principales; el paper agrega **por qué el problema es tan difícil** y un hallazgo biológico que la diapositiva no llega a contar.

---

## 1. El problema

Los fagos son **las entidades biológicas más prevalentes de la Tierra**, y su anotación genómica sigue siendo extremadamente difícil:

- El crecimiento de datos metagenómicos descubre fagos nuevos **con poca o ninguna similitud de secuencia** con los conocidos.
- El resurgimiento de la **terapia con fagos** —usarlos contra patógenos, en particular resistentes a antimicrobianos— hace que entender su potencial funcional deje de ser una curiosidad. Conecta con [[Resistencia antimicrobiana]] del [[Módulo 1 - MOC|Módulo 1]].

## 2. El método

1. **ProstT5** genera [[Embedding|embeddings]] de 1024 dimensiones por residuo (encoder de 1000 M de parámetros).
2. Una **CNN de dos capas** predice el token 3Di de cada residuo.
3. **Foldseek** busca esa "secuencia de forma" contra una base curada de **más de 1,36 millones** de estructuras predichas, mayormente de fagos, con etiquetas funcionales de alta calidad.

> [!note] Una objeción que el paper se anticipa
> El inconveniente de los métodos basados en PLM para anotar es la **falta de interpretabilidad** frente a los métodos de secuencia, que devuelven alineamientos y E-values. Phold mantiene esa interpretabilidad porque el paso final **sigue siendo un alineamiento** — de 3Di, pero alineamiento al fin.

## 3. Los resultados

Sobre 16.460 CDS de fagos:

| Método | % anotado |
|---|---|
| MMseqs2 (secuencia) | 34,7 % |
| PyHMMER (perfil HMM) | 37,7 % |
| **Phold** (estructura) | **49,4 %** |
| Phold con estructuras de ColabFold | 51,5 % |

Aplicado a genomas diversos, cultivados y metagenómicos, anota consistentemente **más del 50 %** de los genes de un fago promedio y **40 %** de un virus de arquea promedio.

## 4. El hallazgo biológico

Comparando las estructuras de proteínas de fagos contra estructuras de todo el árbol de la vida, resulta que **las proteínas de fagos tienen homología estructural con proteínas compartidas a lo largo del árbol**, en particular las de **metabolismo de ácidos nucleicos y funciones enzimáticas**.

Eso explica el resultado anterior y le da sentido: la forma conserva señal que la secuencia ya perdió **porque esos dominios son antiguos y compartidos**, aunque sus secuencias hayan divergido más allá de lo detectable. Ver [[Homología remota]].

## 5. Qué aporta respecto de la clase

- **El "por qué" del resultado**, no solo el número: qué clase de proteínas gana anotación y por qué.
- **La dimensión aplicada**: terapia fágica y resistencia antimicrobiana. Es el punto donde el arco de la clase toca un problema clínico.
- **La confirmación del patrón** que atraviesa todo el módulo: *[[Embedding|embeddings]] congelados + un modelo chico encima* (acá, una CNN de dos capas) resuelve un problema real. Mismo patrón que la sonda de contactos de [[Rives et al 2021 - Biological structure and function emerge from scaling|ESM-1b]] y que el trabajo de tesis de Juan Diego Puglia.

## Conceptos del vault

[[Phold]] · [[ProstT5]] · [[Foldseek]] · [[Alfabeto 3Di]] · [[Bacteriófago]] · [[Homología remota]] · [[Embedding]] · [[Alineamiento múltiple de secuencias]] · [[Resistencia antimicrobiana]] · [[Deep Learning]]

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
- [[Módulo 3 - MOC]]
