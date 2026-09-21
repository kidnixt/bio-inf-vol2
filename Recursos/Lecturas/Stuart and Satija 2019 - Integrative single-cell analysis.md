---
tags: [lectura, modulo-1, single-cell, integracion]
area: Lecturas
tipo: review
autores: Tim Stuart, Rahul Satija
año: 2019
revista: Nature Reviews Genetics
doi: 10.1038/s41576-019-0093-7
aliases: [Stuart y Satija 2019, Stuart & Satija 2019, Integrative single-cell analysis]
---

# Stuart & Satija (2019) — *Integrative single-cell analysis*

> [!info] Ficha de la lectura
> **Tipo:** review — *Nature Reviews Genetics*
> **Autores:** Tim Stuart y Rahul Satija (New York Genome Center / NYU — el grupo de **Seurat**)
> **Clase asociada:** [[Aproximaciones ómicas con resolución de célula única]] (clase 1)
> **PDF:** [[Stuart and Satija 2019 - Integrative single-cell analysis.pdf]]

## En una frase

Medir una sola capa molecular por célula es una limitación **metodológica, no biológica**: la review ordena las técnicas que miden varias modalidades en la misma célula y los métodos computacionales que integran datos de distintas células, experimentos, especies y del espacio.

## Por qué leerla después de la clase

La clase cierra con la [[Integración de datos multiómicos]] y el [[Batch effect]] como desafíos abiertos, y con la pregunta *¿cómo definimos molecularmente a una célula?*. Esta review es la versión extendida de esa diapositiva: explica **cómo** se resuelven hoy esos dos problemas. La figura de la clase que agrupa técnicas en *Lineage / State / Trajectory* (la de "atlas moleculares de la vida") es la **Fig. 1** de este paper.

---

## 1. Cómo se obtienen datos multimodales de una misma célula

Cuatro estrategias experimentales:

| Estrategia | Idea | Ejemplos | Límite |
|---|---|---|---|
| **Citometría antes de destruir la célula** | Medir proteínas de superficie por fluorescencia (*index sorting* en [[Citometría de flujo\|FACS]]) y después hacer [[scRNA-seq]] a la misma célula | Progenitores hematopoyéticos, células madre raras | Pocos parámetros: los fluoróforos se solapan espectralmente |
| **Separar fracciones celulares** (*lyse-and-split*) | Separar núcleo y citosol → ADN genómico por un lado, ARNm por otro | G&T-seq (genoma + transcriptoma), scM&T-seq (metilación + transcriptoma), PEA para proteínas intracelulares | Bajo throughput; 82–96 ARN y 38–75 proteínas por experimento |
| **Convertir todo a un formato común: ADN secuenciable** | Anticuerpos con **barcode de ADN poliadenilado** que se captura junto con los ARNm | **[[CITE-seq]]**, **REAP-seq** (ARN + proteínas de superficie); guías de CRISPR con barcode; *lineage tracing* con Cas9 | Todavía difícil para proteínas **intracelulares** (permeabilizar degrada el ARN) |
| **Extraer más información del propio scRNA-seq** | Leer la secuencia, no solo contar | Mutaciones somáticas → linaje; variantes de número de copia en tumores; eQTLs; **RNA velocity** a partir de intrones sin procesar | Depende de la cobertura del transcripto |

> [!tip] La idea que unifica todo
> *"Si la información celular se puede convertir en un barcode secuenciable, se puede leer con resolución de célula única junto con el transcriptoma."* Es la misma lógica del [[Barcode celular]] y el [[UMI]] de la clase, llevada a proteínas, perturbaciones y linajes.

### Linaje con CRISPR

Un arreglo sintético de sitios blanco de Cas9 acumula mutaciones con cada división; las células que comparten mutaciones vienen del mismo progenitor. Si el arreglo se transcribe con cola poli-A, se captura en el mismo experimento de [[scRNA-seq]] → **árbol de linaje + transcriptoma** de cada célula (scGESTALT, ScarTrace, LINNAEUS en pez cebra). MEMOIR lo lee por imagen (smFISH), sumando la **posición**.

### [[RNA velocity]]

La proporción de transcriptos **sin empalmar** (con intrones) indica si un gen se está encendiendo o apagando. Eso permite estimar el estado *futuro* de cada célula y resolver problemas clásicos del [[Pseudotiempo]]: dónde empieza la trayectoria, ramificaciones y ciclos.

---

## 2. Cómo se analizan datos multimodales

- Analizar cada modalidad por separado puede dar **clusters contradictorios** (dos células iguales por ARN y distintas por proteína).
- El análisis **conjunto** (reducción dimensional conjunta: CCA, NMF, **MOFA**) resuelve estados que ninguna modalidad resuelve sola. Ejemplo: subtipos de linfocitos T (memoria, regulatorios) casi indistinguibles por ARN por la [[Sparsity|escasez de detección (*drop-out*)]], pero claros por proteínas de superficie.
- Modelos que **predicen una modalidad a partir de otra** (p. ej., expresión a partir de accesibilidad de cromatina) revelan regulación: incluir sitios distales mejoró cuatro veces la predicción respecto de usar solo sitios cis.

---

## 3. Integrar datos de **distintas** células: el problema del batch

Los métodos de corrección de [[Batch effect]] pensados para bulk **no sirven** en single cell: no distinguen un cambio en la *proporción* de tipos celulares de un cambio en el *programa* de un tipo celular. Primero hay que encontrar estados biológicos equivalentes entre datasets.

| Método | Cómo encuentra lo compartido |
|---|---|
| **CCA** ([[Seurat y Scanpy\|Seurat]] v2) | Busca combinaciones de genes **máximamente correlacionadas entre datasets** (a diferencia del [[PCA]], que maximiza varianza dentro de uno solo y por eso captura el batch); luego alinea con *dynamic time warping* |
| **MNN** (mnnCorrect) | Pares de células que son **vecinas mutuas más cercanas** entre datasets → vector de corrección |
| **Harmony** (Korsunsky) | Variante de k-means que favorece clusters mezclados; integra 500.000 células en una PC |

Aplicaciones que muestra la review:

- **Meta-análisis**: cuatro estudios independientes de islotes pancreáticos → un solo dataset con más poder estadístico para encontrar células raras.
- **Comparar condiciones**: PBMCs control vs estimuladas con interferón-β → 13 tipos celulares compartidos y una respuesta específica de células dendríticas plasmacitoides.
- **Comparar especies**: cerebro de reptil vs mamífero, islotes humano vs ratón, desarrollo embrionario humano vs ratón alineando trayectorias. El cuello de botella es identificar bien los **ortólogos** → ver [[Shafer 2019 - Cross-species analysis of scRNAseq data]].

### Anotación con referencia

Transferir etiquetas desde un atlas anotado (scmap-cell, scmap-cluster, SVM, LDA) puede resolver subpoblaciones que el clustering *de novo* no separa. Es la "estrategia automatizada" de [[Anotación de tipos celulares]] que muestra la clase.

### Integrar modalidades sin features en común

ARN mide genes; ATAC o metilación miden regiones del genoma. Soluciones: alinear trayectorias 1D (MATCHER — mostró que la metilación **va detrás** de la expresión en reprogramación a iPSC), entrenar un clasificador con los tipos celulares compartidos (*gradient boosting*), o suponer correlaciones entre features (LIGER asume metilación del cuerpo génico ↔ menor expresión; Seurat v3 transfiere tipos de scRNA-seq a [[scATAC-seq]]).

---

## 4. Integrar con el espacio

La disociación borra la posición — el punto de partida de [[Biología espacial - mapeando la expresión génica a su entorno|la clase 2]]. Dos caminos:

1. **Computacional**: medir por FISH unos pocos genes *landmark* con patrón espacial conocido, y usarlos para **ubicar** cada célula de scRNA-seq en el tejido. Después se puede predecir el mapa espacial de *cualquier* gen. Funcionó en tejidos de estructura simple (embrión temprano, hígado); en tejidos maduros o tumores es más difícil.
2. **Experimental**: medir in situ muchos genes a la vez (osmFISH, **STARmap**, [[MERFISH]], seqFISH — descendientes del [[FISH y smFISH|smFISH]]) → ver [[Métodos basados en sondas]] y [[Integración de datos single cell y spatial]].

---

## 5. Cierre

- El [[Human Cell Atlas]] va a necesitar herramientas de "transferencia" entre datasets **análogas a los alineadores de secuencias** para el genoma de referencia.
- Mencionan la [[Secuenciación con nanoporos]] como promesa multimodal (ARN y ADN nativos, modificaciones de bases) — conexión con la [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica|clase 3]].
- *¿Qué es un tipo celular?* — la misma pregunta con la que cierra la clase 1; responderla va a requerir combinar modalidades y condiciones, como *¿qué es un gen?* requirió comparar secuencias entre especies.

## Conceptos del vault

[[scRNA-seq]] · [[scATAC-seq]] · [[CITE-seq]] · [[RNA velocity]] · [[Seurat y Scanpy]] · [[Integración de datos multiómicos]] · [[Batch effect]] · [[Anotación de tipos celulares]] · [[Identidad celular]] · [[Pseudotiempo]] · [[PCA]] · [[Clustering]] · [[Sparsity]] · [[Citometría de flujo]] · [[Metilación del ADN]] · [[Human Cell Atlas]] · [[Integración de datos single cell y spatial]]

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
- [[Módulo 1 - MOC]]
