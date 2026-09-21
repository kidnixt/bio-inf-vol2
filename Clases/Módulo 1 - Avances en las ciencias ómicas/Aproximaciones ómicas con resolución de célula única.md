---
titulo: Aproximaciones ómicas con resolución de célula única
curso: Fronteras y Perspectivas en Bioinformática – Universidad ORT
modulo: Módulo 1 - Avances en las ciencias ómicas
clase: 1
docente: Guillermo Eastman
año: 2026
tags:
  - clase
  - modulo-1
  - single-cell
  - omicas
---

# Aproximaciones ómicas con resolución de célula única

> [!info] Ficha de la clase
> **Curso:** Fronteras y Perspectivas en Bioinformática – Universidad ORT (2026) · **Clase 1**
> **Módulo:** [[Módulo 1 - MOC|Módulo 1 - Avances en las ciencias ómicas]]
> **Docente:** [[Guillermo Eastman]] — Departamento de Genómica, [[IIBCE]]
> **Diapositivas:** [[Diapositivas - Aproximaciones ómicas con resolución de célula única.pdf]]
> **Resumen de la clase (material del curso):** [[Resumen - Genómica de célula única (scRNA-seq).pdf]]
> **Lecturas:** [[Slovin et al 2021 - scRNA-seq analysis a step-by-step overview|Slovin et al. 2021]] · [[Stuart and Satija 2019 - Integrative single-cell analysis|Stuart & Satija 2019]] · [[Shafer 2019 - Cross-species analysis of scRNAseq data|Shafer 2019]]
> **Clase siguiente:** [[Biología espacial - mapeando la expresión génica a su entorno]]

> [!abstract] Cómo leer este resumen
> Sigue la estructura de las diapositivas y completa lo que las figuras dejan implícito. Lo que se **dijo en clase** y no está en las diapositivas (tomado del resumen del curso) va en recuadros *"En la clase"*. Al final de cada bloque se indica qué **lectura** lo profundiza.

---

## Objetivos de la clase

1. ¿Por qué necesitamos resolución de célula única?
2. ¿Cómo se generan estos datos?
3. ¿Qué tipo de preguntas biológicas podemos responder?
4. ¿Qué desafíos bioinformáticos aparecen?

## Contenido

- ¿Por qué estudiar células individuales?
- [[Expresión génica]] y cuantificación de [[Transcriptoma|transcriptomas]]
- [[scRNA-seq|Single cell RNA-seq]]: "la revolución"
- Más allá del transcriptoma: ómicas single-cell
- Desafíos bioinformáticos
- Aplicaciones biológicas

---

## 1. ¿Por qué estudiar células individuales?

La premisa de toda la clase: **la mayoría de los tejidos son heterogéneos**. Un órgano (cerebro, ganglio linfático, páncreas, hígado, colon, riñón — el círculo de órganos de la primera diapositiva) no es un bloque uniforme, sino una **comunidad de células diferentes** que conviven, se comunican y cumplen funciones distintas: la [[Heterogeneidad celular]].

El ejemplo que acompaña es un **tumor**: en el centro hay células tumorales organizadas en subclones distintos, y en la periferia un **microambiente** de células inmunes, vasos y fibroblastos. Dos regiones del mismo tumor pueden tener composiciones completamente diferentes.

> [!quote] En la clase
> La heterogeneidad aparece tanto en condiciones fisiológicas como patológicas: en un tumor, la composición celular cambia desde zonas homogéneas en el centro hasta regiones invasivas muy dinámicas en la periferia.

### El ejemplo del tejido cerebral

El [[Tejido cerebral]] ilustra la escala del problema. La diapositiva muestra un **corte transversal de cerebro de ratón** coloreado por tipo celular:

| Escala | Número aproximado |
|---|---|
| Células en cerebro de ratón | ~110 millones |
| Células en cerebro humano | ~170 mil millones |

Se reconocen **4 grandes tipos celulares**, cada uno con subdivisiones:

- **[[Neurona|Neuronas]]** → excitatorias / inhibitorias
- **[[Macroglía|Macroglías]]** (soporte y mantenimiento) → [[Astrocito|astrocitos]], [[Oligodendrocito|oligodendrocitos]], progenitores de oligodendrocitos ([[Oligodendrocito|OPCs]])
- **[[Microglía|Microglías]]** (sistema inmune del SNC) → homeostática / reactiva
- **Células sanguíneas** → [[Célula endotelial|endoteliales]], musculares

La jerarquía que se usa hoy para nombrar células va de lo grueso a lo fino:

```
[Clase General]  (4)
   ➜ [Subclase]  (docenas)
        ➜ [Clúster / Tipo Celular]  (>3000)
```

Esa jerarquía es el problema de la [[Identidad celular]]: cuántos niveles se reconocen depende de la resolución con la que midamos.

### ¿Cómo definimos una célula a nivel molecular?

> **En función de conocer *qué genes expresa*.**

La diapositiva lo apoya con el inventario del genoma humano:

| Categoría | Nº de genes |
|---|---|
| Codificantes de proteína | 19.433 |
| lncRNA (ARN largos no codificantes) | 35.899 |
| ARN pequeños | 7.563 |
| Pseudogenes | 14.701 |
| **Total** | **78.691** |

Todas las células de un organismo comparten ese genoma; lo que las distingue es **cuáles se prenden**. Los ejemplos visuales:

- Una **célula de hígado** transcribe el gen de la **alcohol deshidrogenasa** y no el del neurotransmisor; una **neurona**, al revés.
- Tres tipos celulares (**músculo, intestino, neurona**) representados como semáforos sobre los mismos genes: verde (encendido), rojo (apagado), amarillo (expresión intermedia). El patrón de semáforos *es* la identidad.

Si la identidad está codificada en el programa de expresión, medir [[Expresión génica]] célula por célula es medir identidad celular.

---

## 2. Expresión génica y transcriptomas

### El flujo de la información genética

El [[Dogma central de la biología molecular|dogma central]]: ADN → (transcripción) → [[ARN mensajero|ARNm]] → ([[Traducción|traducción]]) → polipéptido. La clase lo complementa con el esquema de los **seis niveles de regulación** de la expresión en una célula eucariota:

1. Remodelado de la [[Cromatina]] (ADN "abierto" accesible)
2. Transcripción → transcripto primario (pre-ARNm)
3. Procesamiento del ARN (cap en 5', cola poli-A en 3') → ARNm maduro
4. **Estabilidad del ARNm** en el citoplasma (degradación; la vida media varía)
5. Traducción
6. Modificaciones postraduccionales (plegado, glicosilación, transporte, activación, degradación)

### ¿Qué es un transcriptoma?

> La colección completa de todas las moléculas de ARN presentes en una célula o tejido en un momento dado.

En el esquema, el [[Transcriptoma]] corresponde al **paso 4**: el ARNm maduro y estable presente en el citoplasma. Medirlo responde **qué genes** se están expresando y **en qué nivel**.

Un punto clave es el **[[Rango dinámico]]** de abundancia de transcriptos — varios órdenes de magnitud dentro de la misma célula:

| Gen | Abundancia relativa (orden) |
|---|---|
| GAPDH | ~100.000 |
| ACTB | ~10.000 |
| MAP2 | ~1.000 |
| RBFOX3 | ~100 |
| TREM2 | ~10 |
| NANOG | ~1 |

Los genes más informativos (marcadores de tipo celular, factores de transcripción) suelen ser los de **baja abundancia**, los más difíciles de detectar.

> [!quote] En la clase
> - El rango dinámico abarca **5–6 órdenes de magnitud** (10⁵–10⁶).
> - Ante la pregunta de si el transcriptoma cambia a lo largo del ciclo celular: las técnicas actuales toman una **"fotografía"** estática del estado celular; con series temporales o métodos computacionales ([[Pseudotiempo]]) se puede reconstruir la **"película"**.

### Transcriptómica bulk

El [[Bulk RNA-seq]] en seis pasos: (1) aislar ARN de la muestra, (2) fragmentarlo, (3) convertirlo a ADNc, (4) ligar adaptadores y amplificar, (5) secuenciar por NGS, (6) mapear las lecturas al transcriptoma/genoma (atravesando uniones exón–intrón).

La advertencia conceptual de la clase:

> **No estamos midiendo *expresión* directamente. Estamos cuantificando la abundancia de las moléculas de ARN muestreadas.**

Todo lo que llamamos "expresión" pasa por filtros técnicos: **sampleo**, **[[Profundidad de secuenciación]]**, **ruido** y **distribución de conteos**.

El resultado es una [[Matriz de conteo]] modesta, ~10.000 genes × [6–10] condiciones:

```
          Sample 1   Sample 2   Sample 3
Gene A      1000       1200        950
Gene B        20         50         15
Gene C         0          2          1
```

Sobre ella, los análisis clásicos que muestra la diapositiva:

| Análisis | Qué se ve |
|---|---|
| *Sample clustering* | [[PCA]] de las muestras: las réplicas de cada condición se agrupan |
| **DEGs** | *Volcano plot* de [[Expresión diferencial\|genes diferencialmente expresados]] |
| [[Gene Ontology]] | Árbol de términos enriquecidos |
| Genes co-regulados | Clusters de genes que siguen la misma curva en el tiempo (meses) |

### Las limitaciones del bulk

Si la muestra es corteza cerebral, hipocampo o un tumor, el bulk devuelve **promedios**, y en un promedio se pierden:

- Los distintos [[Tipo celular|tipos celulares]]
- Los [[Estado celular|estadíos / estados celulares]]
- Las subpoblaciones
- Las **células raras** (a menudo las biológicamente decisivas)

---

## 3. La "revolución": single cell RNA-seq

> **Promedios → Distribuciones**

La analogía de la diapositiva: el bulk (2006 → presente) es un **licuado** de frutas; el single cell (2012 → presente) es la **ensalada de frutas** con cada pieza separada.

> [!quote] En la clase — la analogía del licuado
> En el licuado se perciben los sabores predominantes (frutilla, banana) pero no las proporciones ni la composición de cada fruta. El single cell permite medir la distribución y el estado de cada elemento por separado — y detectar **subpoblaciones raras**, **estados intermedios de diferenciación** o cambios **restringidos a un solo tipo celular**.

La figura que lo formaliza: un tejido heterogéneo → ARN total → bulk dice *"no hay cambio de expresión del gen X"*. El mismo tejido → ADNc con barcode por célula → clusters a, b, c → **el gen X cambia solo en el tipo celular b**. El promedio lo había diluido.

### 1er desafío: matchear secuencias con células únicas

*¿Cómo sabemos de qué célula proviene cada molécula de ARN secuenciada?* Dos frentes complementarios, con un objetivo común: **lograr realizar reacciones de biología molecular en células individuales**.

| Frente | Solución |
|---|---|
| **Protocolos de tecnología avanzada** | [[Aislamiento de células individuales]] |
| **Biología molecular** | [[Barcode celular\|Barcodes]] + [[UMI]] (*unique molecular identifier*) |

#### Aislamiento de células individuales

**Primera generación** — poco automatizadas, poco eficientes, lentas para grandes números de células:

| Técnica | Cómo funciona (según la figura) |
|---|---|
| [[Dilución al límite]] | Diluciones seriadas 1:10 (de 50.000 a 5 células/ml) hasta tener ~1 célula por volumen |
| [[Micromanipulación]] | Pipeta capilar bajo el microscopio que "pesca" una célula |
| [[Microdisección por captura láser]] (LCM) | Un láser recorta la célula de un corte de tejido y la deposita en un tubo |

**Alto rendimiento** — las que hicieron viable la escala actual:

| Técnica | Cómo funciona |
|---|---|
| [[Citometría de flujo\|Citometría (*cell sorting*, FACS)]] | Las células pasan de a una frente a un láser; un detector multiespectral decide y una carga eléctrica las desvía a distintos tubos |
| [[Microfluídica]] y microgotas | Un canal une células en suspensión + micropartículas con *buffer* de lisis; el aceite las corta en **gotas con una sola célula** |

La diapositiva siguiente muestra la **evolución de la escala**: de 1 célula por estudio (2009) a ~10⁶ (2017), a medida que se pasó de manual → multiplexado en placas → circuitos microfluídicos integrados (Fluidigm C1) → robótica → **nanogotas** (Drop-seq, inDrop, 2015) → *picowells* (Seq-Well) → **barcoding in situ** combinatorio (sci-RNA-seq, SPLiT-seq, 2017). En el camino aparecen STRT-seq, SMART-seq/SMART-seq2, CEL-seq, MARS-seq, CytoSeq y [[10x Genomics]].

#### Barcodes y UMIs

La lectura secuenciada se construye con cuatro elementos:

| Elemento | Función |
|---|---|
| Adaptador | Anclaje para secuenciar |
| [[Barcode celular]] | Identifica **la célula** |
| [[UMI]] | Identifica **moléculas individuales** |
| Lectura (ADNc) | Identifica el **transcripto / secuencia** |

#### Un ejemplo: el workflow de [[10x Genomics]]

1. **Gel beads** con barcode + células + enzimas se juntan en un chip microfluídico con aceite → **GEMs** (*Gel beads in EMulsion*): gotas con una célula y un bead.
2. Dentro de cada gota ocurre la **retrotranscripción**: cada ADNc queda marcado con el barcode del bead.
3. Se rompe la emulsión, se juntan todos los ADNc (*pool*) y se secuencian.
4. Resultado: perfil transcripcional de cada célula (célula 1 … célula 5.000 × gen 1 … gen 2.000).

Cada **bead funcionalizado** está cubierto de oligos que comparten el barcode 10x y tienen cada uno un UMI distinto.

La clase contrasta las dos químicas:

| | **3' Assay** | **5' Assay** |
|---|---|---|
| Oligo del bead | Read 1 + barcode 10x + UMI + **poly(dT)VN** | Read 1 + barcode 10x + UMI + **TSO** (*template switch oligo*) |
| Captura | El poly(dT) del bead se hibrida a la cola poli-A del ARNm | El cebador poly(dT) (o no-poly(dT)) está **en solución** |
| Cómo se completa | Retrotranscripción → el TSO en solución agrega el extremo 5' (*template switching*) | Retrotranscripción → el **TSO del bead** hace el *template switching* en el extremo 5' |
| Qué extremo del transcripto queda junto al barcode | 3' | 5' |

En ambos casos se obtiene ADNc de ARNm poliadenilado; el 5' permite, por ejemplo, leer el extremo variable de receptores inmunes.

> [!quote] En la clase
> Cada bead tiene **cientos de miles de sondas** con el mismo barcode y UMIs distintos. El 3'-assay es el más usado.

### 2do desafío: la cantidad de ARN

¿Cuánto ARN hay en una célula? Tras aislarla y lisarla:

| Molécula | Cantidad |
|---|---|
| ADN | ~6 pg |
| ARN total | ~10 pg |
| ARNm | **~0,1 pg** |

La solución es la **amplificación de ADNc por PCR** — y la PCR introduce su propio sesgo (algunas secuencias se amplifican más que otras). Por eso el [[UMI]] se agrega **antes** de amplificar: todas las copias de una molécula comparten el mismo UMI, y en el análisis se hace **deduplicación** (UMIs → enriquecimiento por PCR → secuenciación → deduplicación → vuelven a quedar las moléculas originales).

> [!quote] En la clase
> Del ARN total, el ARNm codificante es apenas **1–5 %**. La deduplicación por UMI "cuenta un UMI por molécula única" y elimina la distorsión por sobreamplificación.

### 3er desafío: el alineamiento

Lo primero que sale de un experimento son **secuencias (raw data)**, y ahí aparece la explosión de datos:

| | [[Bulk RNA-seq]] | [[scRNA-seq]] |
|---|---|---|
| Diseño típico | 3 vs 3 (6 muestras) | 10k células |
| Lecturas | 20–30 M por muestra | 20k–50k por célula → **200–500 M** |
| Metadata técnica | — | [[Barcode celular\|barcodes]] + [[UMI\|UMIs]] |

Las [[Alineamiento de secuencias|herramientas clásicas de alineamiento]] sufren con los sitios de unión **exón–exón**, el **uso de memoria RAM** y el manejo de [[Multimapping|multimappings]].

**Cambio de foco: solo queremos *contar*.** No importa dónde mapea la lectura dentro del gen ni qué *mismatch* tiene; solo importa **a qué gen corresponde**. De ahí el [[Pseudoalineamiento]]: alineamiento directo al [[Transcriptoma]], buscando **compatibilidad** en lugar de coordenadas exactas.

El benchmark de la clase (20 datasets de 30 M de lecturas, 20 cores; tiempo de alineamiento + cuantificación):

| Pipeline | Tiempo aproximado |
|---|---|
| TopHat2 + Cufflinks | ~2.500 min |
| Bowtie2 + RSEM | ~2.300 min |
| Bowtie2 + eXpress | ~1.350 min |
| Bowtie2 + EMSAR | ~1.250 min |
| HISAT + Cufflinks | ~1.200 min |
| Sailfish | ~100 min |
| **Kallisto** | **unos pocos minutos** |

> [!quote] En la clase
> Herramientas de pseudoalineamiento como **Kallisto** y **Salmon** mapean directo al transcriptoma usando **grafos de De Bruijn** y reducen el cómputo "de días a minutos".

### La matriz de conteo single cell

El segundo producto es la [[Matriz de conteo]]:

| | Dimensiones |
|---|---|
| [[Bulk RNA-seq]] | ~10.000 genes × [6–10] condiciones |
| [[scRNA-seq]] | ~20.000 genes × [10³–10⁶] **células** |

```
          Cell 1   Cell 2   Cell 3
Gene A      12        8       15
Gene B       0        5        0
Gene C       0        2        1
```

Nótese la cantidad de ceros: la [[Sparsity]].

> [!tip] Para profundizar
> [[Slovin et al 2021 - scRNA-seq analysis a step-by-step overview|Slovin et al. (2021)]] detalla la química de gotas (carga de Poisson, eficiencias de Drop-seq/inDrop/Chromium) y el paso lecturas → matriz con CellRanger/STARsolo.

---

## 4. ¿Qué sigue? El pipeline de análisis

La diapositiva *"¿Qué sigue?"* resume el flujo completo:

```
Secuenciación y alineamiento → Cuantificación (matriz barcodes × genes)
→ Filtrado de células → Normalización de conteos → Selección de features (HVG)
→ Reducción dimensional (PCs) → Visualización y clustering
→ Downstream: pseudotiempo · RNA velocity · marcadores de poblaciones
```

### Control de calidad y filtrado de células

El [[Control de calidad en scRNA-seq]] se apoya en tres métricas por célula, que la clase muestra como curvas de densidad con un umbral vertical:

| Métrica | Umbral en el ejemplo | Qué detecta |
|---|---|---|
| **Número de [[UMI\|UMIs]] por célula** | ~500 | Muy bajo = **gota vacía**; muy alto = **doblete/multiplete** |
| **Número de genes por célula** | ~300 | Complejidad de la biblioteca |
| **Fracción de [[Genes mitocondriales]]** | ~0,2 | Células **apoptóticas** o dañadas |

En el esquema del pipeline, el filtrado separa **célula vs gota vacía** (por nº de UMIs y FDR), **no apoptóticas vs apoptóticas** (% de lecturas mitocondriales) y **singletes vs multipletes**.

### Normalización y selección de features

- **Normalización**: hacer comparables células con distinta profundidad (factor de escala por célula).
- **Selección de [[Genes altamente variables|genes altamente variables (HVG)]]**: quedarse con los genes cuya dispersión supera lo esperado para su expresión media.

### Reducción dimensional y clustering

La figura en seis pasos:

1. Matriz de 26.000 genes × 66.000 células.
2. Cada célula es un punto en un espacio de **26.000 dimensiones**.
3. **Selección de features** + [[PCA]] → matriz de 50 PCs × células.
4. Espacio de ~50 dimensiones.
5. **[[Clustering]] en el espacio de PCs** por vecinos más cercanos (grafo k-NN, *k* = 3 en el dibujo).
6. [[t-SNE]] / [[UMAP]] **solo para visualizar** (aproximan la organización del espacio de PCs).

Ver [[Reducción dimensional]].

### Identificación de tipos celulares

El clúster es una entidad estadística; ponerle nombre es la [[Anotación de tipos celulares]]:

| Estrategias manuales | Estrategias automatizadas |
|---|---|
| [[Expresión diferencial]] entre clusters | Correlación con un dataset previo (referencia) |
| Análisis en base a literatura (marcadores) | [[Machine Learning]] entrenado con múltiples datasets previos |

La clase muestra la escala del problema con un atlas de **27 millones de células** de órganos humanos (sangre 8,8 M, cerebro 2,8 M, pulmón 2,2 M, intestino 2,2 M…) y una **jerarquía armonizada de tipos celulares en 8 niveles**, desde *célula inmune* → mieloide / linfoide → T/NK → T → CD4 / CD8 → … hasta subtipos como *GZMK⁺IL7R⁺ CD8 T cell* en el nivel 8.

### Análisis downstream

- **[[Expresión diferencial]]**: entre clusters o entre condiciones (sano vs enfermo), visualizada como *heatmap* células × genes y *volcano plot*. Con la estrategia de [[Pseudobulk]] para no inflar la significancia tratando células como réplicas.
- **[[Pseudotiempo]] o trayectorias**: ordenar las células a lo largo de una trayectoria de desarrollo o diferenciación según cambios de expresión. La figura: (A) en el tiempo físico las células cambian; (B) al capturarlas se **pierde la información temporal**; (C) la estimación de pseudotiempo produce un **"orden inferido estadísticamente"**; (D) se identifican genes que cambian a lo largo del pseudotiempo. El ejemplo real es un [[UMAP]] coloreado por pseudotiempo (0 → 40) con una trayectoria ramificada.
- **[[RNA velocity]]**: aparece en el esquema del pipeline como análisis downstream (dirección del cambio de cada célula).

> [!quote] En la clase — herramientas y rigor
> - **Pseudobulk** colapsa los datos por **donante** para tener rigor estadístico (evitar N = 1).
> - La tasa de captura es baja: **500–3.000 genes por célula**.

> [!tip] Para profundizar
> [[Slovin et al 2021 - scRNA-seq analysis a step-by-step overview|Slovin et al. (2021)]] es el manual de este pipeline paso por paso (umbrales, EmptyDrops, HVG, elbow plot, Louvain, Wilcoxon) comparando Seurat, Scanpy, Monocle y gf-icf → ver [[Seurat y Scanpy]].

---

## 5. Más allá del transcriptoma: ómicas single-cell

*¿Cómo medir cada nivel regulatorio en células únicas?* El esquema de partida: **genoma, epigenoma, transcriptoma y proteoma** interactúan entre sí y con el **ambiente** para producir el **fenotipo**.

| Nivel regulatorio | Técnica single-cell |
|---|---|
| Accesibilidad de la [[Cromatina]] | [[scATAC-seq]] |
| Eventos traduccionales | [[scRibo-seq]] |
| Proteínas | [[Proteómica de célula única]] |

### [[scATAC-seq]]

*Assay for Transposase-Accessible Chromatin*. La **transposasa Tn5** corta e inserta adaptadores **solo en la cromatina abierta** (entre nucleosomas); la cerrada queda protegida. Workflow en seis pasos:

1. Aislamiento de núcleos (disociación + permeabilización)
2. **Tagmentación** con Tn5
3. Encapsulación de núcleos con beads con barcode en gotas de nanolitros
4. Amplificación por PCR (adaptadores e índices)
5. Secuenciación
6. Análisis: alineamiento, *peak calling*, clustering → tipos celulares y elementos regulatorios

### [[scRibo-seq]]

*Ribosome profiling*: una nucleasa digiere el ARNm salvo los fragmentos **protegidos por ribosomas** (*footprints*), que indican qué se está traduciendo. En single cell:

1. FACS y lisis en placas
2. Digestión con MNasa → se liberan los footprints
3. Biblioteca de ARN pequeño (ligaciones 3' y 5' con UMI, ADNc, PCR con **barcode de célula y de placa**)
4. Selección por tamaño (insertos de **~35 nt**)

Todo en **micro volúmenes (~50 nL)**. Alternativa: **Ribo-STAMP** — una proteína de unión al ARN fusionada a la enzima **APOBEC1** edita **C→U** el ARN al que se une; un RNA-seq normal + cuantificación de ediciones (SAILOR) revela genes blanco y sitios de unión.

### [[Proteómica de célula única]]

Desafíos propios:

- **No podemos amplificar** (no hay PCR para proteínas)
- **Rango dinámico muy amplio**
- **Adsorción en superficies** (las proteínas se pegan a las paredes)

Workflow: (1) aislamiento de células, (2) lisis y desnaturalización, (3) digestión a péptidos, (4) marcado, (5) espectrometría de masa, (6) análisis de espectros.

> [!quote] En la clase
> - La proteómica de célula única se aborda con **espectrómetros de masa de ultra-alta sensibilidad**.
> - Ya existe **multi-ómica en la misma célula** (*Dual-Seq*): accesibilidad de cromatina + ARNm simultáneos, que permite estudiar regulación.
> - **10x Genomics vs [[Smart-seq]]**: 10x captura >10.000 células pero solo el extremo 3' (1.000–4.000 genes/célula); Smart-seq procesa <1.000 células en placas pero lee el **transcripto completo** (>5.000 genes/célula).
> - En **Uruguay** hay capacidad instalada para ambas: Smart-seq (solo requiere *cell sorting*, disponible en el [[IIBCE]]) y 10x Genomics (en el [[Institut Pasteur de Montevideo]]), además de servidores con alta RAM para analizar en R y Python.

> [!tip] Para profundizar
> [[Stuart and Satija 2019 - Integrative single-cell analysis|Stuart & Satija (2019)]] ordena todas las técnicas multimodales (CITE-seq, G&T-seq, linaje con CRISPR, RNA velocity) y cómo se integran.

---

## 6. Desafíos bioinformáticos

| Desafío | En qué consiste |
|---|---|
| [[Sparsity]] | Gran cantidad de ceros en la matriz |
| Ruido + [[Batch effect]] | Variabilidad técnica y biológica + diferentes experimentos/plataformas |
| [[Alta dimensionalidad]] | Pasar de 10k–20k genes a 2–3 dimensiones |
| [[Identidad celular]] | ¿Cómo definir a una célula y cómo nombrarla? |
| [[Integración de datos multiómicos]] | scATAC-seq + scRNA-seq + scRibo-seq + scProteomics |

> 🎯 **Aproximaciones de [[Machine Learning]], [[Deep Learning]] e [[Inteligencia Artificial|IA]] pueden aportar soluciones** — conexión directa con el [[Módulo 3 - MOC|Módulo 3]].

> [!tip] Para profundizar
> Corrección de batch e integración entre datasets (CCA, MNN, Harmony, LIGER): [[Stuart and Satija 2019 - Integrative single-cell analysis|Stuart & Satija (2019)]]. El caso extremo — integrar **entre especies** y la ortología: [[Shafer 2019 - Cross-species analysis of scRNAseq data|Shafer (2019)]].

---

## 7. Aplicaciones: hacia "atlas" moleculares de la vida

La figura de síntesis organiza las técnicas single-cell en tres ejes:

| Eje | Qué mide | Ejemplos |
|---|---|---|
| **Linaje** | De qué progenitor viene cada célula | scGESTALT, ScarTrace, LINNAEUS, MEMOIR |
| **Estado** | El estado molecular actual de la célula | Proteínas de superficie ([[CITE-seq]], REAP-seq, FACS) · proteína intracelular (PEA) · **posición espacial** (MERFISH, smFISH, STARmap) · metilación (scBS-seq, snmC-seq, sci-MET) · genoma (SNS, SCI-seq) · accesibilidad (scATAC-seq, sciATAC-seq, scTHS-seq, 10x) · histonas (scChIP-seq) · ARNm (Drop-seq, InDrop, Smart-seq2, MARS-seq, 10x, SPLiT-seq, sci-RNA-seq) |
| **Trayectoria** | Pseudotiempo | Monocle, Wishbone, Velocyto, Diffusion |

Grandes proyectos para comprender y describir tipos y estados celulares:

- [[Human Cell Atlas]] — al momento de la clase: **70,9 M células, 11,3 k donantes, 532 proyectos, 1 k laboratorios**, organizado en redes biológicas (tejido adiposo, mama, desarrollo, ojo, diversidad genética, intestino, corazón, sistema inmune, riñón, hígado, pulmón, musculoesquelético, sistema nervioso, oral y craneofacial, organoides, páncreas, reproducción, piel).
- [[BRAIN Initiative]] ([[BICCN]])
- [[Malaria Cell Atlas]]

El ejemplo que cierra la sección es un **atlas del cerebro humano**: 105 disecciones, **3.369.219 células**, organizadas en **31 superclusters, 461 clusters y 3.313 subclusters** (neuronas IT de capas superiores y profundas, interneuronas MGE/CGE, neuronas espinosas medianas, oligodendrocitos, astrocitos, microglía, OPCs, células vasculares, plexo coroideo…), repartidos por región (corteza, hipocampo, núcleos cerebrales, tálamo, hipotálamo, mesencéfalo, puente, cerebelo, bulbo, médula). Es la jerarquía "4 clases → docenas → >3000" del inicio de la clase, hecha realidad. Ver [[Atlas celulares]].

> [!quote] En la clase
> Estos repositorios públicos permiten formular y responder preguntas **reanalizando datos existentes**, sin generar muestras nuevas.

---

## Perspectivas

Las tres preguntas con las que cierra la clase:

1. **¿Cómo definimos molecularmente a una célula?**
2. **¿Podemos predecir el estado de una célula en base a su caracterización molecular?**
3. **¿Podemos intervenir/modificar el estado de una célula?**

> [!quote] En la clase
> La tercera se planteó en clave clínica: ¿cómo intervenir terapéuticamente sobre **subpoblaciones específicas** para revertir patologías?

---

## Ideas para retener

- El bulk mide **promedios**; el single cell mide **distribuciones**. Toda la potencia analítica viene de ese cambio.
- No medimos expresión: medimos **abundancia de moléculas muestreadas**. El diseño experimental y el QC se derivan de asumir eso.
- [[Barcode celular]] responde *"¿de qué célula?"*; [[UMI]] responde *"¿molécula nueva o copia de PCR?"*. Son preguntas distintas y necesitan etiquetas distintas.
- Una célula tiene ~0,1 pg de ARNm: sin PCR no hay señal, y sin UMI la PCR distorsiona.
- Para contar no hace falta alinear: el [[Pseudoalineamiento]] cambió el cuello de botella de días a minutos.
- [[t-SNE]] y [[UMAP]] son para mirar; el clustering se hace en el espacio de PCs.
- El cuello de botella del campo se corrió de lo experimental a lo computacional: hoy el límite está en **almacenar, integrar e interpretar**.

## Lecturas de la clase

| Lectura | Qué aporta |
|---|---|
| [[Slovin et al 2021 - scRNA-seq analysis a step-by-step overview]] | El pipeline de la sección 4, paso por paso y con umbrales |
| [[Stuart and Satija 2019 - Integrative single-cell analysis]] | Multiómica en la misma célula e integración de datasets, espacio y linaje |
| [[Shafer 2019 - Cross-species analysis of scRNAseq data]] | Comparar tipos celulares entre especies: ortología, batch y evolución |

## Conexiones

- Continúa en → [[Biología espacial - mapeando la expresión génica a su entorno]] (qué se pierde al disociar el tejido)
- Índice → [[Módulo 1 - MOC]]
