---
tags: [lectura, modulo-3, PLM, transformer]
area: Lecturas
tipo: research article
autores: Ahmed Elnaggar, Michael Heinzinger, Christian Dallago, Ghalia Rehawi, Yu Wang, Llion Jones, Tom Gibbs, Tamas Feher, Christoph Angerer, Martin Steinegger, Debsindhu Bhowmik, Burkhard Rost
año: 2021
revista: IEEE Transactions on Pattern Analysis and Machine Intelligence
doi: 10.1109/TPAMI.2021.3095381
aliases: [Elnaggar 2021, ProtTrans paper, ProtT5 paper, ProtBERT paper, "ProtTrans - Towards Cracking the Language of Life's Code Through Self-Supervised Learning"]
---

# Elnaggar et al. (2021) — *ProtTrans: Towards Cracking the Language of Life's Code Through Self-Supervised Learning*

> [!info] Ficha de la lectura
> **Tipo:** research article — *IEEE TPAMI*
> **Autores:** grupo de **Burkhard Rost** (TUM) con NVIDIA, Google y Oak Ridge National Lab
> **Clase asociada:** [[Modelos de lenguaje de proteínas y embeddings proteicos]] (clase 9)
> **PDF:** [[Elnaggar et al 2021 - ProtTrans.pdf]]
> **Modelos:** `huggingface.co/Rostlab`

## En una frase

El paper de **[[ProtT5 y ProtBERT]]**: seis arquitecturas de NLP entrenadas a escala de supercómputo sobre secuencias de proteínas, y el primer resultado donde un PLM **supera al estado del arte por residuo sin usar información evolutiva**.

## Por qué leerla después de la clase

La clase lo resume en dos líneas ("dos familias, dos objetivos" y "sin alineamientos"). El paper es donde ese "sin alineamientos" pasa de ser una aspiración a un resultado medido — y donde se ve **el costo computacional** que hizo falta para lograrlo.

---

## 1. La escala

- **Seis modelos:** dos autorregresivos (Transformer-XL, XLNet) y cuatro auto-encoder (BERT, Albert, Electra, **T5**).
- **Datos:** UniRef y BFD, hasta **393 mil millones de aminoácidos**.
- **Cómputo:** el supercomputador **Summit** con **5.616 GPUs**, más un TPU Pod de hasta 1024 núcleos.

Ese último dato es el que conviene retener junto con la conclusión de la clase sobre [[Elnaggar et al 2023 - Ankh|Ankh]]: **el mismo grupo** que hizo esto es el que dos años después argumenta que escalar así no era necesario.

## 2. Los resultados

| Nivel | Tarea | Resultado |
|---|---|---|
| Por residuo | Estructura secundaria (3 estados) | **Q3 = 81–87 %** |
| Por proteína | Localización subcelular (10 clases) | **Q10 = 81 %** |
| Por proteína | Membrana vs. soluble | **Q2 = 91 %** |

Y el resultado central: para las predicciones **por residuo**, transferir los embeddings de **ProtT5** superó por primera vez al estado del arte **sin información evolutiva**, evitando búsquedas costosas en bases de datos.

## 3. Lo que muestra sobre los embeddings

La reducción dimensional de los embeddings crudos —**sin ninguna etiqueta**— ya captura propiedades biofísicas de las secuencias. Es, otra vez, el mismo fenómeno que [[Asgari and Mofrad 2015 - Continuous distributed representation of biological sequences|ProtVec]] y [[Heinzinger et al 2019 - SeqVec|SeqVec]] habían mostrado, ahora con transformers.

La conclusión que da el título: los PLMs aprendieron **algo de la gramática** del lenguaje de la vida.

## 4. Qué aporta respecto de la clase

- **El detalle de los dos objetivos.** ProtBERT es *encoder* con objetivo [[Masked language modeling|masked]]; ProtT5 es *encoder-decoder* con objetivo de *denoising* (reconstruir tramos corruptos, no un token suelto). Esa diferencia importa después: [[ProstT5]] se construye **afinando ProtT5**, y hereda de él la capacidad de traducir entre dos alfabetos.
- **La comparación con las arquitecturas que no funcionaron.** Seis modelos entrenados, y los auto-encoder ganan. La clase solo muestra los dos ganadores.
- **El dato del hardware**, que convierte la discusión "usar vs. entrenar un PLM" de la última parte de la clase en algo concreto.

## Conceptos del vault

[[ProtT5 y ProtBERT]] · [[Transformer]] · [[Masked language modeling]] · [[Embedding]] · [[Modelo de lenguaje de proteínas]] · [[Alineamiento múltiple de secuencias]] · [[UniProt]] · [[ProstT5]]

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
- [[Módulo 3 - MOC]]
