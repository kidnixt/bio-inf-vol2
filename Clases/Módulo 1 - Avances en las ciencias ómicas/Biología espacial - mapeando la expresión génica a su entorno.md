---
titulo: "Biología espacial: mapeando la expresión génica a su entorno"
curso: Fronteras y Perspectivas en Bioinformática – Universidad ORT
modulo: Módulo 1 - Avances en las ciencias ómicas
clase: 2
docente: Guillermo Eastman
año: 2026
tags:
  - clase
  - modulo-1
  - spatial
  - omicas
---

# Biología espacial: mapeando la expresión génica a su entorno

> [!info] Ficha de la clase
> **Curso:** Fronteras y Perspectivas en Bioinformática – Universidad ORT (2026) · **Clase 2**
> **Módulo:** [[Módulo 1 - MOC|Módulo 1 - Avances en las ciencias ómicas]]
> **Docente:** [[Guillermo Eastman]] — Departamento de Genómica, [[IIBCE]]
> **Diapositivas:** [[Diapositivas - Biología espacial - mapeando la expresión génica a su entorno.pdf]]
> **Resumen de la clase:** no hay resumen del curso para esta clase.
> **Lecturas:** [[Longo et al 2021 - Integrating single-cell and spatial transcriptomics|Longo et al. 2021]] · [[Yue et al 2023 - A guidebook of spatial transcriptomics technologies|Yue et al. 2023]] · [[Li and Zhou 2026 - Imaging-based Spatial transcriptomics|Li & Zhou 2026]]
> **Clase previa:** [[Aproximaciones ómicas con resolución de célula única]] · **Clase siguiente:** [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]

> [!abstract] Cómo leer este resumen
> Sigue la estructura de las diapositivas y describe lo que muestran las figuras (esquemas de plataformas, químicas, desafíos). Al final de cada bloque se indica qué **lectura** lo profundiza.

---

## La pregunta que abre la clase

La clase arranca retomando la anterior con una figura doble: el **análisis bulk** (células mezcladas → expresión promedio → sin información de heterogeneidad) frente al **análisis single cell** (células aisladas → expresión por célula → heterogeneidad y subpoblaciones). El [[scRNA-seq]] responde:

> **¿Qué genes está expresando cada célula individualmente?**

Es decir, mide la [[Expresión génica|expresión génica]] de cada célula. Pero deja otra pregunta sin responder:

> **¿Dónde está cada célula en el tejido? ¿Qué otras células tiene alrededor?**

La analogía de las frutas de la clase 1 se completa con un tercer paso:

| Aproximación | Desde | Analogía | Qué obtenemos |
|---|---|---|---|
| [[Bulk RNA-seq\|Bulk genomics]] | 2006 | Licuado | **Promedios** |
| [[scRNA-seq\|Single cell genomics]] | 2012 | Ensalada de frutas | **Distribuciones** |
| [[Transcriptómica espacial\|High-plex spatial biology]] | 2019 → futuro | **Tarta de frutas**: cada fruta en su lugar | **Contexto** |

## Objetivos de la clase

1. ¿Por qué necesitamos resolución espacial?
2. ¿Cómo se generan estos datos?
3. ¿Qué tipo de preguntas biológicas podemos responder?
4. ¿Qué desafíos bioinformáticos aparecen?

## Contenido

- ¡La arquitectura del tejido importa!
- Plataformas disponibles para hacer [[Transcriptómica espacial|Spatial transcriptomics]]
- ¿Cómo funcionan las distintas aproximaciones?
- Desafíos bioinformáticos
- Aplicaciones biológicas

---

## 1. ¿Qué perdemos cuando disociamos un tejido?

```
Tejido → disociación → células → scRNA-seq → UMAP
   ▲___________________ ? ___________________│
```

La flecha de vuelta con un signo de pregunta es la idea central: **desde el UMAP no se puede volver al tejido.**

| 👍 Lo que el single cell conserva | 👎 Lo que la disociación destruye |
|---|---|
| Resolución celular | **Posición** |
| [[Heterogeneidad celular\|Heterogeneidad]] | **Arquitectura** |
| [[Estado celular\|Estados celulares]] | **Vecinos** |
| Perfiles transcriptómicos individuales | **Estructura tisular** |
| | **Relaciones espaciales** |

La analogía visual es un **cerebro hecho de LEGO**: el [[scRNA-seq]] desarma el cerebro y deja las piezas agrupadas por color (sabemos cuántas piezas de cada tipo hay); la [[Transcriptómica espacial]] muestra un corte del cerebro con cada pieza en su lugar.

El [[UMAP]] —una [[Reducción dimensional|reducción dimensional]]— es un espacio de **similitud transcriptómica**, no un mapa del tejido: dos células juntas en el UMAP pueden estar en extremos opuestos del órgano, y dos vecinas en el tejido pueden caer en clusters distintos.

### La arquitectura del tejido importa

Dos ejemplos:

- **Cortes de cerebro de ratón a los 3, 6, 12 y 18 meses** (modelo de enfermedad de Alzheimer; Chen & Lu, Fiers & De Strooper, *Cell* 2020): la patología avanza en regiones concretas del tejido, y lo que importa no es solo *qué* células cambian sino *dónde*.
- La **heterogeneidad espacial de un tumor**: células del microambiente en la periferia y subclones tumorales en el centro.

La función de una célula depende de **con quién está**: una [[Microglía]] reactiva pegada a una placa amiloide y una microglía reactiva en tejido sano pueden tener perfiles parecidos y significar cosas distintas. El contexto es parte del fenotipo.

---

## 2. ¿Cómo medimos ARN en el espacio?

La figura de Chen et al. (*Cells*, 2023) divide los métodos en tres rutas:

| Ruta | Flujo | Ejemplo |
|---|---|---|
| **A) Basados en secuenciación** | Corte de tejido sobre un *array* con barcodes espaciales → biblioteca → secuenciación → análisis | [[Visium]] ([[10x Genomics]]) |
| **B) Basados en sondas** | Sondas de ARN con barcode (o sondas RNAscope / anticuerpos fluorescentes) → tinción → imagen y **selección de ROI** → corte UV y colección de barcodes por ROI → análisis | [[GeoMx DSP]] |
| **C) Basados en imagen** | Inmunotinción o hibridación de sondas → **imagen microscópica** → análisis | [[CosMx SMI]] |

La clase agrupa B y C como **métodos de hibridación de sondas**, con un compromiso opuesto al de la secuenciación:

| | [[Métodos basados en sondas]] | [[Métodos basados en secuenciación]] |
|---|---|---|
| ✅ Ventaja | **Resolución extrema** (subcelular) | **Descubrimiento molecular** (transcriptoma sin sesgo de panel) |
| ⚠️ Desafío | **Cantidad de sondas** utilizadas (panel dirigido) · **visualización** | **Resolución** |

### Cuántos estudios usan cada ruta

Del paper de [[Yue et al 2023 - A guidebook of spatial transcriptomics technologies|Yue et al. (2023)]]: las publicaciones con transcriptómica espacial crecen exponencialmente desde 2019 (~500 en 2022), con **NGS (~400)** muy por encima de **imagen (~100)**.

- **Imagen:** BOLORAMIS, CosMx SMI, EEL FISH, ExSeq, **GeoMx DSP** (la más usada), HybISS, ISS, [[MERFISH]], seqFISH+, split-FISH, STARmap, [[Xenium]].
- **NGS:** DBiT-seq, HDST, Seq-Scope, slide-seq, slide-seq2, ST, [[Stereo-seq]], STRP-seq, Tomo-seq, **Visium** (~330 estudios en 2022), XYZeq.

La clase marca con flechas las tres plataformas que va a detallar: **CosMx SMI, GeoMx DSP y Visium**.

### Breve historia

| Año | Hibridación (azul) | Secuenciación (rojo/naranja) | Empresa |
|---|---|---|---|
| 1980 | FISH | | |
| 1992 | [[FISH y smFISH\|smFISH]] | | |
| 2008 | | RNA-seq | |
| 2009 | | single cell RNA-seq | |
| 2012 | seqFISH | | |
| 2013 | *In situ sequencing* | | |
| 2016 | [[MERFISH]] | Ståhl et al. (*Spatial Transcriptomics*) | [[Vizgen]] |
| 2017 | | [[Visium]] | [[10x Genomics]] |
| 2019 | [[GeoMx DSP\|GeoMx]] | | [[Nanostring]] |
| **2020** | ***Method of the year*** | | |
| 2021 | | [[Stereo-seq]] | [[BGI]] |
| 2022 | [[CosMx SMI\|CosMx]], [[Xenium]] | | [[Nanostring]], [[10x Genomics]] |

En 2020 la transcriptómica espacial fue elegida **método del año** por *Nature Methods*.

---

## 3. El trade-off central ⚖️

> **Número de genes × Número de células × Resolución espacial × Throughput**

No se puede maximizar todo a la vez. Elegir plataforma **es** elegir qué sacrificar.

| Instrumento | # Genes | Resolución espacial | Throughput |
|---|---|---|---|
| [[GeoMx DSP\|GeoMx]] | Alto a completo | Baja – regional ([[ROI]]) | Alto |
| [[CosMx SMI\|CosMx]] | Alto a completo | Célula única y subcelular | Moderado – bajo |
| [[Visium HD]]* | Completo | Alta, cerca de célula única | Alto |

---

## 4. Las plataformas en detalle

### [[GeoMx DSP]] (Digital Spatial Profiler)

Trabaja por **[[ROI|regiones de interés]]** elegidas por el usuario sobre la imagen, no célula por célula. Tiene dos vías paralelas, **ARN** y **proteína**:

1. **Tinción** (*stain*): el tejido se marca con anticuerpos fluorescentes (para ver la morfología) y con los reactivos de medición, que llevan un **oligo fotoclivable**.
2. **Selección de ROI** sobre la imagen.
3. **Corte con luz UV** solo dentro de la ROI → se liberan los oligos.
4. **Colección y dispensado** de los oligos liberados.
5. **Conteo** (por secuenciación o nCounter).

Los reactivos:

| Reactivo | Estructura |
|---|---|
| Proteína | Anticuerpo + *linker* fotoclivable + barcode DSP |
| ARN | Sonda complementaria al ARN blanco + *linker* fotoclivable + barcode DSP |

- **Sensibilidad:** hasta **1200 proteínas**, o el **[[Transcriptoma|transcriptoma]] completo**.
- **ROI:** entre **50 y 600 µm** de diámetro → entre **50 y 500 células**.

Formas de definir ROIs: **geométricas** (círculos, cuadrados), por **segmentación** con un marcador (p. ej. PanCK para tumor), **específicas de tipo celular**, por **contorno** (bandas concéntricas desde un borde) o en **grilla**.

¿Cómo ilumina solo la ROI? Con un **chip de microespejos digitales (DMD)**, ~1 millón de espejos de 1 µm² que dirigen la luz UV. Así se pueden generar **máscaras** complementarias — p. ej. *tumor* vs *microambiente tumoral* — y medir cada compartimento por separado. Las sondas para tejido **FFPE** llevan: secuencia complementaria al exón + *linker* fotoclivable + adaptador Illumina i5 + UMI + GeoMx ID + adaptador i7.

Es la plataforma de elección cuando la pregunta es *"¿en qué se diferencian estas dos zonas?"* y no *"¿qué hace cada célula?"*.

### [[CosMx SMI]] (Spatial Molecular Imager)

Basado en imagen, con resolución de **célula única y subcelular**.

**Preparación:** tejido FFPE en portaobjetos estándar → permeabilizar, fijar, recuperar blancos → **hibridación** de sondas de ARN y anticuerpos → armado en una *flow cell* → instrumento.

**La sonda:**

- Sonda ISH con **dominio de unión al blanco (35–50 nt)** + **dominio de lectura (*readout*, 60–80 nt)**.
- Sobre el dominio de lectura se hibridan **reporteros** con muchos fluoróforos unidos por **sitios fotoclivables** (PC).
- Para proteínas: anticuerpo + *linker* sitio-específico + dominio de lectura.

**La lectura por ciclos:** set de reporteros 1 → hibridación e imagen → corte UV y lavado de fluoróforos → set 2 → … → set *n*. En cada ronda, un punto (una molécula) está **encendido o apagado** y con un color.

**El código:** cada gen tiene un **barcode de 16 posiciones** con 4 colores (p. ej. gen 1: `1100001000000001`). Tras 16 imágenes, cada punto del tejido acumula un código binario (`1100`, `0110`, `1001`, `0011`…) que se **decodifica** contra el diccionario de genes.

**Escala:** 1,4 millones de células analizadas en un corte completo de ganglio linfático FFPE (panel de 1.000 ARN), con zoom a resolución celular (100 µm) y **subcelular** (10 µm). La asignación de cada transcripto a una célula se hace con un algoritmo de **segmentación multimodal con ML**.

### [[Visium]] (secuenciación) vs [[Visium HD]] (sondas)

La comparación visual (corte de colon): Visium muestra **spots redondos** con 10 clusters; Visium HD muestra las **criptas intestinales** con 16 clusters y detalle casi histológico.

**Visium:**

- Portaobjetos con 4 áreas de captura de **6,5 mm**, cada una con **~5.000 spots** con barcode.
- Spots de **55 µm** de diámetro, separados **100 µm** (centro a centro) → cada spot mezcla varias células.
- Oligo de captura: *partial read 1* + **[[Barcode espacial|barcode espacial]]** + UMI + **poly(dT)** (captura la cola poli-A del ARNm).

**Visium HD (química de sondas):**

1. Un **par de sondas** (LHS con *Read 2S* y RHS con cola poli-A) se hibridan **adyacentes** sobre el ARNm blanco y se **ligan**.
2. Se digiere el ARN y se **libera la sonda ligada**.
3. La cola poli-A de la sonda es capturada por el oligo del portaobjetos (*Read 1* + barcode espacial + UMI + poly(dT)VN).
4. Extensión, desnaturalización y elución → biblioteca: *Read 1* – barcode espacial – UMI – poli-A – **inserto de sonda ligada** – *Read 2S*.

La superficie ya no son spots sino un **"césped continuo" de oligos** en un área de 6,5 × 6,5 mm (marco fiducial de 8 × 8 mm), con una **grilla de cuadrados de 2 × 2 µm** con barcode que se agrupan (*binning*) en **8 × 8 µm**.

> [!tip] Para profundizar
> Las cuatro familias de tecnologías (hibridación, secuenciación in situ, NGS y reconstrucción), con resoluciones y eficiencias: [[Yue et al 2023 - A guidebook of spatial transcriptomics technologies|Yue et al. (2023)]]. La lógica de los códigos binarios (MERFISH, seqFISH) y la amplificación in situ (STARmap, Xenium): [[Li and Zhou 2026 - Imaging-based Spatial transcriptomics|Li & Zhou (2026)]].

---

## 5. Desafíos bioinformáticos (y técnicos)

### En métodos de captura sobre oligos en superficie ([[Visium HD]])

**[[Lateral diffusion]]**: al permeabilizar el tejido, las moléculas de ARN **difunden** antes de ser capturadas y terminan en spots vecinos. La dispersión normal es de **~100 µm (5–10 células)**. Consecuencias que lista la figura:

- **Mapas espaciales borrosos**: los bordes nítidos se vuelven gradientes difusos.
- **Falsas interacciones célula–célula**: datos engañosos para el análisis ligando–receptor → [[Comunicación célula-célula]].
- Se pierde la **resolución de célula única**.
- **La paradoja de la permeabilización**: más sensibilidad (captura de ARN) requiere permeabilizar más, lo que aumenta la difusión → **sensibilidad vs resolución**.

### En métodos de sondas

- **[[Optical crowding]] / crosstalk**: con alta densidad de transcriptos, cada molécula se ve como un punto limitado por la difracción (**~250 nm**) y los puntos se superponen.
- **[[Photobleaching]]**: la fluorescencia se apaga con las rondas sucesivas de imagen (ilustrado con la sonda de reporteros de CosMx).
- **[[Autofluorescencia]]**: el propio tejido emite señal de fondo.
- **[[Stage drift]]**: el portaobjetos se desplaza entre rondas y las imágenes dejan de alinearse.

### ⚠️⚠️ [[Segmentación celular]] ⚠️⚠️

Decidir qué píxeles y qué transcriptos pertenecen a qué célula. La clase le dedica tres diapositivas:

1. **El pipeline:** *Z-stack* de imágenes multicanal → preprocesamiento (mejorar calidad) → **segmentación aumentada con ML** (modelos neuronales preentrenados **Cellpose**). Canales de ejemplo en hígado: DAPI (núcleos), CK8/18, CD45, CD298/B2M, PanCK. Se combinan los resultados de varios modelos; el **hígado canceroso** es mucho más difícil de segmentar que el normal.
2. **Qué sale mal:** difusión de fondo, **células superpuestas**, difusión entre células, **células sin núcleo** en el plano. Errores posibles: **falsos negativos** (transcriptos de la célula que quedan afuera), **falsos positivos** (se incluyen transcriptos ajenos), **sobre-segmentación** (una célula partida en varias) y **sub-segmentación** (varias células fusionadas).
3. **Estrategias según la tinción disponible** (nuclear, interior, borde):
   - Tinción de **borde** (no requiere núcleo; resuelve células anucleadas y multinucleadas)
   - Tinción de **interior + expansión** (requiere núcleo)
   - **Expansión nuclear** (requiere núcleo; expande ~5 µm o hasta chocar con otra célula)

Es el paso más determinante y frágil: un error se propaga a la anotación, al clustering y a cualquier conclusión sobre vecindarios.

### [[Integración de datos single cell y spatial]]

La figura de *cluster-based mapping* (el caso de datos de resolución celular; para spots que mezclan células se usa [[Deconvolución espacial|deconvolución]]): los datos de [[scRNA-seq]] (profundos, sin posición) y los espaciales (con posición, menos genes) se proyectan a un **espacio compartido** donde se agrupan por tipo celular (A, B, C) → **datos espaciales alineados con resolución de célula única**.

### *Storage and Visualization!* → [[Almacenamiento y visualización]]

La clase presenta el framework **[[SpatialData]]**: un formato de almacenamiento común (tablas, puntos, formas, etiquetas, imágenes; sobre **OME-NGFF / Zarr**), una librería de Python (datasets alineados, transformaciones —trasladar, escalar, rotar—, consultas espaciales, agregación), lectores para cada plataforma (Xenium, Visium, CosMx, IMC, CyCIF), anotación y visualización interactiva, interfaz con **PyTorch** para [[Deep Learning]] e integración con el ecosistema.

> [!tip] Para profundizar
> Todo el pipeline de imagen —registro entre rondas, restauración, decodificado de barcodes, segmentación con transcriptos (Baysor, pciSeq) y análisis sin segmentación—: [[Li and Zhou 2026 - Imaging-based Spatial transcriptomics|Li & Zhou (2026)]]. Deconvolución de spots vs mapeo de células, y comunicación célula–célula: [[Longo et al 2021 - Integrating single-cell and spatial transcriptomics|Longo et al. (2021)]].

---

## 6. Aplicaciones biológicas: ¿qué estamos aprendiendo?

### Estructura del tejido

- **[[Spatial domains]]**: regiones con un perfil transcriptómico coherente. La figura muestra cómo se obtienen: un **grafo de vecinos por expresión génica** + un **grafo de proximidad espacial** (los spots vecinos en el portaobjetos) + la **histología** (opcional) → dominios 0–6 sobre un corte de cerebro de ratón.
- **[[Neighborhoods]]**: qué tipos celulares aparecen sistemáticamente juntos.
- **[[Spatial niches]]**: microambientes funcionales definidos por la composición local. El ejemplo son las **placas amiloides** del Alzheimer:
  - Imágenes de placas rodeadas de glía reactiva (Chen & Lu, Fiers & De Strooper, *Cell* 2020).
  - El **nicho de la placa** como un círculo de **40 µm de radio** alrededor, con microglía, astrocitos, oligodendrocitos y neuronas glutamatérgicas y GABAérgicas (Mallach & Zielonka et al., *Cell Reports* 2024).
  - Agregados de **tau** en hipocampo de ratón 15 meses después de inyectar extracto cerebral con tau mutante P301S, ausentes en los controles (Goedert et al., *Brain* 2017).

### Atlas espaciales

- *"Atlas!"* — atlas espaciales en siete organismos: *Arabidopsis*, pez cebra, *Drosophila*, axolotl, ratón, mono y humano (Cheng et al., 2022).
- *"Atlas! (!!!)"* — **embriones humanos** de los estadios de Carnegie **CS12–13 a CS23**, con [[Stereo-seq]] + snRNA-seq secuenciados en DNBSEQ-Tx ([[BGI]]); mapas de ~50 órganos y tejidos en desarrollo y patrones de genes marcadores (*SHH*, *STMN2*, *PMEL*, *LMX1A*, *ALB*, *MYL7*, *MYH6*, *MYH7*) validados por imagen (Pan, J. et al., *Nature* 2026). Ver [[Atlas celulares]].

---

## Perspectivas

1. **¿Vamos hacia la construcción de un "Google Maps" de la biología?**
2. **Si podemos medir cada célula, saber dónde está y qué ocurre a su alrededor… ¿qué nos falta para entender realmente un tejido?**
3. **Estamos generando datos biológicos a una velocidad mayor de la que somos capaces de interpretarlos.**

```
datos  ──────────────────────────►  conocimiento
        almacenamiento
        visualización
        integración
```

El cuello de botella ya no es generar los datos, sino atravesar esas tres etapas. Eso conecta con el [[Módulo 2 - MOC|Módulo 2 (Biología de Sistemas)]], el [[Módulo 3 - MOC|Módulo 3]] ([[Inteligencia Artificial|IA]] aplicada) y el [[Módulo 4 - MOC|Módulo 4 (desarrollo y despliegue)]].

---

## Ideas para retener

- La disociación es **destructiva**: lo espacial se pierde ahí y no se recupera computacionalmente sin una referencia.
- El [[UMAP]] no es un mapa del tejido. Confundir proximidad transcriptómica con proximidad física es el error conceptual más común.
- Elegir plataforma es elegir en qué esquina del trade-off *genes × células × resolución × throughput* estar. La pregunta biológica define la plataforma.
- En sondas, **la identidad del gen es un código** que se lee en varias rondas de imagen; en secuenciación, **la posición es un barcode** que se lee al secuenciar.
- La [[Segmentación celular]] es el paso que más condiciona todo lo que viene después.
- La [[Lateral diffusion]] no es solo ruido: puede **inventar** interacciones entre células.

## Lecturas de la clase

| Lectura | Qué aporta |
|---|---|
| [[Longo et al 2021 - Integrating single-cell and spatial transcriptomics]] | Por qué y cómo integrar scRNA-seq con datos espaciales: deconvolución, mapeo, comunicación célula–célula |
| [[Yue et al 2023 - A guidebook of spatial transcriptomics technologies]] | Guía de 22 tecnologías, 791 datasets y 70 herramientas de análisis |
| [[Li and Zhou 2026 - Imaging-based Spatial transcriptomics]] | El pipeline computacional de los métodos de imagen y cómo se propagan los errores |

## Conexiones

- Viene de → [[Aproximaciones ómicas con resolución de célula única]]
- Continúa en → [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
- Índice → [[Módulo 1 - MOC]]
