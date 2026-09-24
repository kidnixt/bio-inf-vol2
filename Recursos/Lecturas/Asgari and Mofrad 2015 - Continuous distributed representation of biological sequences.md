---
tags: [lectura, modulo-3, embeddings, PLM]
area: Lecturas
tipo: research article
autores: Ehsaneddin Asgari, Mohammad R. K. Mofrad
año: 2015
revista: PLoS ONE 10(11), e0141287
doi: 10.1371/journal.pone.0141287
aliases: [Asgari 2015, Asgari and Mofrad 2015, ProtVec paper, BioVec, GeneVec, "Continuous Distributed Representation of Biological Sequences for Deep Proteomics and Genomics"]
---

# Asgari & Mofrad (2015) — *Continuous Distributed Representation of Biological Sequences for Deep Proteomics and Genomics*

> [!info] Ficha de la lectura
> **Tipo:** research article — *PLoS ONE* (acceso abierto)
> **Autores:** Asgari y Mofrad (Molecular Cell Biomechanics Lab, UC Berkeley y Lawrence Berkeley National Lab)
> **Clase asociada:** [[Modelos de lenguaje de proteínas y embeddings proteicos]] (clase 9)
> **PDF:** [[Asgari and Mofrad 2015 - Continuous distributed representation of biological sequences.pdf]]

## En una frase

El paper de **[[ProtVec]]**: la primera traducción de [[Word2vec]] a secuencias biológicas — partir la proteína en [[K-mer|3-meros]], aprender un vector por 3-mero, y representar la proteína entera como la suma de esos vectores.

## Por qué leerla después de la clase

En la clase, ProtVec aparece casi solo por sus **límites** (vector fijo, ventana de 3 residuos demasiado corta). El paper muestra el otro lado: por qué en 2015 era un resultado fuerte, y sobre todo **qué aprendió el modelo sin que nadie se lo dijera** — que es el mismo fenómeno que [[ESM-1b y ESM-2|ESM-1b]] va a reportar seis años después a otra escala.

---

## 1. El método

- La secuencia se parte en **3-meros** en **tres marcos superpuestos** (empezando en la posición 1, 2 y 3), así que cada proteína genera tres listas de "palabras".
- Se entrena Skip-gram sobre el corpus de Swiss-Prot → un vector de **100 dimensiones por 3-mero** (9.048 3-meros posibles).
- La proteína se representa como la **suma** de los vectores de sus 3-meros: una *bolsa de palabras*.

El nombre general es **BioVec**, con **ProtVec** para proteínas y **GeneVec** para secuencias de genes. Ese detalle importa acá: la idea nació ya pensada para **ADN además de proteínas**, que es justamente el puente hacia los modelos de lenguaje genómicos de la clase 10.

## 2. Resultados

| Tarea | Resultado |
|---|---|
| Clasificación de familias proteicas | **93 % ± 0,06** sobre 324.018 secuencias de Swiss-Prot en 7.027 familias |
| Proteínas desordenadas vs. estructuradas | ~**100 %** de exactitud (DisProt y regiones FG-Nup de nucleoporinas) |

## 3. El hallazgo que anticipa todo lo que viene

Proyectando los 3-meros con [[t-SNE]], los autores muestran que **los 3-meros se agrupan por masa, volumen, polaridad, hidrofobicidad, carga y volumen de van der Waals** — propiedades biofísicas que **nunca estuvieron en el entrenamiento**, que solo vio secuencias.

Es la misma clase de resultado que:

- [[ELMo y SeqVec|SeqVec]] (2019): los embeddings **sin entrenar** ya agrupan proteínas por localización celular.
- [[ESM-1b y ESM-2|ESM-1b]] (2021): el [[Mapa de contactos]] se recupera de las representaciones sin haber visto un solo contacto.

Dicho de otro modo: **la estructura emerge** no es un hallazgo de 2021, es una progresión que arranca acá — lo que cambia es *cuánta* estructura y a qué profundidad.

## 4. Qué aporta respecto de la clase

- **El número de la clasificación de familias (93 %)**, que la clase no menciona y que explica por qué el método se tomó en serio.
- **La parte "GeneVec"**: la misma receta sobre ADN. Útil como antecedente directo de la clase 10.
- **Una lectura más justa de sus límites.** La clase dice "no hay contexto" y es cierto, pero el paper ya proponía los embeddings como **pre-entrenamiento reutilizable** ("trained once and then used to encode biological sequences in any given problem"). Esa es la idea de *transfer learning* que [[ProtT5 y ProtBERT|ProtTrans]] y el caso de tesis de Puglia explotan después: [[Embedding|embeddings]] congelados + un clasificador simple.

## Conceptos del vault

[[ProtVec]] · [[Word2vec]] · [[Embedding]] · [[K-mer]] · [[t-SNE]] · [[Modelo de lenguaje de proteínas]] · [[UniProt]]

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
- [[Módulo 3 - MOC]]
