---
tags: [lectura, modulo-3, fármacos, IA]
area: Lecturas
tipo: review (keynote)
autores: Lei Wang, Zhenran Zhou, Xixi Yang, Shaohua Shi, Xiangxiang Zeng, Dongsheng Cao
año: 2024
revista: Drug Discovery Today 29(6), 103985
doi: 10.1016/j.drudis.2024.103985
aliases: [Wang 2024, "The present state and challenges of active learning in drug discovery"]
---

# Wang et al. (2024) — *The present state and challenges of active learning in drug discovery*

> [!info] Ficha de la lectura
> **Tipo:** *Keynote review* — *Drug Discovery Today*
> **Autores:** Central South University y Hunan University (China)
> **Clase asociada:** [[Métodos para el diseño computacional de fármacos]] (clase 6)
> **PDF:** [[Wang et al 2024 - Active learning in drug discovery.pdf]]

## En una frase

La revisión de la que sale la diapositiva *"Active learning — Aplicaciones"* de la clase: qué es el [[Aprendizaje activo]], cómo se arma un ciclo, y qué hace en cada etapa del descubrimiento de fármacos.

## Por qué leerla después de la clase

La clase muestra el esquema del ciclo y la tabla de aplicaciones. El paper desarma el ciclo en **cuatro componentes de diseño** y, sobre todo, explica la distinción **explorar vs. explotar**, que es la decisión que realmente define un AL y que la diapositiva deja implícita.

---

## 1. Por qué AL y no solo ML

El [[Machine Learning|ML]] aplicado a descubrimiento de fármacos choca con tres problemas de datos: **pocas etiquetas**, obtenerlas es **caro**, y los conjuntos etiquetados están **desbalanceados y son redundantes**. El AL ataca los tres a la vez: selecciona qué etiquetar, y también qué descartar de lo ya etiquetado.

El paper señala que la idea tiene ~40 años y entró al descubrimiento de fármacos hace ~20, pero que su aplicación fue limitada porque **no encajaba con la rigidez del cribado de alto rendimiento**. Lo que cambió es la **automatización** del HTS: recién cuando el laboratorio puede correr rondas chicas y adaptativas, un ciclo iterativo tiene sentido.

## 2. Los cuatro componentes

| Componente | Decisiones |
|---|---|
| **Conjunto inicial** | En estudios prospectivos, datos históricos preprocesados; en retrospectivos, un subconjunto chico al azar |
| **Algoritmo de ML** | Desde RF y SVM hasta redes profundas y transfer learning |
| **Estrategia de consulta** | El corazón del método (ver abajo) |
| **Métricas de corte** | Basadas en moléculas (activos y *scaffolds* recuperados) o en el modelo (cambio de desempeño, importancia de rasgos) |

## 3. La distinción que importa

| Estrategia | Qué prioriza | Riesgo |
|---|---|---|
| **Explotativa** (*greedy*) | Moléculas con alta actividad potencial | No mejora el modelo |
| **Explorativa** (incertidumbre) | Moléculas informativas, aunque no sean activas | No encuentra nada útil en el corto plazo |
| **Balanceada** | Mezcla —desde 50/50 hasta pesos ajustables— | — |

Ese es el punto que separa al AL del cribado ordenado por score: **el mejor compuesto para medir no es el de mejor predicción**, es el que más reduce la incertidumbre.

Ejemplos que el paper destaca: Reker et al. muestran que la estrategia *curious* (elegir los pares molécula-blanco más inciertos) construye un conjunto balanceado con amplia cobertura de blancos a partir de datos desbalanceados.

## 4. Una limitación honesta

Las métricas de corte **evalúan la iteración actual y no miden la ganancia potencial de seguir iterando**. Algunos trabajos recientes recurren a modelado analítico y estadística para estimar el beneficio de rondas adicionales. Es decir: *cuándo parar* sigue sin estar resuelto.

## 5. Qué aporta respecto de la clase

- **La tabla de aplicaciones desarrollada**: predicción de interacción compuesto–blanco (donde AL ataca el desbalance), [[Virtual screening]] (ayuda al LBVS a encontrar *scaffolds* nuevos y mejora eficiencia y precisión del SBVS), generación y optimización de moléculas, y predicción de propiedades.
- **La conexión con el HTS automatizado**, que explica por qué el AL es reciente en la práctica y no solo en los papers.
- **El marco para el ciclo "IA-driven"** que la clase enuncia: *la medición actualiza el modelo y cambia la próxima decisión*. Acá está el detalle de cómo se implementa esa frase.

## Conceptos del vault

[[Aprendizaje activo]] · [[Machine Learning]] · [[Virtual screening]] · [[Diseño de fármacos asistido por computadora]] · [[Diseño basado en ligandos]] · [[Diseño basado en estructura]] · [[QSAR]] · [[ChEMBL]] · [[Inteligencia Artificial]]

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
- [[Módulo 3 - MOC]]
