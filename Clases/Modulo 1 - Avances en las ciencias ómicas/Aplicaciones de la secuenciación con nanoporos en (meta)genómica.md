---
titulo: "Aplicaciones de la secuenciación con nanoporos en (meta)genómica"
curso: Fronteras y Perspectivas en Bioinformática – Universidad ORT
modulo: Módulo 1 - Avances en las ciencias ómicas
docente: Cecilia Salazar
fecha: 2026-09-02
año: 2026
tags:
  - clase
  - modulo-1
  - nanoporos
  - metagenomica
  - omicas
---

# Aplicaciones de la secuenciación con nanoporos en (meta)genómica

> [!info] Ficha de la clase
> **Curso:** Fronteras y Perspectivas en Bioinformática – Universidad ORT (2026)
> **Módulo:** [[Módulo 1 - MOC|Módulo 1 - Avances en las ciencias ómicas]]
> **Docente:** [[Cecilia Salazar]] — [[Institut Pasteur de Montevideo]]
> **Fecha:** 2 de setiembre de 2026
> **PDF original:** `Modulo 1 - Avances en las ciencias ómicas/Clase020926_final_CSalazar.pdf`
> **Clase previa:** [[Biología espacial - mapeando la expresión génica a su entorno]]

## Contenido de la clase

1. Evolución de las plataformas de secuenciación.
2. Fundamentos de la [[Secuenciación con nanoporos]].
3. Generación y análisis de los datos.
4. Aplicaciones en microbiología y [[Metagenómica clínica|metagenómica]].
5. Limitaciones y oportunidades.
6. Plataformas emergentes y nuevas aplicaciones.
7. Consideraciones finales.

---

## 1. Bioinformática y tecnologías de secuenciación: una historia de coevolución

El marco con el que abre la clase es que **la bioinformática no viene después de la tecnología: evoluciona con ella**. Cada cambio de plataforma no solo produjo más datos, sino datos con otras propiedades, y eso obligó a rediseñar los métodos de análisis.

### Las tres generaciones

| Generación | Año de referencia | Plataformas | Cómo obtiene la secuencia | Longitud |
|---|---|---|---|---|
| **Primera** | 1977 | [[Secuenciación Sanger\|Sanger]], Maxam y Gilbert | Terminación de cadena con dNTPs y visualización por electroforesis | 500–1.000 pb |
| **Segunda** | 2005 | 454, Solexa / [[Illumina]], Ion Torrent | Alto rendimiento por **paralelización** de las reacciones | ~50–500 pb |
| **Tercera** | 2011 | [[PacBio]] HiFi, [[Oxford Nanopore Technologies\|Oxford Nanopore]] | **Molécula única**, tramos largos de ADN | Decenas de kb en promedio |

Las dos primeras son [[Secuenciación de segunda generación|secuenciación de lectura corta]]; la tercera es [[Secuenciación de tercera generación|secuenciación de lectura larga]].

### Cuatro formas físicamente distintas de "leer" ADN

Lo interesante de la comparación es que la señal que se mide es **de naturaleza diferente** en cada plataforma:

| Plataforma | Qué se mide |
|---|---|
| [[Secuenciación Sanger\|Sanger]] | Fluorescencia del ddNTP terminal de cada fragmento, leída en orden de tamaño |
| [[Illumina]] | Intensidad y patrón de fluorescencia de cada cluster en cada ciclo de síntesis |
| [[PacBio]] | Pulsos de fluorescencia en tiempo real asociados a cada incorporación de nucleótido |
| [[Secuenciación con nanoporos\|Oxford Nanopore]] | **Cambios en la corriente iónica** producidos por distintos [[K-mer\|k-mers]] al atravesar el nanoporo |

> Sanger: fragmentos + fluorescencia → Illumina: imágenes cíclicas de fluorescencia → PacBio: fluorescencia de molécula única en tiempo real → **Nanopore: señal eléctrica directa**

Nanopore es la única que no usa luz ni síntesis: mide directamente la molécula nativa. Esa diferencia es la que después permite leer [[Metilación del ADN|bases modificadas]] sin ningún tratamiento químico adicional.

*Logsdon, G.A. et al. (2020). https://doi.org/10.1038/s41576-020-0236-x*

### El [[Perfil de error]] asociado a las plataformas

| Plataforma | Tipo de lectura | Exactitud / calidad oficial | Error equivalente | Probabilidad de base errónea | Longitud |
|---|---|---|---|---|---|
| [[Illumina]] | short read | Q30 como benchmark; mayoría de bases ≥Q30 (~99,9%) | ≤0,1% | Q30 = 1 error cada 1.000 bases | 150–300 pb |
| [[PacBio]] HiFi | long read HiFi | 99,9% oficial; hasta 99,95% (Q33) | ~0,1% a 0,05% | 1 error cada 1.000–2.000 bases | hasta 25 kb (típicas ~15 kb) |
| **ONT R10.4.1 + [[Dorado]] v5 simplex** | long read | 99,75% (**Q26**) | ~0,25% | 1 error cada 400 bases | larga; ultra-long posible (>50 kb N50, reads >4 Mb) |
| **ONT [[Secuenciación dúplex\|dúplex]] (Kit 14 + SUP)** | long read duplex | ~Q30–Q31 (>99,9%) | ~0,1% a 0,08% | 1 error cada 1.000–1.250 bases | long reads |

La lectura clave de la tabla: ONT en modo simplex **sigue estando un escalón por debajo** de Illumina y PacBio HiFi en exactitud por base, pero la compensa con longitud, y en modo [[Secuenciación dúplex|dúplex]] llega al mismo orden de calidad. Ver [[Calidad Phred]].

### La explosión de herramientas bioinformáticas

Las tecnologías de tercera generación cambiaron **tres cosas simultáneamente**:

- el **volumen** de datos,
- la **longitud** de las lecturas,
- el **[[Perfil de error|perfil de error]]** asociado.

Como consecuencia, gran parte de las herramientas diseñadas para lecturas cortas dejó de ser directamente aplicable, y aparecieron familias enteras de software nuevo:

- [[Pulido de secuencias|Corrección de errores y pulido de secuencias]]
- [[Ensamblaje de novo]]
- SNPs y análisis de [[Variantes estructurales|variantes]]

El gráfico de Amarasinghe et al. muestra el número acumulado de herramientas creciendo casi verticalmente desde ~2014, dominado por la fracción de Oxford Nanopore.

*Amarasinghe et al. 2020. DOI: 10.1186/s13059-020-1935-5*

> [!quote] La idea que cierra la sección
> La principal consecuencia de las lecturas largas **no fue solamente obtener fragmentos más extensos**. Cambió el tipo de información recuperable y obligó a rediseñar los métodos bioinformáticos.

---

## 2. De dónde viene la secuenciación con nanoporos

> La secuenciación con nanoporos nace de la **convergencia de ideas, disciplinas y descubrimientos**.

El origen documentado es el cuaderno de [[David Deamer]] (UC Santa Cruz), con fecha **25 de junio de 1989**: volviendo en auto de Eugene a Belknap Lodge, anota la idea de secuenciar ADN directamente haciendo pasar la molécula por un canal pequeño mientras se aplica un voltaje, y registrando el cambio de corriente que produce cada base. El esquema del cuaderno ya incluye la traza escalonada con las letras I–C–G–T–A: es, literalmente, el primer [[Squiggle|squiggle]] dibujado a mano.

### Las líneas de trabajo que confluyeron

| # | Línea | Aporte | Nombres de referencia |
|---|---|---|---|
| 1 | Concepto y translocación | Idea de translocación, bloqueos de corriente, ADN/ARN monocatenario, lectura eléctrica | Deamer, Branton, Kasianowicz, Akeson, Bezrukov |
| 2 | Secuenciación escalable y concepto de motor | Proyecto Genoma Humano, motor de fago, movimiento controlado del ADN | Church, Baldarelli |
| 3 | Poros proteicos y biosensores | α-hemolisina, ingeniería del poro, *stochastic sensing*, adaptadores moleculares | Bayley, Cheley, Gouaux, Howorka, Gu |
| 4 | Reconocimiento de nucleótidos | Discriminación de bases, corriente dependiente de la secuencia | Ghadiri, Stoddart, Maglia, Clarke |
| 5 | Control del movimiento y *strand sequencing* | Polimerasa φ29, *ratcheting*, [[Basecalling|basecalling]] inicial | Cherf, Lieberman, Karplus |
| 6 | Traducción tecnológica | MspA, nanoporos de estado sólido, comercialización y CsgG | Gundlach, Niederweis, Derrington, Manrao; Golovchenko, Meller, Dekker, Marziali, Tabard-Cossa; Sanghera, Willcocks, Brown |

### Línea de tiempo (1995–2015)

| Año | Hito |
|---|---|
| 1995 | Church, Deamer y Branton presentan la solicitud de patente de secuenciación por nanoporos |
| 1996 | Primeros resultados de transporte de ADN a través del nanoporo de **α-hemolisina** |
| 1999 | Se distinguen segmentos de purinas y pirimidinas en moléculas individuales de ARN |
| 2001 | Se producen **nanoporos de estado sólido** y se usan para detectar ADN |
| 2005 | Un nanoporo logra discriminación de nucleobases individuales dentro de una hebra |
| 2005 | Se funda **Oxford Nanopore Technologies**, por Hagan Bayley con Spike Willcocks, David Norwood y Gordon Sanghera |
| 2008 | El grupo de Jens Gundlach detecta moléculas individuales de ADN con el poro **MspA** |
| 2012 | Control procesivo de la translocación con la **polimerasa φ29**; secuenciación con φ29 + MspA; Clive Brown presenta el **MinION** en el congreso AGBT |
| 2014 | ONT libera el MinION a usuarios tempranos en el programa **MAP** |
| 2015 | Se ensambla *de novo* un genoma de *E. coli* con 99,4% de exactitud usando **solo MinION** |

*Deamer, Akeson & Branton (2016). doi:10.1038/nbt.3423*

---

## 3. Las partes del sistema

El sistema tiene **tres componentes** con funciones inseparables.

### 3.1 La membrana

En las flow cells comerciales el nanoporo se integra en una **membrana sintética altamente estable** que forma parte del circuito de detección.

- Separa dos compartimentos (*cis* y *trans*) con electrolito, y debe generar **aislamiento eléctrico**.
- Evita que los iones la atraviesen libremente.
- La diferencia de potencial aplicada impulsa la **corriente iónica principalmente a través del nanoporo** — por eso lo que pasa dentro del poro se lee como una variación de corriente medible.
- Es compatible con **arrays y automatización**.
- Es **almacenable y transportable** (de ahí que exista un secuenciador de 130 g).

La versión comercial actual es una **membrana polimérica**, no una bicapa lipídica. La genealogía del concepto es larga:

| Etapa | Aporte |
|---|---|
| 1925 · Gorter y Grendel | La membrana como bicapa lipídica |
| 1962 · Mueller, Rudin, Tien y Wescott | Bicapas artificiales para medir corriente |
| 1970–1976 · Hladky, Haydon, Neher y Sakmann | Registro eléctrico de canales individuales |
| 1996 · Kasianowicz, Brandin, Branton y Deamer | El ADN/ARN altera la corriente de un poro |
| 2014–actualidad | Membranas poliméricas y **arrays de sensores** de ONT |

### 3.2 El nanoporo

El nanoporo actual es una **versión ingenierizada de CsgG**, una proteína de curli de *E. coli*. La clase compara las tres arquitecturas históricas:

| Poro | Características |
|---|---|
| **α-hemolisina** | Autoensamblaje estable en membranas; permite el paso de ADN monocatenario; produce cambios detectables en la corriente iónica. Su canal es relativamente largo y tiene regiones capaces de interactuar con el ADN — muchas bases influyen a la vez sobre la señal |
| **MspA** | Geometría más favorable; **constricción muy corta y estrecha**; alta densidad de corriente concentrada en la constricción |
| **CsgG** *(el actual)* | Constricción estrecha; caída de potencial concentrada alrededor de la constricción; apertura vestibular amplia; arquitectura **susceptible de ingeniería por mutagénesis**; buena interacción geométrica con el complejo ADN–proteína motora |

El salto de α-hemolisina a MspA y CsgG es, en el fondo, un problema de **resolución espacial molecular**: cuanto más corta es la zona sensible, menos bases contribuyen simultáneamente a la corriente y más fácil es asignarlas.

#### R9 → R10.4.1

El poro **R10.4.1** (CsgG–CsgF) presenta **dos regiones sensibles** —"doble lector"— en lugar de una:

- R9: una sola *scanning region*.
- R10: **dos constricciones**, lo que mejora la resolución, **especialmente en [[Homopolímeros|homopolímeros]]** (el talón de Aquiles clásico de la tecnología).
- Vigente desde 2020.

Con la química **R10.4.1 + V14**, el rendimiento típico reportado por ONT es **Q20+ en simplex y Q30+ en lecturas [[Secuenciación dúplex|dúplex]]**, según la química, el modelo y las condiciones experimentales.

*Goyal et al., 2014; Van der Verren et al., 2020; Van Dijk et al., 2023*

### 3.3 La proteína motora

La proteína motora está **unida al adaptador de secuenciación** que se liga a la molécula durante la [[Preparación de bibliotecas de secuenciación|preparación de la biblioteca]].

Su función es de control temporal: medir variaciones tan pequeñas de corriente requiere **controlar la velocidad de translocación del ADN**. Sin motor, la molécula atraviesa el poro demasiado rápido para muestrear la señal.

Se han usado dos familias:

- **Polimerasas** (históricamente, φ29)
- **Helicasas / translocasas** ← la opción actual

Además, la motora **desenrolla** el dúplex y hace pasar una sola hebra por el poro.

> [!quote] Cierre de la sección
> Estos tres componentes cumplen funciones inseparables: **la membrana aísla, el poro ayuda a pasar la molécula y generar la señal eléctrica, y la proteína motora regula el tiempo en que está en el poro.**

---

## 4. La asignación de bases — [[Basecalling]]

El **basecalling** es el proceso computacional donde la señal eléctrica se convierte al formato de secuencia nucleotídica (ADN o ARN).

### El punto conceptual central

> **ONT no detecta cada nucleótido de forma aislada.**
> La corriente está determinada por un grupo corto de nucleótidos —un **[[K-mer|k-mer]]**— situado simultáneamente en la región sensible del nanoporo.

Ese es el motivo por el cual el basecalling es un problema de aprendizaje automático y no una tabla de conversión: cada nivel de corriente corresponde a un *contexto*, no a una base. La traza de corriente cruda se llama **[[Squiggle|squiggle]]**.

### El flujo de datos

- La señal eléctrica se guarda en el formato **[[POD5]]** (antes FAST5).
- El basecaller toma los POD5 y convierte a **[[FASTQ]]** (o BAM/CRAM).
- El basecaller actual y oficial es **[[Dorado]] v2.1.2**.

### Cómo funciona Dorado por dentro

| # | Etapa | Qué hace |
|---|---|---|
| 1 | Señal cruda ([[POD5]]) | Corriente iónica medida por el nanoporo |
| 2 | Preprocesamiento | Escalado, normalización, recorte, división en *chunks* con solapamiento |
| 3 | **Inferencia neuronal** | Red neuronal (CNN + Transformer) que convierte la señal en representaciones contextuales |
| 4 | Representación estructurada | Estados **CRF**: probabilidades de transición entre contextos de k-mers (ej. estado de largo 5 → 4⁵ = 1024 contextos posibles) |
| 5 | Decodificación | *Beam search*: se consideran múltiples hipótesis y se selecciona la mejor trayectoria |
| 6 | Secuencia y calidad | Salida con [[Calidad Phred\|Q-scores]] en BAM/CRAM/FASTQ |

En paralelo, modelos adicionales predicen **[[Metilación del ADN|bases modificadas]]** (5mC, 5hmC, 4mC, 6mA…), que se emiten como *tags* MM/ML en el BAM y alimentan el análisis posterior (Modkit, visualización en IGV, identificación de motivos, metiloma/epitranscriptoma).

### La evolución de los basecallers

Los basecallers han evolucionado junto con la química de secuenciación:

| Basecaller | Período | Rasgos |
|---|---|---|
| **Metrichor** | 2014–2017 | Basecalling en la **nube**; primer flujo oficial; enfoque temprano basado en eventos |
| **Albacore** | 2017–2018 | Basecalling **local**; *raw basecalling*; mayor autonomía y precisión |
| **Guppy** | 2018–2024 (*legacy*) | **GPU** y tiempo real; modelos Fast/HAC/SUP; demultiplexado y modelos de bases modificadas |
| **[[Dorado]]** | 2023–actualidad | Basecaller actual de ONT; integrado en MinKNOW; simplex y dúplex; ADN y ARN; bases modificadas; más rápido y más preciso |
| **Bonito** | 2019–actualidad | Rama de **investigación**, código abierto, entrenamiento y evaluación de modelos; no es la línea principal de producción |

La trayectoria es nítida: **nube → local → GPU/tiempo real → ecosistema moderno** (MinKNOW, contenedores Docker).

### FAST, HAC y SUP

Los modelos neuronales **FAST, HAC y SUP** están optimizados para distintos compromisos entre **velocidad de inferencia y exactitud**. Es una decisión analítica real: el mismo POD5 rebasecalleado con SUP da una exactitud mayor que con FAST, a costa de mucho más cómputo. De ahí que la **versión del basecaller y el modelo usado sean metadatos que hay que registrar**.

---

## 5. Generación de los datos: plataformas y bibliotecas

### [[Plataformas de secuenciación ONT|Plataformas con distintas prestaciones]]

| | MinION Mk1D | GridION | PromethION 2 Integrated | PromethION 24 |
|---|---|---|---|---|
| Flow cells | 1 | 1–5 | 1–2 | 1–24 |
| Output típico por flow cell | 15–35 Gb | 15–35 Gb | 100–200 Gb | 100–200 Gb |
| Output típico por equipo | 15–35 Gb | 75–175 Gb | 200–400 Gb | **2,4–4,8 Tb** |
| Análisis a bordo | — | ✓ | ✓ | ✓ |
| Peso | **130 g** | 14,4 kg | 10,6 kg | 23 + 26 kg |

- Longitud de lectura: **cualquiera**, de 20 pb a más de 4 Mb, en todos los equipos.
- Tiempo de corrida: ~1–72 h, con **streaming de datos en tiempo real** para obtener resultados durante la corrida.
- Usos declarados: MinION y GridION → genomas pequeños, secuenciación dirigida, identificación microbiana, perfilado de [[Resistencia antimicrobiana|resistencia antimicrobiana]], expresión génica. PromethION → genomas grandes y humanos, cáncer, [[Metagenómica clínica|metagenómica]], transcriptómica de isoformas, single-cell.

### [[Preparación de bibliotecas de secuenciación|Preparación de bibliotecas]] con distintas estrategias

| Familia | Kit | Tiempo | Input | Longitud de lectura | PCR | Metilación |
|---|---|---|---|---|---|---|
| **ADN nativo** | Ligation | 60 min | ~1 µg gDNA | = largo del fragmento | No | ✓ |
| | Rapid | **10 min** | ~200 ng gDNA | Distribución aleatoria | No | ✓ |
| | Ultra-Long | 200 min + O/N | 6M células | **N50 >50 kb** | No | ✓ |
| **ADN amplificado** | Rapid PCR Barcoding | 15 min + PCR | **1–5 ng** | ~2 kb | Sí | — |
| **Dirigido** | Microbial Amplicon Barcoding | 60 min + PCR | 10 ng | **16S completo + ITS** | Sí | — |
| **ARN** | cDNA-PCR | 2,25 h + PCR | 10 ng poly(A)+ | cDNA full-length | Sí | — |
| | **Direct RNA** | 135 min | 300 ng poly(A)+ | = largo del ARN | No | ✓ |

El compromiso es sistemático: **la PCR abarata el input pero borra las modificaciones de base y acorta las lecturas**; el ADN nativo conserva todo pero exige más material.

### Qué determina la calidad de los datos

La clase separa los factores en tres bloques —una distinción muy útil porque cada uno se corrige en un lugar distinto del flujo:

**A. Plataforma y basecalling** *(afectan sobre todo la lectura individual)*

1. **Poro y química**: R10.4.1/E8.2 mejora la resolución y reduce errores frente a R9.4.1.
2. **Modelo de basecalling**: SUP > HAC >> FAST — mayor capacidad del modelo, menor error.
3. **Versión de [[Dorado]]**: rebasecallear con modelos más nuevos puede mejorar la exactitud sin volver al laboratorio.
4. **Modo de lectura**: [[Secuenciación dúplex|dúplex]] reduce errores combinando ambas hebras.

**B. Contexto molecular de la muestra** *(explican los errores residuales específicos de contexto)*

5. **Contexto de secuencia**: [[Homopolímeros|homopolímeros]], STR y regiones de baja complejidad aumentan sobre todo los **indels**.
6. **Bases modificadas / epigenética**: 5mC, 6mA y otras modificaciones alteran la señal y pueden inducir errores puntuales.

**C. Análisis posterior** *(afecta la [[Secuencia consenso|exactitud del consenso]], no la de cada read)*

7. **Cobertura y posprocesamiento**: más cobertura + corrección/[[Pulido de secuencias|pulido]] mejoran la exactitud del consenso.

> [!important] Resumen operativo
> - La **lectura individual** depende de: versión del poro y química, modelo y versión del basecalling, y modo de secuenciación (simplex o dúplex).
> - [[Dorado]] puede realizar **conjuntamente** el basecalling y la inferencia de determinadas modificaciones, mediante modelos específicos preentrenados.
> - Las **secuencias consenso** dependen de la cobertura, la corrección previa de errores, el pulido y la calidad inicial de las lecturas.

*Sanderson et al., Microbial Genomics 2024; Hall et al., eLife; Purushothaman et al., BMC Medical Genomics 2026*

### El crecimiento del campo

Las publicaciones indexadas en PubMed para *"oxford nanopore sequencing"* pasan de una decena a comienzos de los 2010 a **1.867 en 2025**, con crecimiento sostenido año a año.

---

## 6. Aplicaciones en microbiología y genómica microbiana

> [!warning] Marco regulatorio
> La mayor parte de las aplicaciones microbiológicas de ONT continúa siendo **RUO** (*Research Use Only*). Algunos de los protocolos mencionados son **LDT** (*Laboratory Developed Test*). Ver [[Uso clínico y marco regulatorio]].

Dos grandes bloques de aplicación:

| Bloque | Aproximaciones |
|---|---|
| **Microbiología clínica** | [[Secuenciación 16S\|16S rRNA Nanopore]] (identificación bacteriana desde muestra clínica; rutina documentada en Liverpool NHS y Berna) · [[Vigilancia genómica hospitalaria\|WGS de aislados]] (vigilancia y brotes; ejemplo Wellington) · TBseq / AmPORE-TB (tuberculosis + resistencia) |
| **[[Metagenómica clínica]]** | Muestra respiratoria → [[Depleción de ADN humano\|depleción de ADN humano]] → secuenciación → análisis taxonómico + AMR → informe clínico. Resultado en ~6–24 h, con impacto terapéutico el mismo día |

### 6.1 Caracterización bacteriana — [[Secuenciación 16S|secuenciación 16S]]

Tres implementaciones hospitalarias recientes, con diseños complementarios:

#### Siete hospitales del NHS, Reino Unido (2026)

Cheshire y Merseyside; muestras de pus, fluidos y tejidos de **sitios estériles**; 16S rRNA con ONT; *turnaround* 24–72 h; **218 casos** analizados.

| Resultado | Valor |
|---|---|
| Casos que aportaron información útil para *antimicrobial stewardship* | **56,9%** (124/218) |
| Solicitado por cultivo fallido | 32,1% (70/218) |
| Solicitado con paciente ya bajo antibióticos | 32,6% (71/218) |
| Géneros más detectados | *Streptococcus* 27,6% · *Staphylococcus* 20,7% · Enterobacterales 10,0% |

Impacto sobre el tratamiento (en los 165 positivos): confirmó el tratamiento existente 26,6%, sin cambios 28,0%, escalación 8,3%, desescalación y otros 28,0%. El mayor impacto clínico se observó en **pacientes inmunosuprimidos**.

Ante cultivo negativo o antibióticos en curso: el 16S **detectó la bacteria directamente en la muestra**, disminuyó la incertidumbre etiológica, y permitió convertir tratamiento empírico en **tratamiento dirigido**. Pero **no reemplaza el cultivo ni el antibiograma**.

*Cunningham-Oakes et al., 2026. https://doi.org/10.1016/j.ebiom.2026.106317*

#### Muestras de baja biomasa, ONT vs [[Illumina]] — Insel Gruppe, Suiza (2026)

101 muestras clínicas, 43 tipos de muestra, sitios normalmente estériles, comparación directa.

| Métrica | Valor |
|---|---|
| Concordancia ONT–Illumina | **93,5 ± 7,6%** |
| Cohen's kappa | 0,81 ± 0,04 |
| Precisión media | ONT 99,9 ± 0,39% · Illumina 99,8 ± 0,42% |
| Tiempo total (batch de 24) | ONT **~7,5 h** vs Illumina ~50,5 h (**≈50 h menos**) |
| Costo por muestra | ONT **35 CHF** vs Illumina 155 CHF |

Interpretación clínica: 77/101 (76,2%) con patógeno probable, 24/101 (23,8%) señal compatible con contaminación, **sin discordancia entre métodos** en la clasificación patógeno vs contaminación. Illumina mostró sensibilidad ligeramente mayor a concentraciones bacterianas muy bajas.

Conclusión: **alta concordancia**, y ONT como alternativa **rápida, costo-efectiva y viable**.

*Geers et al., 2026. https://doi.org/10.1128/spectrum.00623-26*

#### Workflow 16S intrahospitalario, Bélgica (2026)

54 muestras clínicas prospectivas, 53 pacientes, comparación con cultivo y hallazgos clínicos.

| Validación analítica | Valor |
|---|---|
| Límite de detección | *S. aureus* 260 CFU/mL · *P. aeruginosa* 747 CFU/mL |
| Linealidad | R² = 0,9778–0,9986 |
| Identificación correcta | Género >98% · Especie >85% |

Utilidad clínica: 25/26 muestras cultivo-positivas también positivas por 16S; **patógenos clínicamente relevantes adicionales** detectados en 5/28 cultivo-negativas y 7/26 cultivo-positivas.

Conclusión: 16S ONT es una herramienta viable para la detección microbiológica y **aumenta la recuperación de patógenos no detectados por cultivo**.

*Van de Gaer et al., 2026. https://doi.org/10.3389/fmicb.2026.1870167*

#### [[Porefile]]

Pipeline en **Nextflow** para perfilado de 16S de largo completo con lecturas ONT, desarrollado en el laboratorio de microbiología y genómica de Montevideo (`github.com/microgenlab/porefile`).

Flujo: lecturas 16S → **Nanofilt** (filtrado) → **NanoPlot** (QC) → **Minimap2** contra la base **SILVA** → **MEGAN6 LCA** → [[Clasificación taxonómica|clasificación taxonómica]] → tablas de conteo y taxonomía → estimación de abundancia relativa (con opción de reducir la base de datos).

Aplicaciones: identificación de aislamientos bacterianos y caracterización de comunidades **procariotas y eucariotas**.

> [!quote] Cierre de la sección 16S
> La secuenciación 16S ONT puede aumentar la recuperación de microorganismos cuando el cultivo es negativo o está condicionado por antibióticos.
> Su fortaleza es la **detección rápida y amplia**; su límite es que **no reemplaza el cultivo, el antibiograma ni la interpretación clínica**.

### 6.2 Caracterización bacteriana — genómica

Cuatro casos de [[Vigilancia genómica hospitalaria|vigilancia genómica hospitalaria]] articulados alrededor de un MinION:

| Caso | Aporte |
|---|---|
| **MRSA – NICU (2024)** | Detección temprana de brote y vigilancia prospectiva en tiempo real |
| **pQEB1 / KPC-2 (2024)** | Transmisión de [[Plásmido\|plásmidos]] AMR **entre especies**; resolución de elementos móviles |
| ***K. variicola* – NICU (2025)** | Brote + reservorio **ambiental**; intervención dirigida |
| **Sauerborn et al. (2026)** | Pacientes + ambiente; persistencia y reservorios de resistencia |

Lo que aporta ONT en este escenario: **rapidez**, **vigilancia descentralizada** con resolución de la cadena de transmisión, **reconstrucción de plásmidos y AMR**, e **integración paciente–ambiente** como apoyo al control de infecciones.

La docente conecta esto con trabajo propio en la región: la primera detección de *Klebsiella pneumoniae* ST15 multirresistente portadora de **OXA-48** en Sudamérica (*Journal of Global Antimicrobial Resistance*, 2022) y el estudio de cómo la microbiota humana disemina resistencia asociada a hospitales en el ambiente urbano, reflejando las tasas de casos en pacientes (*Microbiome*, 2022).

> [!quote] Cierre de la sección genómica
> En vigilancia hospitalaria, el valor diferencial de ONT aparece cuando necesitamos **pasar de identificar una especie a reconstruir transmisión, plásmidos, resistencia y conexiones entre pacientes y ambiente**.

*White et al. (2024) DOI: 10.1099/mgen.0.001273 · White et al. (2025) DOI: 10.1186/s13756-025-01529-2 · Moran et al. (2024) DOI: 10.1099/mgen.0.001291 · Sauerborn et al. (2026) DOI: 10.1099/mgen.0.001644*

### 6.3 Caracterización microbiana — [[Metagenómica clínica|metagenómica]]

El caso más maduro es la **NHS Respiratory Metagenomics Network** (`metagenomics.nhs.uk`), que desarrolla testeo metagenómico dentro del NHS para identificar rápidamente infecciones respiratorias.

#### Qué aporta

| # | Aporte | Dato reportado |
|---|---|---|
| 1 | Respuesta rápida | Resultados clínicamente útiles el mismo día (≥7–8 h) |
| 2 | Detección agnóstica | Bacterias, hongos y virus ADN/ARN en **un solo ensayo** |
| 3 | Más diagnósticos | 30% de las muestras con detecciones adicionales |
| 4 | Tratamiento dirigido | 28% cambios terapéuticos, 21% desescalación |
| 5 | [[Resistencia antimicrobiana]] | Detección de genes de resistencia para terapia precoz |
| 6 | Control de infecciones | 14% con implicancias para control de infecciones / salud pública |
| 7 | Más allá de la infección | 20% contribuyó a decisiones de inmunomodulación |

Impacto en tres niveles: **paciente** (diagnóstico etiológico rápido y terapia personalizada), **hospital** (brotes, AMR, control de infecciones) y **salud pública** (vigilancia genómica y patógenos emergentes).

> La metagenómica con ONT no solamente amplía el número de microorganismos que podemos detectar: **integra diagnóstico, resistencia y epidemiología dentro de una misma ventana temporal clínicamente útil**.

#### El flujo bioinformático

| Etapa | Herramientas / detalle |
|---|---|
| 1. Muestra | Muestras clínicas (respiratorias, sangre…) |
| 2. Preparación | Lisis y **[[Depleción de ADN humano\|depleción de ADN humano]]** |
| 3. Secuenciación | GridION / PromethION, [[Secuenciación en tiempo real\|en tiempo real]] |
| 4. [[Basecalling]] y QC | Guppy / MinKNOW, filtros de calidad (Q ≥ 10) |
| 5. Eliminación de humano | Alineamiento a **GRCh38**, se descartan reads humanas |
| 6. [[Clasificación taxonómica]] | **Centrifuge** + base curada (virus, bacterias, hongos) |
| **⏱ ≈2 h** | **Resultado preliminar**: identificación de patógenos (umbrales clínicos de reporte) + [[Resistencia antimicrobiana\|AMR]] (**Abricate + CARD + Scagaire**) |
| 7. [[Ensamblaje de novo\|Ensamblaje]] / [[Secuencia consenso\|consenso]] | Mapeo a referencia (**minimap2**); variantes y consenso (**Medaka**, **bcftools**) |
| 8. Tipado y vigilancia | SNPs, MLST, linajes/clados (**Nextclade**, **SNP-sites**) |
| **⏱ ≈24 h** | **Resultado final**: 9. Interpretación clínica e informe integrado |

Atributos del flujo: detección amplia · rápido · preciso · escalable. Pero —advierte la clase— **cada una de sus etapas introduce posibles sesgos**.

#### Limitaciones y oportunidades

| # | Limitación | Detalle |
|---|---|---|
| 1 | **Sensibilidad en baja carga** | Puede perder microorganismos poco abundantes, especialmente virus ARN. Metagenómica < PCR en límite de detección |
| 2 | **Preparación de la muestra** | La [[Depleción de ADN humano\|depleción de ADN humano]] puede reducir también material microbiano; el rendimiento varía según el tipo de muestra |
| 3 | **Genoma incompleto** | No siempre se recupera cobertura suficiente para ensamblar; limita AMR, tipado y vigilancia |
| 4 | **Infección vs colonización** | Detectar un microorganismo no implica que sea la causa de la infección; requiere correlación clínica |
| 5 | **Escalabilidad** | La implementación rutinaria aún requiere automatización y mayor throughput; flujo más complejo que el cultivo |
| 6 | **Validación clínica** | Faltan estudios multicéntricos y controlados; el impacto en *outcomes* está todavía en evaluación |

> [!danger] Las tres desigualdades a recordar
> **detección ≠ infección** · **gen de AMR ≠ fenotipo** · **resultado rápido ≠ beneficio clínico demostrado**

*Charalampous et al., Genome Medicine 2021; Alcolea-Medina et al., Communications Medicine*

#### GridION Dx — 2026

ONT obtiene para GridION las certificaciones **CE y UKCA**: es el **primer dispositivo de diagnóstico *in vitro*** de la compañía registrado en el Reino Unido y Europa. Se usará con **protocolos validados por terceros**, y **no** admite desarrollo de ensayos custom ni modos research/developer (para eso ONT ofrece la línea Q-Line, orientada a [[Uso clínico y marco regulatorio|LDT]]).

Es un hito de madurez: marca el paso de "plataforma de investigación que a veces se usa en clínica" a "dispositivo regulado".

### 6.4 Caracterización microbiana — metiloma

Una capacidad exclusiva de la secuenciación de molécula nativa: ONT permite descubrir **directamente y *de novo*** los tres tipos principales de [[Metilación del ADN|metilación bacteriana]] —**6mA, 4mC y 5mC**— tanto en bacterias individuales como en microbiomas, sin conversión con bisulfito.

- Herramienta desarrollada: **[[Nanodisco]]** (`github.com/fanglab/nanodisco`).
- Uso principal: las metilaciones funcionan como **huellas epigenéticas naturales** para identificar y relacionar componentes del metagenoma (asignar contigs y plásmidos a su hospedador).

En un estudio sobre comunidades bacterianas y virales del **hielo marino**, ONT permitió obtener simultáneamente la secuencia metagenómica y las modificaciones del ADN nativo. La conclusión fue que allí la metilación **no solo participa en la defensa frente a ADN extraño**, sino que podría regular la **adaptación metabólica** bacteriana y mediar las **interacciones fago–hospedador**.

*Tourancheau et al., Nature Methods · Kanaan & Deming, ISME J 2025*

---

## 7. [[Plataformas emergentes de nanoporos|Plataformas emergentes]]

El campo dejó de ser un monopolio. Todas las especificaciones son **declaradas por el fabricante y requieren validación independiente**.

| Plataforma | Principio | Rendimiento | Exactitud | Observaciones |
|---|---|---|---|---|
| **QitanTech** (QNome-3841, QCell-384) | Nanoporo clásico | Menor que ONT | 99% reportada | Algunas herramientas de ONT aceptan su [[FASTQ]]; limitada principalmente a China |
| **MGI CycloneSEQ** (G100) | Nanoporo | **>50 Gb por celda** en evaluaciones iniciales independientes | Algo inferior a R10.4.1 | Benchmark cross-platform reporta errores de sustitución asociados a metilación |
| **PolyseqOne** | Nanoporo | >50 Gb por celda | **>99%** | Requiere validaciones independientes |
| **Roche AXELIOS 1** — [[Sequencing by Expansion\|SBX]] | Nanoporo para detección, **sin ADN nativo en el poro**: la secuencia se convierte en un polímero sintético expandido (**Xpandomer**) | **≥1,8 Tb** | Error ~1:6000 (**Q38**) | **Lecturas cortas** — rompe la asociación nanoporo = lectura larga |
| **Axbio AxiLona AXP-100** | *Nanopore sequencing by synthesis* (NSBS/EL-NGS) | — | >99% tras consenso circular | Longitud ≥10 kb hasta 100 kb |
| **Geneus Gseq-500** | NSBS | 15 Gb en 10 h | 93,25% | ADN y ARN; basecalling en tiempo real |

La línea de tiempo de la tecnología (Zhang T. et al., 2024) muestra la sucesión de químicas **R6 → R7 → R7.3 → R9 → R9.4 → R9.5 → R10 → R10.3 → R10.4 → R10.4.1**, con los equipos apareciendo en paralelo: MinION (2014), primer genoma humano con MinION (2016), PromethION (2018), Flongle y primer secuenciador chino QNome-9604 (2020), PromethION 2 / QNome-3841hex / Gseq-500 (2022, el año en que *Nature Methods* declaró la secuenciación de lecturas largas como método del año), PolyseqOne y CycloneSEQ (2024)… y el signo de interrogación final: **¿Roche? ¿Illumina? ¿Quién sigue?**

*Zhang T., et al. (2024). https://doi.org/10.1016/j.jgg.2024.09.007*

---

## 8. [[Secuenciación de proteínas con nanoporos|La secuenciación de proteínas con nanoporos]]

> La evolución hacia una plataforma comercial **está sucediendo ahora**.

| Año | Hito | Referencia |
|---|---|---|
| 2013 | **Translocación controlada**: ClpX despliega y conduce proteínas por α-hemolisina | Nivala et al. |
| 2014 | **Huellas de variantes**: el patrón de corriente diferencia variantes proteicas | Nivala et al. |
| 2018 | **Resolución de un residuo**: la aerolisina distingue homopéptidos que difieren en un aminoácido de longitud | Piguet et al. |
| 2020 | **Los 20 aminoácidos**: reconocimiento eléctrico individual con aerolisina | Ouldali et al. |
| 2021 | **Relectura molecular**: helicasa + MspA detectan sustituciones de un aminoácido | Brinkerhoff et al. |
| 2023 | **Secuenciación de péptidos**: degradación con carboxipeptidasa + reconocimiento por α-hemolisina | Zhang et al. |
| 2024 | **Proteínas largas**: ClpX + CsgG permiten lectura multipaso en una matriz ONT | Motone et al. |
| 2026 | **Sensado paralelo**: perfilado de péptidos e identificación de proteínas con bibliotecas OPO | Wang et al. |

En paralelo, la bioinformática de proteínas por nanoporos:

| Año | Herramienta | Qué hace |
|---|---|---|
| 2017 | **Nano-Align** | Identificación contra bases de datos proteicas |
| 2021 | **NanoporeTERs** | Clasificación de etiquetas proteicas sintéticas |
| 2021 | **Poretitioner** | Detección, extracción y filtrado de eventos |
| 2021 | **Chop-n-drop** | Simulación y alineamiento de huellas proteicas |
| 2024 | **PASTOR-sequencing** | Segmentación, DTW, aprendizaje automático y relecturas |

- La bioinformática de proteínas por nanoporos ha avanzado desde la **detección y segmentación de eventos** hacia el ***fingerprinting*** y la **identificación asistida por [[Machine Learning|aprendizaje automático]]**.
- El **"basecalling" de proteínas completas es un punto caliente de innovación**.

Es exactamente la misma trayectoria que recorrió el ADN entre 1989 y 2014, comprimida y en curso.

---

## Consideraciones finales

1. Con la secuenciación de nanoporos se pueden observar, **en una misma molécula de ADN, varias dimensiones de la información biológica**: secuencia, [[Variantes estructurales|variantes estructurales]] y [[Metilación del ADN|metilación]].
2. De secuenciar genomas a **obtener genomas completos**: bacterianos, e incluso genomas humanos completos y **haplotipo-resueltos**.
3. **Secuenciación como proceso dinámico**: los datos se generan y analizan mientras la biblioteca está en el equipo ([[Secuenciación en tiempo real]]).
4. La **aplicación clínica es aún limitada**: bases de datos curadas y actualizadas, trazabilidad de las versiones de basecaller y software, acreditación regulatoria y evaluación costo-beneficio.
5. En [[Metagenómica clínica|metagenómica clínica]], el principal cuello de botella es la **baja proporción de ADN microbiano frente al ADN humano** y la capacidad de analizar los datos de forma **reproducible**. Detectar un microorganismo o un gen de resistencia **no demuestra causalidad clínica, viabilidad ni expresión fenotípica**: se requiere metodología clásica confirmatoria.

> [!quote] El cierre
> El impacto de la secuenciación con nanoporos a largo plazo dependerá tanto de los avances e implementaciones **como de nuestra capacidad bioinformática para interpretar responsablemente esa información.**

---

## Ideas para retener

- **La señal no es una base, es un contexto.** ONT mide la corriente de un [[K-mer|k-mer]] completo dentro del poro. Todo el problema del [[Basecalling|basecalling]] —y buena parte del [[Perfil de error|perfil de error]]— sale de ahí.
- **Los datos crudos son la señal, no la secuencia.** Guardar los [[POD5]] permite **rebasecallear** años después con un modelo mejor y mejorar la exactitud sin volver al laboratorio. Ningún otro tipo de dato de secuenciación tiene esa propiedad.
- **La longitud cambió el tipo de pregunta, no solo la escala.** Plásmidos, elementos móviles, repeticiones y haplotipos son resolubles porque una sola lectura los atraviesa enteros.
- **Leer ADN nativo trae la epigenética gratis.** La [[Metilación del ADN|metilación]] no requiere un ensayo aparte; es una capa que ya está en la señal si no se hizo PCR.
- **En clínica, la velocidad no es el argumento decisivo.** Los tres estudios de 16S y toda la sección de metagenómica insisten en lo mismo: el valor aparece cuando el resultado **cambia una decisión**, y eso todavía necesita validación, bases curadas y correlación clínica.
- **El cuello de botella se corrió, otra vez, al análisis.** Igual que en las clases de single cell y espacial, la conclusión es que generar los datos ya no es el problema.

## Conexiones

- Viene de → [[Biología espacial - mapeando la expresión génica a su entorno]]
- Índice → [[Módulo 1 - MOC]]
- Continúa en → [[Módulo 2 - MOC|Módulo 2 (Biología de Sistemas)]] y [[Módulo 4 - MOC|Módulo 4 (desarrollo y despliegue)]]
