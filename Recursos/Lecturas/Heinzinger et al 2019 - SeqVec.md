---
tags: [lectura, modulo-3, embeddings, PLM]
area: Lecturas
tipo: research article
autores: Michael Heinzinger, Ahmed Elnaggar, Yu Wang, Christian Dallago, Dmitrii Nechaev, Florian Matthes, Burkhard Rost
año: 2019
revista: BMC Bioinformatics 20, 723
doi: 10.1186/s12859-019-3220-8
aliases: [Heinzinger 2019, SeqVec paper, "Modeling aspects of the language of life through transfer-learning protein sequences"]
---

# Heinzinger et al. (2019) — *Modeling aspects of the language of life through transfer-learning protein sequences*

> [!info] Ficha de la lectura
> **Tipo:** research article — *BMC Bioinformatics* (acceso abierto)
> **Autores:** grupo de **Burkhard Rost** (TUM) — el mismo laboratorio que después hace [[ProtT5 y ProtBERT|ProtTrans]] y [[ProstT5]]
> **Clase asociada:** [[Modelos de lenguaje de proteínas y embeddings proteicos]] (clase 9)
> **PDF:** [[Heinzinger et al 2019 - SeqVec.pdf]]

## En una frase

El paper de **[[ELMo y SeqVec|SeqVec]]**: aplicar la arquitectura ELMo a secuencias de proteínas, y mostrar que un embedding **contextual** entrenado sobre UniRef50 permite predecir estructura y localización **sin alineamientos**.

## Por qué leerla después de la clase

La clase usa su Figura 2 (la proyección [[t-SNE|t-SNE]] donde los embeddings sin entrenar ya agrupan por función) y su comparación de rendimiento. El paper agrega el **argumento estratégico** que la clase menciona al pasar y que resulta central para toda la familia: por qué querríamos prescindir de la información evolutiva.

---

## 1. Los dos problemas que plantea

Durante 26 años, el estado del arte combinó machine learning con **información evolutiva** de un [[Alineamiento múltiple de secuencias|MSA]]. Eso tiene dos costos:

1. **Tiempo** — recuperar proteínas relacionadas se volvió demasiado lento para algunas aplicaciones.
2. **Cobertura** — la información evolutiva es **débil para familias chicas**, por ejemplo las proteínas del *Dark Proteome*.

El segundo punto es el importante y es el que reaparece en toda la cadena: en el [[ESM Atlas]] (proteínas metagenómicas sin parientes conocidos) y en [[Phold]] (fagos cuyas proteínas no tienen homólogos detectables). Ver [[Homología remota]].

## 2. Los resultados

| Nivel | Tarea | Resultado |
|---|---|---|
| Por residuo | Estructura secundaria | **Q3 = 79 % ± 1**, Q8 = 68 % ± 1 |
| Por residuo | Regiones de desorden intrínseco | **MCC = 0,59 ± 0,03** |
| Por proteína | Localización subcelular (10 clases) | **Q10 = 68 % ± 1** |
| Por proteína | Membrana vs. soluble | **Q2 = 87 % ± 1** |

Todos **significativamente mejores** que one-hot encoding o que enfoques tipo [[Word2vec]] ([[ProtVec]]). La clase reporta además el salto de **77,6 → 92,3** en predicción de membrana cuando DeepLoc usa SeqVec en vez de ProtVec.

## 3. El hallazgo que la clase destaca

En la proyección t-SNE, **los embeddings del modelo sin entrenar ya separan proteínas por localización celular y por carácter de membrana** — una señal que el modelo nunca recibió como etiqueta. Entrenarlo **mejora** la separación, no la crea.

Es la misma observación de [[Asgari and Mofrad 2015 - Continuous distributed representation of biological sequences|Asgari & Mofrad]] cuatro años antes, y la misma que [[Rives et al 2021 - Biological structure and function emerge from scaling|Rives et al.]] dos años después. La diferencia entre las tres es **qué tan profunda es la propiedad que emerge**: de propiedades biofísicas de 3-meros, a localización, a [[Mapa de contactos|contactos 3D]].

## 4. Qué aporta respecto de la clase

- **La honestidad sobre el límite.** SeqVec queda *cerca* de los mejores métodos, no los supera: sin información evolutiva se paga un precio. Lo que el paper defiende es la **relación costo/beneficio** (velocidad, y cobertura en familias chicas). Recién [[ProtT5 y ProtBERT|ProtT5]] va a superar el estado del arte por residuo sin MSA.
- **La arquitectura en detalle** — dos biLSTM por dirección, 4096 unidades con proyección a 512, entrada **por caracteres**. Ese último punto es más natural en proteínas que en texto: el vocabulario son 20 letras y no hay palabras fuera de vocabulario.
- **El autor.** Heinzinger firma también [[Heinzinger et al 2024 - ProstT5|ProstT5]] (2024) y aparece entre los autores de [[Bouras et al 2026 - Phold|Phold]] (2026). Toda la línea 1D → 3D del vault sale del mismo laboratorio.

## Conceptos del vault

[[ELMo y SeqVec]] · [[Embedding]] · [[Modelo de lenguaje de proteínas]] · [[Alineamiento múltiple de secuencias]] · [[Homología remota]] · [[t-SNE]] · [[ProtVec]] · [[UniProt]]

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
- [[Módulo 3 - MOC]]
