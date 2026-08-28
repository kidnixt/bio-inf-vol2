---
titulo: "Biología espacial: mapeando la expresión génica a su entorno"
curso: Fronteras y Perspectivas en Bioinformática – Universidad ORT
modulo: Módulo 1 - Avances en las ciencias ómicas
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
> **Curso:** Fronteras y Perspectivas en Bioinformática – Universidad ORT (2026)
> **Módulo:** [[Módulo 1 - MOC|Módulo 1 - Avances en las ciencias ómicas]]
> **Docente:** [[Guillermo Eastman]] — Departamento de Genómica, [[IIBCE]]
> **PDF original:** `Modulo 1 - Avances en las ciencias ómicas/Biología espacial - mapeando la expresión génica a su entorno.pdf`
> **Clase previa:** [[Aproximaciones ómicas con resolución de célula única]]

---

## La pregunta que abre la clase

El [[scRNA-seq]] nos dice **qué genes está expresando cada célula individualmente**. Pero deja una segunda pregunta sin responder:

> **¿Dónde está cada célula en el tejido? ¿Qué otras células tiene alrededor?**

Esto completa una progresión de tres pasos que estructura todo el módulo:

| Aproximación | Qué obtenemos |
|---|---|
| [[Bulk RNA-seq]] | **Promedios** |
| [[scRNA-seq]] | **Distribuciones** |
| [[Transcriptómica espacial]] | **Contexto** |

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

El flujo estándar de single cell es:

```
Tejido → disociación → células → scRNA-seq → UMAP
```

Ese flujo **conserva** mucho:

- Resolución celular
- [[Heterogeneidad celular|Heterogeneidad]]
- [[Estado celular|Estados celulares]]
- Perfiles transcriptómicos individuales

Pero el paso de **disociación** destruye irreversiblemente:

- **Posición**
- **Arquitectura**
- **Vecinos**
- **Estructura tisular**
- **Relaciones espaciales**

El [[UMAP]] es un espacio de similitud transcriptómica, no un mapa del tejido: dos células juntas en el UMAP pueden estar en extremos opuestos del órgano, y dos células vecinas en el tejido pueden caer en clusters distintos.

### La arquitectura del tejido importa

El argumento biológico es que la función no depende solo de qué es cada célula, sino de **con quién está**. Una [[Microglía]] reactiva pegada a una placa amiloide y una microglía reactiva en tejido sano pueden tener perfiles parecidos, pero significan cosas distintas. El contexto es parte del fenotipo.

---

## 2. ¿Cómo medimos ARN en el espacio?

Las plataformas se dividen en **dos grandes familias**, con un compromiso opuesto entre ellas:

### Métodos basados en hibridación de sondas

Se detectan transcriptos *in situ* mediante sondas fluorescentes, imagen y rondas de hibridación.

| Ventajas | Desafíos |
|---|---|
| **Resolución extrema** (subcelular) | Limitados a la **cantidad de sondas** utilizadas (panel dirigido) |
| | **Visualización** de los datos |

Ver [[Métodos basados en sondas]].

### Métodos basados en secuenciación masiva

Se captura el ARN sobre una superficie con [[Barcode espacial|barcodes espaciales]] y luego se secuencia.

| Ventajas | Desafíos |
|---|---|
| **Descubrimiento molecular** (transcriptoma sin sesgo de panel) | **Resolución** más gruesa |

Ver [[Métodos basados en secuenciación]].

### Breve historia

La línea de tiempo de la clase muestra las dos familias avanzando en paralelo desde ~1980 (hibridación) y ~2008–2009 (secuenciación), con la aceleración comercial concentrada en la última década:

| Año | Actor |
|---|---|
| 2016 | [[Vizgen]] |
| 2017 | [[10x Genomics]] |
| 2019 | [[Nanostring]] |
| 2021 | [[BGI]] |
| 2022 | [[Nanostring]] / [[10x Genomics]] (nuevas generaciones) |

---

## 3. El trade-off central

> **Número de genes × Número de células × Resolución espacial × Throughput**

No se puede maximizar todo a la vez. Ninguna plataforma gana en las cuatro dimensiones; elegir plataforma **es** elegir qué sacrificar.

| Instrumento | # Genes | Resolución espacial | Throughput |
|---|---|---|---|
| [[GeoMx DSP\|GeoMx]] | Alto a completo | Baja – regional ([[ROI]]) | Alto |
| [[CosMx SMI\|CosMx]] | Alto a completo | Célula única y subcelular | Moderado – bajo |
| [[Visium HD]]* | Completo | Alta, cerca de célula única | Alto |

---

## 4. Las plataformas en detalle

### [[GeoMx DSP]] (Digital Spatial Profiler)

Trabaja por **[[ROI|regiones de interés]]** seleccionadas por el usuario sobre la imagen del tejido, no célula por célula.

- **Sensibilidad:** hasta 1200 proteínas, o [[Transcriptoma]] completo
- **[[ROI]]:** entre 50 y 600 µm de diámetro → entre 50 y 500 células por región

Es la plataforma de elección cuando la pregunta es *"¿en qué se diferencian estas dos zonas del tejido?"* y no *"¿qué hace cada célula?"*.

### [[CosMx SMI]] (Spatial Molecular Imager)

Basado en imagen y sondas, con resolución de **célula única y subcelular**. Permite ubicar transcriptos individuales dentro del citoplasma o el núcleo, a costa de un throughput menor y de trabajar con un panel de genes definido.

### [[Visium]] vs [[Visium HD]]

La clase contrasta las dos generaciones de [[10x Genomics]]:

- **[[Visium]]**: captura sobre spots con [[Barcode espacial|barcodes espaciales]] y **secuenciación**; cada spot agrupa varias células.
- **[[Visium HD]]**: pasa a una grilla continua mucho más fina basada en **sondas**, acercándose a resolución de célula única con transcriptoma completo.

---

## 5. Desafíos bioinformáticos (y técnicos)

### En métodos de captura sobre oligos en superficie ([[Visium HD]])

- **[[Lateral diffusion]]**: el ARN difunde lateralmente antes de ser capturado, así que la señal se "corre" respecto de su origen real y difumina los bordes entre estructuras.

### En métodos de sondas

- **[[Optical crowding]] / crosstalk**: demasiadas señales fluorescentes en un mismo vóxel, imposibles de resolver ópticamente.
- **[[Photobleaching]]**: la fluorescencia se apaga con las rondas sucesivas de imagen.
- **[[Autofluorescencia]]**: el propio tejido emite señal de fondo.
- **[[Stage drift]]**: el portaobjetos se desplaza entre rondas y las imágenes dejan de alinearse.

### Transversales a todas las plataformas

- **[[Segmentación celular]]** (*cell segmentation*): decidir qué píxeles y qué transcriptos pertenecen a qué célula. Es el paso más determinante y más frágil de todo el pipeline espacial: un error de segmentación se propaga a la anotación, al clustering y a cualquier conclusión sobre vecindarios.
- **[[Integración de datos single cell y spatial]]**: usar un atlas de [[scRNA-seq]] (profundo pero sin posición) como referencia para anotar o deconvolucionar datos espaciales (posicionados pero menos profundos).
- **[[Almacenamiento y visualización]]**: *storage and visualization!* — los datos espaciales combinan matrices de conteo con imágenes de alta resolución; el volumen y la interactividad son un problema en sí mismos.

---

## 6. Aplicaciones biológicas: ¿qué estamos aprendiendo?

### Estructura del tejido

- **[[Spatial domains]]**: regiones del tejido con un perfil transcriptómico coherente (capas corticales, zonas de un tumor).
- **[[Neighborhoods]]**: qué tipos celulares aparecen sistemáticamente juntos.
- **[[Spatial niches]]**: microambientes funcionales definidos por la composición celular local. El ejemplo de la clase es el nicho glial alrededor de las placas amiloides en modelos de enfermedad de Alzheimer.

Referencias citadas: Chen and Lu & Fiers and De Strooper, *Cell* (2020); A. Mallach & M. Zielonka et al., *Cell Reports* (2024); M. Goedert et al., *Brain* (2017).

### Atlas espaciales

La escala de los [[Atlas celulares]] espaciales dio un salto reciente — la clase lo marca con un enfático *"Atlas! (!!!)"*, citando Cheng et al. (2022) y Pan, J. et al., *Nature* (2026).

---

## Perspectivas

Las preguntas de cierre:

1. **¿Vamos hacia la construcción de un "Google Maps" de la biología?**
2. **Si podemos medir cada célula, saber dónde está y qué ocurre a su alrededor… ¿qué nos falta para entender realmente un tejido?**
3. **Estamos generando datos biológicos a una velocidad mayor de la que somos capaces de interpretarlos.**

Y el diagnóstico final, que es la bisagra hacia el resto del curso:

```
datos  ──────────────────────────►  conocimiento
        almacenamiento
        visualización
        integración
```

El cuello de botella ya no es generar los datos, sino atravesar esas tres etapas. Eso conecta directamente con el [[Módulo 2 - MOC|Módulo 2 (Biología de Sistemas)]], el [[Módulo 3 - MOC|Módulo 3 (IA aplicada)]] y el [[Módulo 4 - MOC|Módulo 4 (desarrollo y despliegue)]].

---

## Ideas para retener

- La disociación es un paso **destructivo**: todo lo espacial se pierde ahí y no se recupera computacionalmente sin una referencia.
- El [[UMAP]] no es un mapa del tejido. Confundir proximidad transcriptómica con proximidad física es el error conceptual más común del campo.
- Elegir plataforma espacial es elegir en qué esquina del trade-off *genes × células × resolución × throughput* querés estar. La pregunta biológica define la plataforma, no al revés.
- La [[Segmentación celular]] es el paso que más condiciona la calidad de todo lo que viene después.

## Conexiones

- Viene de → [[Aproximaciones ómicas con resolución de célula única]]
- Índice → [[Módulo 1 - MOC]]
