---
tags: [lectura, modulo-1, spatial, single-cell, integracion]
area: Lecturas
tipo: review
autores: Sophia K. Longo, Margaret G. Guo, Andrew L. Ji, Paul A. Khavari
año: 2021
revista: Nature Reviews Genetics 22, 627–644
doi: 10.1038/s41576-021-00370-8
aliases: [Longo 2021, Longo et al. 2021, Integrating single-cell and spatial transcriptomics to elucidate intercellular tissue dynamics]
---

# Longo et al. (2021) — *Integrating single-cell and spatial transcriptomics to elucidate intercellular tissue dynamics*

> [!info] Ficha de la lectura
> **Tipo:** review — *Nature Reviews Genetics*
> **Autores:** Longo, Guo, Ji y Khavari
> **Clase asociada:** [[Biología espacial - mapeando la expresión génica a su entorno]] (clase 2)
> **PDF:** [[Longo et al 2021 - Integrating single-cell and spatial transcriptomics.pdf]]

## En una frase

Ninguna técnica espacial tiene todavía la **profundidad** del [[scRNA-seq]] con **resolución de célula única**, así que hay que combinar ambos mundos: el scRNA-seq define *qué* tipos celulares hay, el dato espacial dice *dónde* están, y juntos permiten inferir *quién le habla a quién*.

## Por qué leerla después de la clase

Es el desarrollo completo del desafío [[Integración de datos single cell y spatial]] que la clase menciona en una diapositiva (la figura de *cluster-based mapping* de la clase es la **Fig. 4f** de este paper). También da el marco para entender por qué el trade-off *genes × células × resolución × throughput* obliga a integrar.

---

## 1. Por qué integrar

- La disociación del scRNA-seq **borra la posición** y además puede **inducir expresión ectópica** (respuesta de estrés) → subtipos artificiales.
- Las señales **yuxtacrinas y paracrinas** actúan entre **0 y 200 µm**: sin posición no se puede estudiar la comunicación intercelular real.
- Las técnicas espaciales tienen el problema inverso:

| Familia (nombre en el paper) | Equivale en el vault a | Fortaleza | Debilidad |
|---|---|---|---|
| **HPRI** — *high-plex RNA imaging* (ISS, MERFISH, seqFISH, STARmap…) | [[Métodos basados en sondas]] | Resolución de célula única, buena sensibilidad por gen | Panel de genes preseleccionado (típicamente 100–200 en tejido intacto) |
| **Spatial barcoding** (Spatial Transcriptomics / [[Visium]], Slide-seq, HDST…) | [[Métodos basados en secuenciación]] | Transcriptoma completo, sin sesgo de panel, comercial y accesible | Profundidad baja; cada spot mezcla células (en Visium, 55 µm ≈ **3–30 células**) |

Referencia: scRNA-seq mide del orden de 10⁴–10⁶ lecturas por célula.

## 2. Qué se aprendió integrando (ejemplos)

| Contexto | Hallazgo |
|---|---|
| **Homeostasis** — hígado | Asignar cada célula a **9 zonas** del lobulillo (no solo periportal/pericentral) → clase nueva de hepatocitos intermedios |
| **Homeostasis** — intestino | Tres regiones funcionales a lo largo de la vellosidad, sin genes *landmark* previos |
| **Homeostasis** — médula ósea | [[Microdisección por captura láser\|LCM]] guiada por inmunotinción + bulk RNA-seq + deconvolución con scRNA-seq → nichos no descritos |
| **Desarrollo** — corazón e intestino embrionarios | Mapas en varios tiempos; en corazón, scRNA-seq + barcoding sirvieron para elegir el panel de HPRI → mapa 3D a resolución celular |
| **Tumor** — carcinoma escamoso | Subpoblación de queratinocitos **inmunosupresora** ubicada en un nicho fibrovascular del borde tumoral |
| **Tumor** — melanoma | Mayor heterogeneidad en la zona de transición → peor sobrevida |
| **Alzheimer** | Microglía asociada a enfermedad localizada **junto a las placas amiloides**; redes génicas cercanas a placas como blancos terapéuticos (el mismo ejemplo de [[Spatial niches\|nichos]] de la clase) |
| **ELA** (médula espinal) | 31 módulos de co-expresión seguidos en el tiempo |
| **Infarto** | snRNA-seq + [[scATAC-seq]] + barcoding → redes regulatorias de la diferenciación a miofibroblasto en la zona de borde |

## 3. El flujo propuesto: las "cuatro A"

1. **Adopt** — definir la pregunta (homeostasis, desarrollo, microambiente de enfermedad o tumoral).
2. **Assay** — scRNA-seq para definir subpoblaciones + técnica espacial para ubicarlas; el scRNA-seq, el barcoding y los [[Genes espacialmente variables]] ayudan a **elegir el panel** de HPRI.
3. **Assemble** — construir mapas de tipos celulares: **deconvolución** para spots, **mapeo** para células individuales; anotar la histología (p. ej., el borde del tumor).
4. **Analyse** — nichos, vecindarios e interacciones ligando–receptor.

## 4. Deconvolución vs mapeo

### [[Deconvolución espacial|Deconvolución]] — para spots que mezclan células

Primero se definen los tipos con scRNA-seq; después se estima qué hay en cada spot:

- **Regresión**: mínimos cuadrados no negativos (**SPOTlight**), mínimos cuadrados ponderados amortiguados (**SpatialDWLS**).
- **Bayesiana**: ajustar una binomial negativa (o Poisson) por gen y tipo celular, y estimar la composición del spot por máximo a posteriori (**RCTD** — *robust cell-type decomposition* — con "modo doblete": ¿lo explica mejor uno o dos tipos celulares?).
- **Scores de enriquecimiento**: puntuar cada spot por un set de genes (Seurat) o intersecar programas (*multimodal intersection analysis*). Sirve también para puntuar ciclo celular, tumor/no tumor, etc.
- **Validación**: mezclas *in silico* de células conocidas; SPOTlight es el benchmark más completo.

### Mapeo — para datos de resolución celular (HPRI)

Asignar a cada célula espacial un tipo del scRNA-seq e **imputar** los genes que el panel no midió:

- Primeros métodos: pocos genes *landmark* por ISH → solo en tejidos de estructura prototípica.
- Una evaluación de 14 algoritmos encontró que los mejores para scRNA-seq + datos espaciales de célula única son **LIGER**, **Seurat Integration** (CCA + anclas MNN) y **Harmony**. Harmony y Seurat suponen que toda diferencia entre datasets es técnica; LIGER separa factores compartidos y específicos, y es más robusto al *mismatch*.
- **pciSeq**: modelo bayesiano que asigna cada lectura a una célula y cada célula a un tipo.

### El problema del *mismatch*

Los tipos del scRNA-seq y del dato espacial no siempre coinciden: la disociación puede **crear** subtipos (estrés) o **perder** tipos que no sobreviven al protocolo; el muestreo de secciones distintas agrega sesgo. Los modelos de deconvolución tratan al scRNA-seq como verdad y consideran ruido a un tipo que solo aparece en el espacio — por eso conviene también **clusterizar los spots** directamente.

## 5. [[Comunicación célula-célula|Comunicación intercelular]] con contexto espacial

Los algoritmos clásicos predicen pares ligando–receptor solo con scRNA-seq y una base de datos de interacciones. El espacio permite **descartar** interacciones entre células demasiado lejanas y fijar rangos:

- Modelos lineales generalizados: ¿co-localizan ligando y receptor en el mismo spot o en spots adyacentes?
- **Giotto**: probabilidad de uso de una interacción según la proximidad de las células que la expresan.
- **SpaOTsc**: transporte óptimo; estima el **rango máximo** de señalización a partir de la expresión de genes blanco río abajo.
- **novoSpaRc**, **CSOmap**: reconstruyen un "tejido virtual" desde scRNA-seq.
- Validación experimental: PIC-seq (dobletes de células que interactúan), LIPSTIC.

> [!warning] Conexión con la clase
> Esto es exactamente lo que la [[Lateral diffusion]] pone en riesgo: si los transcriptos se corren a spots vecinos, aparecen **falsas interacciones célula-célula** — la consecuencia que muestra la diapositiva de la clase.

## 6. Hacia dónde va

- **Deep learning sobre la histología**: ST-Net predice expresión de 102 genes por spot desde la imagen H&E; XFuse lleva barcoding + histología a resolución celular → [[Deep Learning]].
- **3D**: STARmap y ExSeq fijan el tejido en un hidrogel; ExSeq usa microscopía de expansión para resolver transcriptos densos (el problema del [[Optical crowding]]).
- **Tiempo real**: el dato espacial es una foto; rastrear células vivas (tomografía, PET) sería el complemento.
- A medida que el barcoding llegue a resolución subcelular, la **deconvolución se convertirá en un problema de mapeo**.

## Conceptos del vault

[[Transcriptómica espacial]] · [[Integración de datos single cell y spatial]] · [[Deconvolución espacial]] · [[Comunicación célula-célula]] · [[Genes espacialmente variables]] · [[FISH y smFISH]] · [[MERFISH]] · [[scRNA-seq]] · [[Métodos basados en sondas]] · [[Métodos basados en secuenciación]] · [[Visium]] · [[GeoMx DSP]] · [[Barcode espacial]] · [[Spatial niches]] · [[Neighborhoods]] · [[Lateral diffusion]] · [[Segmentación celular]] · [[Batch effect]] · [[Microdisección por captura láser]] · [[Deep Learning]]

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
- [[Módulo 1 - MOC]]
