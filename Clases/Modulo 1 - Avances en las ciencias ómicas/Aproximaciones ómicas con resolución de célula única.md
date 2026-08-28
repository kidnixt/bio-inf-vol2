---
titulo: Aproximaciones ómicas con resolución de célula única
curso: Fronteras y Perspectivas en Bioinformática – Universidad ORT
modulo: Módulo 1 - Avances en las ciencias ómicas
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
> **Curso:** Fronteras y Perspectivas en Bioinformática – Universidad ORT (2026)
> **Módulo:** [[Módulo 1 - MOC|Módulo 1 - Avances en las ciencias ómicas]]
> **Docente:** [[Guillermo Eastman]] — Departamento de Genómica, [[IIBCE]]
> **PDF original:** `Modulo 1 - Avances en las ciencias ómicas/Aproximaciones ómicas con resolución de célula única.pdf`
> **Clase siguiente:** [[Biología espacial - mapeando la expresión génica a su entorno]]

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

La premisa de toda la clase es una sola frase: **la mayoría de los tejidos son heterogéneos**. Un tejido no es un bloque uniforme de "un tipo de célula", sino una *comunidad de células diferentes* que conviven, se comunican y cumplen funciones distintas. Ese fenómeno se conoce como [[Heterogeneidad celular]].

### El ejemplo del tejido cerebral

El [[Tejido cerebral]] ilustra bien la escala del problema:

| Escala | Número aproximado |
|---|---|
| Células en cerebro de ratón | ~110 millones |
| Células en cerebro humano | ~170 mil millones |

Sobre ese tejido se reconocen **4 grandes tipos celulares**, cada uno con subdivisiones cada vez más finas:

- **[[Neurona|Neuronas]]** → excitatorias / inhibitorias
- **[[Macroglía|Macroglías]]** (soporte y mantenimiento) → [[Astrocito|astrocitos]], [[Oligodendrocito|oligodendrocitos]], progenitores de oligodendrocitos ([[Oligodendrocito|OPCs]])
- **[[Microglía|Microglías]]** (sistema inmune del SNC) → homeostática / reactiva
- **Células sanguíneas y vasculares** → [[Célula endotelial|endoteliales]], musculares

La estructura jerárquica que se usa hoy para nombrar células va de lo grueso a lo fino:

```
[Clase General]  (4)
   ➜ [Subclase]  (docenas)
        ➜ [Clúster / Tipo Celular]  (>3000)
```

Esta jerarquía es exactamente el problema de la [[Identidad celular]]: cuántos niveles se reconocen depende de la resolución con la que midamos.

### ¿Cómo definimos una célula a nivel molecular?

> **En función de conocer qué genes expresa.**

Ésa es la respuesta que habilita todo lo demás: si la identidad de una célula está codificada en su programa de expresión, entonces medir [[Expresión génica]] célula por célula es medir identidad celular.

---

## 2. Expresión génica y transcriptomas

La [[Expresión génica]] sigue el flujo de la información genética del [[Dogma central de la biología molecular|dogma central]]: ADN → [[ARN mensajero|ARN]] → [[Traducción|proteína]].

### ¿Qué es un transcriptoma?

El [[Transcriptoma]] es **la colección completa de todas las moléculas de ARN presentes en una célula o tejido en un momento dado**. Medirlo responde dos preguntas:

- ¿Qué genes se están expresando?
- ¿En qué nivel?

Un punto clave que se destaca en la clase es el **[[Rango dinámico]]** de abundancia de transcriptos: los niveles de expresión abarcan varios órdenes de magnitud dentro de la misma célula.

| Gen | Abundancia relativa (orden) |
|---|---|
| GAPDH | ~100.000 |
| ACTB | ~10.000 |
| MAP2 | ~1.000 |
| RBFOX3 | ~100 |
| TREM2 | ~10 |
| NANOG | ~1 |

Esto significa que los genes interesantes (marcadores de tipo celular, factores de transcripción) suelen ser justamente los de **baja abundancia**, los más difíciles de detectar.

### Transcriptómica bulk

En [[Bulk RNA-seq]] se secuencia el ARN de una muestra entera. Una advertencia conceptual importante de la clase:

> **No estamos midiendo expresión directamente. Estamos cuantificando la abundancia de las moléculas de ARN muestreadas.**

Todo lo que llamamos "expresión" pasa por filtros técnicos:

- **Sampleo** (qué moléculas terminan en la librería)
- **[[Profundidad de secuenciación]]**
- **Ruido**
- **Distribución de conteos**

El resultado es una [[Matriz de conteo]] de dimensiones modestas: ~10.000 genes × [6–10] condiciones.

```
          Sample 1   Sample 2   Sample 3
Gene A      1000       1200        950
Gene B        20         50         15
Gene C         0          2          1
```

Sobre esa matriz se hacen los análisis clásicos: clustering de muestras, [[Expresión diferencial|DEGs]], [[Gene Ontology]] y detección de genes co-regulados.

### Las limitaciones del bulk

Al mezclar corteza cerebral con hipocampo (o cualquier región con otra), el bulk devuelve **promedios**. Y en un promedio se pierden:

- Los distintos [[Tipo celular|tipos celulares]]
- Los [[Estado celular|estadíos / estados celulares]]
- Las subpoblaciones
- Las **células raras** (que a menudo son las biológicamente decisivas)

---

## 3. La "revolución": single cell RNA-seq

El salto conceptual del [[scRNA-seq]] se resume en una sola oposición:

> **Promedios → Distribuciones**

En lugar de un valor por gen por muestra, obtenemos una distribución de valores por gen a lo largo de miles o millones de células.

### 1er desafío: matchear secuencias con células únicas

*¿Cómo sabemos de qué célula proviene cada molécula de ARN secuenciada?*

La respuesta combina dos frentes:

| Frente | Solución |
|---|---|
| **Protocolos / tecnología** | [[Aislamiento de células individuales]] |
| **Biología molecular** | [[Barcode celular|Barcodes]] + [[UMI]] (*unique molecular identifier*) |

El objetivo final es **lograr realizar reacciones de biología molecular en células individuales**.

#### Aislamiento de células individuales

Métodos de primera generación — poco automatizados y poco eficientes, requieren mucho tiempo para aislar grandes números de células:

- [[Dilución al límite]]
- [[Micromanipulación]]
- [[Microdisección por captura láser]] (LCM)

Métodos de alto rendimiento, los que hicieron viable la escala actual:

- [[Citometría de flujo|Citometría (cell sorting)]]
- [[Microfluídica]] y microgotas

#### Barcodes y UMIs

La lectura secuenciada se construye con varios elementos, cada uno con una función:

| Elemento | Función |
|---|---|
| Adaptador | Anclaje para secuenciar |
| [[Barcode celular]] | Identifica **la célula** |
| [[UMI]] | Identifica **moléculas individuales** |
| Secuencia de ADNc | Identifica el **transcripto** |

El [[UMI]] es el que permite distinguir *moléculas originales* de *copias generadas por PCR*, y por eso es la pieza que vuelve cuantitativo al método.

#### Un ejemplo de workflow: [[10x Genomics]]

La clase recorre el workflow de [[10x Genomics]] como caso concreto, y contrasta sus dos químicas: el **3' Assay** y el **5' Assay** (este último es el que habilita, por ejemplo, el perfilado de receptores inmunes).

### 2do desafío: la cantidad de ARN

Una célula individual contiene muy poco ARN — del orden de picogramos. La solución es la **amplificación de ADNc por PCR**, que introduce a su vez el sesgo que el [[UMI]] viene a corregir.

### 3er desafío: el alineamiento

De un experimento de scRNA-seq obtenemos, en primer lugar, **secuencias (raw data)**. Y ahí aparece la explosión de datos:

| | [[Bulk RNA-seq]] | [[scRNA-seq]] |
|---|---|---|
| Diseño típico | 3 vs 3 (6 muestras) | 10k células |
| Lecturas | 20–30 M reads por muestra | 20k–50k reads por célula → **200–500 M reads** |
| Metadata técnica | — | [[Barcode celular\|barcodes]] + [[UMI\|UMIs]] |

Las [[Alineamiento de secuencias|herramientas clásicas de alineamiento]] sufren con:

- Sitios de unión exón–exón
- Uso de memoria RAM
- Manejo de [[Multimapping|multimappings]]

**Cambio de foco:** *no importa dónde mapea la lectura dentro del gen, ni qué mismatch hay; solo importa saber a qué gen corresponde.* De ahí el [[Pseudoalineamiento]]:

- Alineamiento directo al [[Transcriptoma]]
- No se buscan coordenadas exactas, sino **compatibilidad**

El beneficio es de órdenes de magnitud en tiempo y memoria (la clase muestra un benchmark de 20 sets de datos de 30 millones de lecturas con 20 cores).

### La matriz de conteo single cell

El segundo producto del experimento es la [[Matriz de conteo]], y la diferencia de escala con el bulk es brutal:

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

Nótese la cantidad de ceros: ése es el fenómeno de [[Sparsity]].

---

## 4. ¿Qué sigue? El pipeline de análisis

### Control de calidad

El [[Control de calidad en scRNA-seq]] se apoya en tres métricas canónicas, que se inspeccionan por célula:

- **Número de [[UMI|UMIs]] por célula** — profundidad; valores muy bajos = gotas vacías, muy altos = dobletes
- **Número de genes por célula** — complejidad de la librería
- **Fracción de [[Genes mitocondriales]]** — proxy de estrés / muerte celular

### Reducción dimensional y clustering

Se pasa de un espacio de 10–20 mil genes a 2–3 dimensiones mediante [[Reducción dimensional]] ([[PCA]], y luego [[UMAP]] o t-SNE para visualizar), y sobre ese espacio se hace [[Clustering]] para agrupar células con perfiles similares.

### Identificación de tipos celulares

El clúster es una entidad estadística; convertirlo en un tipo celular con nombre es [[Anotación de tipos celulares]]. Dos familias de estrategias:

**Estrategias manuales**

- [[Expresión diferencial]] entre clusters
- Análisis en base a literatura (genes marcadores conocidos)
- Anotación de tipos celulares

**Estrategias automatizadas**

- Basadas en correlación con un set de datos previo (referencia)
- Basadas en [[Machine Learning]] con múltiples sets de datos previos

### Análisis downstream

- **[[Expresión diferencial]]**: entre clusters o entre condiciones, con la estrategia de [[Pseudobulk]] para no inflar la significancia tratando células como réplicas.
- **[[Pseudotiempo]] o trayectorias**: ordenar las células a lo largo de una trayectoria de desarrollo o diferenciación basada en cambios de expresión génica.

---

## 5. Más allá del transcriptoma: ómicas single-cell

*¿Cómo medir cada nivel regulatorio en células únicas?*

| Nivel regulatorio | Técnica single-cell |
|---|---|
| Accesibilidad de la [[Cromatina]] | [[scATAC-seq]] (*Assay for Transposase-Accessible Chromatin sequencing*) |
| Eventos traduccionales | [[scRibo-seq]] (*ribosome profiling*), con micro volúmenes (~50 nL); alternativa: **Ribo-STAMP** |
| Proteínas | [[Proteómica de célula única]] |

Los desafíos propios de la [[Proteómica de célula única]] son distintos de los del ARN:

- **No podemos amplificar** (no hay PCR para proteínas)
- **Rango dinámico muy amplio**
- **Adsorción en superficies** (se pierde material en las paredes del tubo)

---

## 6. Desafíos bioinformáticos

| Desafío | En qué consiste |
|---|---|
| [[Sparsity]] | Gran cantidad de ceros en la matriz |
| Ruido + [[Batch effect]] | Variabilidad técnica y biológica + diferentes experimentos/plataformas |
| [[Alta dimensionalidad]] | Pasar de 10k–20k genes a 2–3 dimensiones |
| [[Identidad celular]] | ¿Cómo definir a una célula y cómo nombrarla? |
| [[Integración de datos multiómicos]] | scATAC-seq + scRNA-seq + scRibo-seq + scProteomics |

> Aproximaciones de [[Machine Learning]], [[Deep Learning]] y [[Inteligencia Artificial]] pueden aportar soluciones.
> — conexión directa con el [[Módulo 3 - MOC|Módulo 3: Inteligencia Artificial aplicada a Bioinformática]]

---

## 7. Aplicaciones: hacia "atlas" moleculares de la vida

Grandes proyectos internacionales para comprender y describir tipos y estados celulares:

- [[Human Cell Atlas]] — al momento de la clase: **70,9 M células, 11,3 k donantes, 532 proyectos, 1k laboratorios**
- [[BRAIN Initiative]] ([[BICCN]])
- [[Malaria Cell Atlas]]

---

## Perspectivas

Las tres preguntas con las que cierra la clase:

1. **¿Cómo definimos molecularmente a una célula?**
2. **¿Podemos predecir el estado de una célula en base a su caracterización molecular?**
3. **¿Podemos intervenir/modificar el estado de una célula?**

---

## Ideas para retener

- El bulk mide **promedios**; el single cell mide **distribuciones**. Toda la potencia analítica viene de ese cambio.
- No medimos expresión: medimos **abundancia de moléculas muestreadas**. Todo el diseño experimental y el QC se derivan de asumir eso.
- [[Barcode celular]] responde *"¿de qué célula?"*; [[UMI]] responde *"¿es una molécula nueva o una copia de PCR?"*. Son preguntas distintas y necesitan etiquetas distintas.
- El cuello de botella del campo se corrió de lo experimental a lo computacional: hoy el límite está en **almacenar, integrar e interpretar**, no en generar datos.

## Conexiones

- Continúa en → [[Biología espacial - mapeando la expresión génica a su entorno]] (qué se pierde al disociar el tejido)
- Índice → [[Módulo 1 - MOC]]
