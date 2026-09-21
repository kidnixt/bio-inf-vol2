---
tags: [lectura, modulo-1, spatial, imagen, segmentacion]
area: Lecturas
tipo: review
autores: Wenhao Li, Yuan Zhou
año: 2026
revista: Biology (MDPI) 15(12), 900
doi: 10.3390/biology15120900
aliases: [Li y Zhou 2026, Li & Zhou 2026, "Imaging-Based Spatial Transcriptomics: Data Interpretation Methods and Biomedical Applications"]
---

# Li & Zhou (2026) — *Imaging-Based Spatial Transcriptomics: Data Interpretation Methods and Biomedical Applications*

> [!info] Ficha de la lectura
> **Tipo:** review — *Biology* (MDPI), acceso abierto
> **Autores:** Wenhao Li y Yuan Zhou (Departamento de Informática Biomédica, Universidad de Pekín)
> **Clase asociada:** [[Biología espacial - mapeando la expresión génica a su entorno]] (clase 2)
> **PDF:** [[Li and Zhou 2026 - Imaging-based Spatial transcriptomics.pdf]]

## En una frase

En la transcriptómica espacial **basada en imagen**, la computación no es un paso "posterior": cada decisión de procesamiento —desde corregir la iluminación hasta asignar transcriptos a células— puede fabricar o borrar biología, y los errores **se propagan** hasta las conclusiones sobre nichos e interacciones.

## Por qué leerla después de la clase

La clase lista los desafíos técnicos de los [[Métodos basados en sondas]] —[[Optical crowding]], [[Photobleaching]], [[Autofluorescencia]], [[Stage drift]]— y marca la [[Segmentación celular]] con cuatro ⚠️. Este paper es la versión detallada de esas diapositivas: explica de dónde sale cada problema, qué estrategias experimentales y computacionales lo mitigan, y por qué todos terminan en la misma pregunta de incertidumbre. Es la lectura más reciente (2026) del bloque.

---

## 1. Cómo evolucionó la tecnología

| Etapa | Idea clave | Técnicas |
|---|---|---|
| **[[FISH y smFISH\|smFISH]]** | Varias sondas fluorescentes sobre el mismo ARN → cada molécula es un punto limitado por difracción. Cuantitativo y sin amplificación, pero pocos genes a la vez | smFISH |
| **Hibridación secuencial** | La identidad del gen se lee como un **código de colores a lo largo de varias rondas**: capacidad teórica **F^N** (F fluoróforos, N rondas) | seqFISH |
| **Códigos con corrección de errores** | *Codebooks* con distancia de Hamming mínima: un bit perdido no cambia el gen asignado | **[[MERFISH]]** (base del diseño de sondas de [[CosMx SMI]]) |
| **Amplificación in situ** | Sondas *padlock* + amplificación por círculo rodante (RCA) → "rolonies" más brillantes, compatibles con tejidos gruesos | STARmap, ExSeq, HybISS, **[[Xenium]]**, RAEFISH, PRISM |
| **Especímenes complejos** | Tejido grueso (MERFISH 3D hasta ~200 µm; Deep-STARmap 60–200 µm), ARN + proteína, muestras de patología **FFPE** | STARmap PLUS, CosMx/SMI, Xenium |

> [!note] El código binario de CosMx de la clase
> La diapositiva donde cada gen tiene un barcode de 16 posiciones y cada ronda "enciende" o "apaga" un punto es exactamente este esquema de hibridación secuencial con codebook.

## 2. El problema del *optical crowding* y tres salidas

Cada ARN se ve como un punto del tamaño de la función de dispersión del microscopio (resolución lateral ≈ 0,61 λ / NA). Si hay demasiados transcriptos juntos, los puntos se superponen y el decodificado falla. Además, en ensayos de muchas rondas el **photobleaching**, la remoción incompleta de sondas y la caída de señal por ciclo generan **bits perdidos**. Tres estrategias:

1. **Expandir el espacio físico** — anclar el ARN en un gel que se hincha (ExFISH, MERFISH con expansión, ExSeq, EASI-FISH).
2. **Diluir el espacio de códigos** — repartir transcriptos en muchos pseudocolores para ver menos a la vez (seqFISH+).
3. **Limitar la multiplexación** — pocos genes por ciclo, sin barcodes combinatorios (osmFISH): más robusto, menos genes.

## 3. De la imagen a la molécula (preprocesamiento)

| Paso | Qué resuelve | Riesgo si se hace mal |
|---|---|---|
| **Preprocesamiento y QC** | Iluminación despareja, fondo, [[Autofluorescencia]], foco | Sobrecorregir borra moléculas débiles; el fondo residual crea falsos positivos |
| **Volumen de datos** | Cientos de GB a TB por muestra → formatos por bloques y multiescala (**OME-Zarr / OME-NGFF**, **[[SpatialData]]**) | Comprimir o submuestrear puede perder transcriptos poco abundantes → [[Almacenamiento y visualización]] |
| **Registro entre rondas** | Corregir el desplazamiento entre ciclos y canales con marcadores fiduciales ([[Stage drift]]) | Una desalineación mínima **mezcla señales de moléculas distintas en un mismo barcode** |
| **Restauración** (deconvolución y denoising) | Separar puntos superpuestos (Richardson–Lucy, Deconwolf, CARE) | Las redes neuronales pueden "alucinar" puntos que no existen |
| **Detección de puntos** | Convertir la imagen en una nube de moléculas candidatas (LoG, RS-FISH, Spotiflow, deepBlink) | Puntos perdidos = falsos negativos; puntos fusionados distorsionan la abundancia |
| **Decodificado y *molecule calling*** | Traducir la traza de varias rondas a un gen del codebook | Los **barcodes vacíos** (*blank codes*) sirven como control de la tasa de error |

## 4. De la molécula al tejido (interpretación)

### Segmentación y asignación de transcriptos

Es el cuello de botella de la resolución celular — el ⚠️⚠️ de la clase.

- Los primeros métodos (tinción nuclear, *watershed*) fallan en tejido denso y en células de morfología compleja (**neuronas**, infiltrados inmunes).
- Cambio de paradigma: usar la **posición de los transcriptos**, no solo la morfología. **pciSeq** (asignación probabilística a partir de núcleos), **Baysor** (células como distribuciones moleculares coherentes, con o sin tinción), Proseg, CelloType, Bering.
- Corrección posterior de la matriz: FastReseg (dobletes espaciales), resolVI y DenoIST (modelan la contaminación por difusión desde células vecinas).
- La matriz célula × gen debe tratarse como una **estimación con incertidumbre**, no como una medida exacta.

### Análisis sin segmentación

Resumir la composición molecular de vecindarios locales (los *neighborhood composition vectors* de Baysor, **FICTURE**) permite encontrar dominios y nichos aun cuando los bordes celulares son dudosos.

### Tipado celular con referencia

De marcadores manuales a **transferencia de etiquetas desde un atlas de [[scRNA-seq]]** (CCA + k-NN en el atlas de cerebro completo con MERFISH; Harmony en el atlas STARmap PLUS de sistema nervioso). El panel dirigido pasa a ser un "ancla" hacia el transcriptoma completo — pero hereda los sesgos de la referencia → ver [[Integración de datos single cell y spatial]] y [[Anotación de tipos celulares]].

### Dominios, gradientes e interacciones

- [[Spatial domains]]: modelos de campo aleatorio de Markov (seqFISH+), registro a un marco de coordenadas común (Allen CCF) en los atlas de cerebro; la organización del tejido suele ser **continua (gradientes)**, no solo regiones discretas.
- [[Comunicación célula-célula|Interacciones]] y [[Spatial niches]]: de la proximidad par a par a modelos de orden superior (CellNEST) y *foundation models* (Nicheformer). Limitación práctica: los pares ligando–receptor muchas veces **no están en el panel**.

## 5. Aplicaciones

- **Localización subcelular del ARN** como fenotipo en sí mismo: transcriptos enriquecidos en núcleo o retículo, en protrusiones, en espinas dendríticas (MERFISH, seqFISH+, ExSeq).
- **Organización tisular y atlas**: capas corticales, gradientes, atlas de cerebro de ratón completo → [[Atlas celulares]].
- **Microambientes de enfermedad y patología**: CosMx/SMI en muestras FFPE de tumores; **STARmap PLUS** mapeó estados transcripcionales junto a placas de β-amiloide y tau en un modelo de Alzheimer — "capas" de nicho alrededor de la lesión, el mismo tipo de hallazgo que muestra la clase con los nichos gliales alrededor de las placas.

## 6. Mensaje final

El desafío ya no es medir **más genes**, sino interpretar con **fidelidad**: pasar de decisiones duras (esta molécula es de este gen, este transcripto es de esta célula) a **representaciones probabilísticas** que arrastren la confianza hasta el análisis final. Los autores lo describen como un campo de **co-diseño experimento–algoritmo**.

## Conceptos del vault

[[Transcriptómica espacial]] · [[Métodos basados en sondas]] · [[FISH y smFISH]] · [[MERFISH]] · [[Xenium]] · [[SpatialData]] · [[Comunicación célula-célula]] · [[CosMx SMI]] · [[GeoMx DSP]] · [[Vizgen]] · [[Optical crowding]] · [[Photobleaching]] · [[Autofluorescencia]] · [[Stage drift]] · [[Segmentación celular]] · [[Integración de datos single cell y spatial]] · [[Anotación de tipos celulares]] · [[Spatial domains]] · [[Spatial niches]] · [[Atlas celulares]] · [[Almacenamiento y visualización]] · [[Deep Learning]]

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
- [[Módulo 1 - MOC]]
