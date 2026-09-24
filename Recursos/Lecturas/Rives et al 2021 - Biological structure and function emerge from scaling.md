---
tags: [lectura, modulo-3, PLM, estructura]
area: Lecturas
tipo: research article
autores: Alexander Rives, Joshua Meier, Tom Sercu, Siddharth Goyal, Zeming Lin, Jason Liu, Demi Guo, Myle Ott, C. Lawrence Zitnick, Jerry Ma, Rob Fergus
año: 2021
revista: PNAS 118(15), e2016239118
doi: 10.1073/pnas.2016239118
aliases: [Rives 2021, ESM-1b paper, "Biological structure and function emerge from scaling unsupervised learning to 250 million protein sequences"]
---

# Rives et al. (2021) — *Biological structure and function emerge from scaling unsupervised learning to 250 million protein sequences*

> [!info] Ficha de la lectura
> **Tipo:** research article — *PNAS* (el PDF del vault es el preprint de bioRxiv, doi 10.1101/622803)
> **Autores:** Facebook AI Research (hoy Meta AI) y NYU
> **Clase asociada:** [[Modelos de lenguaje de proteínas y embeddings proteicos]] (clase 9)
> **PDF:** [[Rives et al 2021 - Biological structure and function emerge from scaling.pdf]]
> **Modelo:** `huggingface.co/facebook/esm1b_t33_650M_UR50S`

## En una frase

El paper de **[[ESM-1b y ESM-2|ESM-1b]]**: entrenar un transformer con [[Masked language modeling|máscaras]] sobre **86 mil millones de aminoácidos** de **250 millones de secuencias**, y descubrir que en sus representaciones quedó codificada la **estructura** que nadie le enseñó.

## Por qué leerla después de la clase

Es el paper del que sale la Figura 5 que la clase muestra (el [[Mapa de contactos]] contra CCMpred) y la frase *"nadie le enseñó estructura, y sin embargo quedó codificada"*. Leerlo aporta el **encuadre conceptual**, que es más fuerte que el resultado puntual.

---

## 1. La idea de fondo

> "La idea de que la función y la estructura biológicas están registradas en la estadística de las secuencias seleccionadas por la evolución tiene una larga historia."

El paper recupera esa tradición (Yanofsky 1964, Altschuh 1987–88, Göbel 1994) y la reformula: de todas las perturbaciones posibles a una secuencia, **la evolución sesga hacia las compatibles con el fitness**. Las variables no observadas que determinan ese fitness —estructura, función, estabilidad— quedan por lo tanto **impresas en la distribución de secuencias observadas**.

Un modelo de lenguaje entrenado sobre esa distribución tiene que aprender algo de esas variables para poder predecir bien. Esa es la justificación completa de la frase de cierre de la clase: *"la evolución ya resolvió el problema; el modelo absorbe esas restricciones sin que nadie se las explicite"*.

## 2. Lo que emerge

| Nivel | Qué queda codificado |
|---|---|
| Bioquímico | Propiedades de los aminoácidos: hidrofobicidad, carga, peso |
| Evolutivo | Homología remota, alineamiento de familias |
| Estructural | Estructura secundaria y **contactos terciarios** |
| Funcional | Efecto de mutaciones sobre la actividad |

## 3. El matiz metodológico que la clase remarca

La información **está** en las representaciones, pero **para leerla hace falta una sonda entrenada**: una proyección lineal o un clasificador chico. Nadie le pasó un solo contacto durante el pre-entrenamiento — los aprendió de rellenar máscaras.

Ese patrón —**[[Embedding|embeddings]] congelados + un modelo simple encima**— es el mismo que:

- usa [[ProtT5 y ProtBERT|ProtTrans]] para sus benchmarks;
- usa el trabajo de tesis de Juan Diego Puglia (ORT) para predecir localización subcelular con 96 % de F1;
- usa [[Phold]] (una CNN de dos capas sobre embeddings de [[ProstT5]]).

## 4. Qué aporta respecto de la clase

- **El marco teórico**, que la clase comprime en una frase. Es lo más citable del paper y lo que distingue a los PLMs de "aplicar NLP a proteínas porque sí".
- **La escala como variable experimental**: el paper muestra que la calidad de las representaciones mejora con el tamaño del modelo y con la diversidad de los datos. Esa curva es la que [[Lin et al 2023 - Evolutionary-scale prediction with a language model|ESM-2]] extiende hasta 15.000 millones de parámetros, y la que [[Elnaggar et al 2023 - Ankh|Ankh]] discute.
- **La comparación con CCMpred**, el método clásico basado en covariación en un [[Alineamiento múltiple de secuencias|MSA]]. Ver los dos en la misma matriz deja claro que no es "el PLM anda bien" sino "el PLM extrae del texto solo lo que el método clásico extraía de los homólogos".

## Conceptos del vault

[[ESM-1b y ESM-2]] · [[Mapa de contactos]] · [[Masked language modeling]] · [[Transformer]] · [[Embedding]] · [[Modelo de lenguaje de proteínas]] · [[Alineamiento múltiple de secuencias]] · [[Homología remota]]

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
- [[Módulo 3 - MOC]]
