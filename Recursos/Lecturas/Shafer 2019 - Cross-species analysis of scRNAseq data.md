---
tags: [lectura, modulo-1, single-cell, evolucion, integracion]
area: Lecturas
tipo: perspective
autores: Maxwell E. R. Shafer
año: 2019
revista: Frontiers in Cell and Developmental Biology 7:175
doi: 10.3389/fcell.2019.00175
aliases: [Shafer 2019, Cross-Species Analysis of Single-Cell Transcriptomic Data]
---

# Shafer (2019) — *Cross-Species Analysis of Single-Cell Transcriptomic Data*

> [!info] Ficha de la lectura
> **Tipo:** perspective — *Frontiers in Cell and Developmental Biology*
> **Autor:** Maxwell E. R. Shafer (Biozentrum, Universidad de Basilea)
> **Clase asociada:** [[Aproximaciones ómicas con resolución de célula única]] (clase 1)
> **PDF:** [[Shafer 2019 - Cross-species analysis of scRNAseq data.pdf]]

## En una frase

Comparar datos de [[scRNA-seq]] **entre especies** es un caso extremo de [[Batch effect]]: además del ruido técnico hay que decidir qué genes son "el mismo gen" (ortología) y distinguir tipos celulares homólogos de tipos celulares que convergieron — y todo eso apunta a construir **filogenias de tipos celulares**.

## Por qué leerla después de la clase

La clase deja abiertas dos preguntas: *¿cómo definimos molecularmente a una célula?* y el problema de la [[Identidad celular]]. Shafer las lleva al plano evolutivo: si un tipo celular se define por su programa de expresión, ¿cuándo dos tipos de especies distintas son "el mismo"? Complementa la sección de integración entre especies de [[Stuart and Satija 2019 - Integrative single-cell analysis|Stuart & Satija (2019)]].

---

## 1. El punto de partida: el pipeline estándar

La review resume el flujo de **[[Seurat y Scanpy|Seurat]]** que también muestra la clase: [[Genes altamente variables|genes altamente variables]] → [[PCA]] → [[Clustering]] por grafo de vecinos (modularidad) → t-SNE o [[UMAP]] para visualizar. El producto es una lista de clusters anotados por especie; el problema es **compararlos**.

Nota sobre tecnologías: los métodos de gotas o microwells (y el *combinatorial barcoding* de sci-RNA-seq) ganan **número de células** a costa de **profundidad**, y eso suele identificar mejor la heterogeneidad que secuenciar muy profundo pocas células ([[Smart-seq|Smart-seq2]]).

## 2. Dos estrategias para comparar especies

| | Análisis **separado** | Análisis **combinado** |
|---|---|---|
| Cómo | Se anota cada especie por su lado y después se emparejan clusters | Se integran los datos en un espacio común y se clusteriza todo junto |
| Ventaja | Preserva la heterogeneidad propia de cada dataset | Más células → más poder para encontrar tipos raros |
| Desventaja | Emparejar a mano; el batch persiste | Más complejo; puede **ocultar tipos celulares exclusivos** de una especie |

### Emparejar clusters por separado

- **Índice de especificidad génica** (Tosches et al., 2018): para cada gen y cada tipo celular, expresión en ese tipo / expresión media en todos. Se correlacionan esos índices entre especies (Pearson). No depende de la escala de cuantificación de cada plataforma. Resultado en tortugas, lagartos y mamíferos: las **interneuronas** de mamífero son ancestrales a todos los amniotas, pero la neocorteza está compuesta mayormente por tipos celulares **propios del linaje**.
- **Random forest**: se entrena un clasificador con los tipos celulares de la especie A y se predice a qué tipo de A se parece cada célula de B → **matriz de confusión**. Usado en habénula de pez cebra y retina de ratón.

### Integrar (corregir el batch entre especies)

Los métodos de bulk basados en regresión lineal suponen la **misma composición celular** y un efecto de batch **uniforme** en todos los tipos — dos supuestos falsos en single cell. Los métodos específicos:

| Método | Idea |
|---|---|
| **mnnCorrect / fastMNN** | Pares de vecinos mutuos más cercanos entre datasets → vector de corrección por tipo celular |
| **Seurat (CCA + MNN "anchors")** | Estructura de correlación compartida (CCA), alineada con *dynamic time warping*; en v3 suma MNN como anclas |
| **Scanorama** | MNN generalizado, "cosido panorámico" como en fotos, para reducir sobreajuste |
| **LIGER (iNMF)** | Factoriza la matriz célula × gen en factores **compartidos** y factores **específicos de especie** → identifica tipos comunes *y* qué genes explican las diferencias |
| **Harmony** | Mueve iterativamente células análogas hacia un centroide compartido en el espacio de PCs |
| **Conos** | Grafo unificado sobre muchos datasets; solo conserva conexiones que se repiten |

Riesgo común: el **sobreajuste** que fusiona tipos celulares distintos. Los métodos con MNN lo mitigan porque un tipo celular exclusivo de un dataset no tiene vecino mutuo en el otro.

---

## 3. Los problemas propiamente evolutivos

1. **Ortología.** Solo se pueden usar genes con ortólogo en ambas especies; si se incluyen genes sin par, las células se agrupan **por especie** y no por tipo celular. Pero descartarlos pierde información: los genes **específicos de un clado** impulsan la diversificación de tipos celulares, y tras una **duplicación** una copia puede sub- o neo-funcionalizarse. En especies cercanas (humano/ratón) alcanza con el símbolo del gen; en lejanas, bases como ENSEMBL o BLAST recíproco, con dificultad creciente.
2. **Evolución modular.** Grupos de genes bajo el mismo factor de transcripción cambian juntos; hay que tenerlo en cuenta (o quitar genes muy correlacionados).
3. **Homología vs homoplasia.** Dos tipos celulares pueden parecerse por ancestro común **o** por convergencia (reuso de módulos regulatorios). Separarlos exige muestrear muchas especies a lo largo de la filogenia.
4. **Métodos comparativos filogenéticos.** Especies cercanas comparten más rasgos: las comparaciones no son observaciones independientes, y eso ya se modela en bulk pero no en single cell.

## 4. Cierre

Una definición completa de tipo celular y de su origen evolutivo va a requerir **combinar evidencia**: identidad molecular, función y **linaje** del desarrollo (reconstruido in silico o con barcodes de CRISPR — ver Stuart & Satija).

## Conceptos del vault

[[scRNA-seq]] · [[Genes altamente variables]] · [[Seurat y Scanpy]] · [[Smart-seq]] · [[Identidad celular]] · [[Tipo celular]] · [[Batch effect]] · [[Clustering]] · [[PCA]] · [[UMAP]] · [[Anotación de tipos celulares]] · [[Machine Learning]] · [[Atlas celulares]]

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
- [[Módulo 1 - MOC]]
