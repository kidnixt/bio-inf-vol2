---
titulo: "Métodos para el diseño computacional de fármacos"
curso: Fronteras y Perspectivas en Bioinformática – Universidad ORT
modulo: Módulo 3 - Inteligencia Artificial aplicada a Bioinformática
docente: Andrés Ballesteros
fecha: 2026-09
año: 2026
clase: 6
tags:
  - clase
  - modulo-3
  - diseño-de-fármacos
  - CADD
  - quimioinformática
  - IA
---

# Métodos para el diseño computacional de fármacos

> [!info] Ficha de la clase
> **Curso:** Fronteras y Perspectivas en Bioinformática – Universidad ORT (2026) · **Clase 6**
> **Módulo:** [[Módulo 3 - MOC|Módulo 3 - Inteligencia Artificial aplicada a Bioinformática]]
> **Docente:** [[Andrés Ballesteros]] — Área Bioinformática, DETEMA, [[Facultad de Química (UdelaR)]] · LSBM, [[Institut Pasteur de Montevideo]]
> **Subtítulo:** *Diseño molecular, simulación e inteligencia artificial*
> **Fecha:** setiembre de 2026 (las bases de datos de la clase se consultaron el 09/09/2026)
> **Diapositivas:** [[Diapositivas - Métodos para el diseño computacional de fármacos.pdf]]
> **Resumen de la clase (material del curso):** — no hay
> **Lecturas:** [[Wang et al 2024 - Active learning in drug discovery|Wang et al. 2024]] · [[Fang et al 2026 - A comprehensive review of AI in drug design|Fang et al. 2026]] · [[Nazarova et al 2026 - V-SYNTHES2|Nazarova et al. 2026]] · [[Fahim 2026 - Structure-based design of antiviral and antihypertensive drugs|Fahim 2026]]
> **Clase previa (en el vault):** [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]] — es la primera clase del [[Módulo 3 - MOC|Módulo 3]].

## De qué va la clase

La pregunta que abre y organiza toda la clase:

> **¿Cómo elegimos qué moléculas merece la pena estudiar para desarrollar un tratamiento?**

La respuesta es el [[Diseño de fármacos asistido por computadora|diseño de fármacos asistido por computadora]] (CADD): un conjunto de métodos que **ordenan y priorizan** hipótesis antes de ir al laboratorio. La clase recorre cinco bloques:

1. **Blancos y datos** — qué bases de datos existen y cómo se representa una molécula o una proteína.
2. **[[Diseño basado en ligandos|LBDD]]** — aprender de moléculas con actividad conocida.
3. **[[Diseño basado en estructura|SBDD]]** — diseñar dentro del sitio de unión de un blanco con estructura 3D.
4. **Dinámica y energía** — tratar la proteína como un conjunto de estados, no una foto.
5. **[[Inteligencia Artificial]]** — qué cambió y qué sigue dependiendo de la física y el experimento.

La idea que atraviesa todo: **ningún método es "el bueno"**. La información disponible decide la ruta, y el éxito siempre fue un sistema (hipótesis computacional + química + ensayo + desarrollo), nunca un algoritmo solo.

> [!abstract] Cómo leer este resumen
> Sigue la estructura de las diapositivas. Esta clase no tiene PDF de resumen del curso, así que no hay recuadros *"En la clase"*: todo lo que está acá sale de las diapositivas, con lo implícito de las figuras explicado.

---

## 1. Diseño de fármacos y desarrollo de medicamentos

### El recorrido de una molécula

> El diseño de fármacos busca **moléculas capaces de modificar un proceso biológico de manera útil**.

El [[Descubrimiento y desarrollo de fármacos|desarrollo de un medicamento]] se presenta como una línea de cinco etapas:

| # | Etapa | Qué se evalúa |
|---|---|---|
| 01 | **Descubrimiento / Diseño** | Blanco, *hit* y *lead* |
| 02 | **Preclínica** | Exposición y seguridad |
| 03 | **Clínica I–III** | Personas y beneficio |
| 04 | **Evaluación** | Calidad y evidencia |
| 05 | **Seguimiento** | Seguridad en uso real |

Tres palabras que vuelven en toda la clase:

- **Hit:** molécula con **actividad confirmada** frente al blanco.
- **Lead:** una **serie** (familia de moléculas relacionadas) con **potencial de optimización**.
- **Candidato:** molécula con el **perfil para avanzar en desarrollo**.

> Afinidad y potencia ayudan. **La exposición y la seguridad condicionan el beneficio.**

Es decir: una molécula que se une muy fuerte al blanco pero no llega al tejido, o es tóxica, no sirve. El diseño computacional trabaja casi todo en la etapa 01, pero tiene que anticipar lo que se va a medir después.

### Blancos y mecanismos de acción

Un [[Blanco terapéutico|blanco o diana]] es **una entidad biológica cuya modificación puede producir un efecto terapéutico**:

| Tipo de blanco | Qué hace | Cómo se lo modula |
|---|---|---|
| **Enzima** | Acelera una reacción química | Un **inhibidor** puede reducir esa actividad |
| **Receptor** | Reconoce señales | Un **agonista** activa una respuesta; un **antagonista** puede bloquearla |
| **Canal o transportador** | Controla el paso de sustancias a través de una membrana | — |
| **Ligando** | Molécula que se une a un blanco | La unión puede modificar su función |

> La pregunta terapéutica incluye **qué** modificar, **en qué dirección** y **dónde**.

### Cómputo y experimento: un ciclo compartido

| Cómputo (*in silico*) | Experimento |
|---|---|
| Predice actividad y propiedades | Sintetiza y verifica identidad |
| Propone estructuras y modificaciones | Mide unión, función y exposición |
| Prioriza candidatos y experimentos | Evalúa selectividad y toxicidad |

Los dos lados comparten un ciclo: **diseñar → sintetizar → medir → aprender** (el equivalente farmacológico del [[Ciclo DBTL]] de la clase 5). Y hay cuatro propiedades que el ciclo intenta optimizar a la vez:

| Propiedad | Qué mide |
|---|---|
| **Afinidad** | Fuerza de unión al blanco (ver [[Energía libre de unión]]) |
| **Potencia** | Concentración necesaria para un efecto |
| **Selectividad** | Preferencia entre blancos (unirse al que quiero y no a otros) |
| **[[ADMET]]** | Destino en el organismo (absorción, distribución, metabolismo, excreción) y toxicidad |

### La decisión central

> **¿Qué molécula sintetizaríamos mañana?**

La diapositiva lo muestra con dos números: **10⁶ moléculas** posibles frente a **10 experimentos** que se pueden hacer. La computadora **ordena y prioriza**; el laboratorio **determina qué hipótesis son viables**. Toda la clase es sobre cómo hacer bien ese embudo.

### Diseño en computadora: aportes y límites

| Aportes | Límites |
|---|---|
| Prioriza blancos y moléculas | Depende de datos y supuestos |
| Compara hipótesis **antes de sintetizar** | Puede **extrapolar fuera de dominio** |
| Integra señales que vienen de escalas distintas | Necesita controles y **medición experimental** |

Las etapas donde interviene: (1) **identificación del blanco** (tratable y seguro) → (2) **identificación de *hits*** (señal reproducible) → (3) **optimización de *leads*** (serie optimizable) → (4) estudios preclínicos → (5) pruebas clínicas. El cómputo vive sobre todo en las tres primeras. Y un recordatorio clave: **cada resultado puede obligar a volver a una etapa anterior**.

---

## 2. CADD: el mapa general

El [[Diseño de fármacos asistido por computadora|CADD]] (*Computer-Aided Drug Design*) tiene dos grandes ramas, según qué información se tenga:

| | [[Diseño basado en ligandos\|LBDD]] | [[Diseño basado en estructura\|SBDD]] |
|---|---|---|
| **Idea** | Aprende de ligandos conocidos | Usa la estructura del blanco |
| **Métodos** | [[Similitud química\|Similitud]] · [[Farmacóforo\|farmacóforo]] · [[QSAR]] · [[Virtual screening\|VS]] | [[Docking molecular\|Docking]] · [[Dinámica molecular\|MD]] · [[Energía libre de unión\|energía libre]] |
| **Flujo** | Datos (activos e inactivos) → representar (descriptores o grafos) → aprender (regla o modelo) → priorizar (nuevas moléculas) | Estructura (proteína o complejo) → preparar (protonación y aguas) → explorar (poses y conformaciones) → evaluar (score, física, ensayo) |
| **Pregunta típica** | *¿Qué compuestos se parecen a patrones asociados con actividad?* | *¿Cómo podría una molécula reconocer y modular este sitio?* |
| **Fortaleza** | Aprovecha datos | Propone un mecanismo 3D |
| **Riesgo** | Extrapolar fuera del dominio | Estructura o score incorrectos |

> La pregunta y los datos disponibles determinan la ruta.

### ¿LBDD o SBDD? La información decide

| Qué conocemos | Ruta | Herramientas |
|---|---|---|
| Ligandos activos | **LBDD** | Similitud, farmacóforo, QSAR |
| La estructura 3D | **SBDD** | Sitio de unión, docking, dinámica molecular |
| Ambos | **Combinación** | Modelo, pose, síntesis y ensayo |
| Muy poco | **Generar evidencia** | Biología, cribado y medición |

> **No es una competencia entre métodos: es una decisión condicionada por evidencia.**

En una situación real se combinan las dos rutas: LBDD aporta **patrones en datos**, SBDD aporta **hipótesis de unión**, el experimento aporta **medición**, y la evidencia nueva vuelve a alimentar ambos modelos.

### Casos de éxito: el método fue parte de un sistema

| Año | Fármaco / caso | Ruta | Qué se hizo |
|---|---|---|---|
| 1993 | **Zanamivir** | SBDD | Diseño racional sobre la neuraminidasa (gripe) |
| 2019 | **DRD4** | SBDD + VS | Docking de **138 millones** de moléculas; nuevos quimiotipos |
| 2020 | **Halicina** | LBDD + IA | Modelo fenotípico y validación antibacteriana |
| 2021 | **Nirmatrelvir** | SBDD + química | Inhibidor oral de Mpro (proteasa principal del SARS-CoV-2) |

> **Éxito = hipótesis computacional + química + ensayo + desarrollo.**

Detalle de cada caso en [[Casos de éxito del diseño computacional de fármacos]].

---

## 3. Blancos y datos

> ¿Cómo convertimos una enfermedad compleja en una hipótesis tratable?

Una base de datos **organiza objetos e identificadores, conserva información sobre su procedencia y permite recuperarlos de manera consistente**. La elección depende de la pregunta biológica.

### Bases de datos en CADD y diseño guiado por IA

| Necesidad | Bases | Para qué |
|---|---|---|
| **Bibliotecas químicas** | [[ZINC]] y [[PubChem]] | Buscar, representar y seleccionar moléculas |
| **Actividad y farmacología** | [[ChEMBL]], [[BindingDB]] y [[DrugBank]] | Aprender de ensayos y de fármacos conocidos |
| **Proteínas y estructuras** | [[UniProt]], [[PDB]] y [[AlphaFold DB]] | Identificar blancos y estudiar su geometría |
| **Estructura con afinidad** | [[PDBbind]] | Relacionar un complejo 3D con una medición |

La clase dedica una diapositiva a cada base con el mismo formato (propietario, tamaño, qué datos ofrece, cómo se usa, ejemplo de consulta y una advertencia). Resumido:

| Base | Quién | Qué ofrece | Consulta típica | Advertencia |
|---|---|---|---|---|
| [[ZINC]] | UCSF, grupos de John Irwin y Brian Shoichet | Estructuras 2D/3D, propiedades, referencias a proveedores | *¿Qué moléculas puedo comprar o encargar para evaluar este sitio?* | Un catálogo de síntesis bajo pedido **no** es un inventario físico ni actividad demostrada |
| [[PubChem]] | NCBI, NLM, NIH (EE.UU.) | Compuestos, bioactividad, propiedades fisicoquímicas, referencias | *¿Cuál es la identidad de esta molécula y qué ensayos la describen?* | Un compuesto puede tener varias entradas y múltiples resultados de ensayo |
| [[ChEMBL]] | EMBL-EBI (Reino Unido) | Compuestos, ensayos, blancos, bioactividades, ADMET, fármacos | *¿Qué compuestos tienen actividad medida frente a este blanco?* | Ki, Kd, IC50 y respuestas celulares requieren interpretación y curación |
| [[BindingDB]] | UC San Diego, equipo de Michael Gilson | Afinidades medidas, estructuras, proteínas, condiciones | *¿Qué afinidades se han medido para esta familia de ligandos?* | Comparte datos con ChEMBL |
| [[DrugBank]] | U. of Alberta y OMx Personal Health Analytics (Canadá) | Fármacos, blancos, mecanismos, indicaciones, metabolismo, interacciones | *¿Qué mecanismo, blancos e interacciones tiene este fármaco?* | Incluye fármacos experimentales y retirados; el acceso depende del producto |
| [[UniProt]] | Consorcio UniProt: EMBL-EBI, SIB y PIR | Secuencias, funciones, dominios, variantes, referencias cruzadas | *¿Qué secuencia, función y variantes corresponden a este blanco?* | — |
| [[PDB]] | wwPDB (RCSB PDB, PDBe, PDBj) | Coordenadas 3D, ligandos, método experimental, validación | *¿Hay estructuras experimentales del blanco con ligandos unidos?* | Una entrada es **una** estructura; una proteína puede aparecer en muchos complejos |
| [[AlphaFold DB]] | EMBL-EBI y Google DeepMind | Modelos de monómeros y complejos, métricas de confianza | *¿Qué modelo estructural existe y qué regiones tienen mayor confianza?* | La confianza depende del modelo; índice y descargas tienen coberturas distintas |
| [[PDBbind]] | Equipo de Renxiao Wang (Fudan University), portal con TopScience | Complejos 3D con afinidades experimentales | *¿Qué complejos 3D disponen de una afinidad experimental asociada?* | Estructura, ligando y medida deben corresponder; versiones recientes son pagas |

### Tamaño de las bases (corte de setiembre de 2026)

| Base | Tipo de registro | Cantidad | Versión o consulta |
|---|---|---|---|
| ZINC | Moléculas 2D | ≈ 54.900.000.000 | Portal, 09/09/2026 |
| PubChem | Compuestos (CID) | 124.663.908 | Entrez, 09/09/2026 |
| ChEMBL | Compuestos | 2.921.148 | v37, 29/05/2026 |
| BindingDB | Compuestos con datos de afinidad | 1.440.011 | 202609, 30/08/2026 |
| DrugBank | Entradas de fármacos | 20.161 | Portal, 09/09/2026 |
| PDB | Estructuras | 259.747 | Archivo, 09/09/2026 |
| UniProt | Secuencias UniProtKB | 150.006.383 | 2026_03, 02/09/2026 |
| AlphaFold DB | Modelos indexados (monómeros y complejos) | 261.247.178 | Índice, 09/09/2026 |
| PDBbind | Complejos proteína–ligando | 29.001 | v2025, 08/02/2026 |

Lo que salta a la vista: hay **tres órdenes de magnitud** entre el espacio químico enumerable (decenas de miles de millones de moléculas en ZINC) y lo que tiene actividad medida (millones en ChEMBL/BindingDB), y otros tres hasta lo que tiene **estructura + afinidad** (29 mil complejos en PDBbind). Esa escasez de datos "completos" es la que condiciona todo lo que viene después. También: hay **más estructuras predichas (AlphaFold DB) que secuencias en UniProtKB** en este corte, y ~1000 veces más que estructuras experimentales en el PDB.

### Menciones por año en la literatura

Un gráfico de publicaciones en PubMed/Europe PMC que mencionan cada base en el contexto de descubrimiento de fármacos (2000–2026, 2026 parcial hasta el 9 de setiembre):

- Todas son marginales hasta ~2010 y crecen fuerte **a partir de 2019–2020**.
- **PubChem, ChEMBL y DrugBank** encabezan en los últimos años (del orden de 150–200 menciones anuales); el **PDB** es el que tiene la historia más larga y estable.
- **UniProt** y **AlphaFold DB** suben después de 2020; **BindingDB** y **PDBbind** quedan más abajo.

> [!warning] Cómo leer ese gráfico
> Son **menciones recuperadas**, no citas al artículo de la base ni número de usuarios. Y 2026 es un acumulado parcial, que no se debe extrapolar al cierre del año.

### Representaciones moleculares

> **La representación decide qué diferencias puede aprender el modelo.**

Las [[Representaciones moleculares]] van de lo más ligero a lo más rico:

| Representación | Qué es | Ejemplo | Ventaja |
|---|---|---|---|
| **Propiedades fisicoquímicas** | Texto/numérico | logP, peso molecular | Ligero |
| **SMILES** | Texto químico | `O=C(O)c1ccccc1O` (ácido salicílico) | Ligero y secuencial |
| **Fingerprint** | Vector de bits de subestructuras | MACCS: 166 bits (anillo aromático, –OH, C=O…) | Rápido para similitud |
| **Grafo molecular** | Átomos (nodos) y enlaces (aristas) | — | Aprendizaje local |
| **Confórmero 3D** | Geometría | Varios confórmeros de la misma molécula | Interacciones espaciales |

La diapositiva lo muestra con una sola molécula, el **ácido salicílico**, escrita de cuatro maneras: SMILES, fingerprint MACCS, grafo molecular numerado y tres confórmeros 3D.

Una variante de uso de las propiedades fisicoquímicas son los **filtros**: las [[Reglas de drug-likeness]], de las cuales la más conocida es la **regla de los cinco de Lipinski** (MW ≤ 500 Da, ≤ 10 aceptores y ≤ 5 donores de puente de hidrógeno, cLogP ≤ 5). La tabla de la clase suma otras (Ghose, Oprea, Veber, REOS, *beyond rule of five*, *rule of three* de Congreve) y hasta variantes para agroquímicos (*herbicide-likeness*, *insecticide-likeness*, regla de Hao para pesticidas).

### Representaciones de proteínas

Del lado del blanco, también hay niveles:

| Nivel | Qué captura | Herramientas |
|---|---|---|
| **Secuencia** | Motivos y evolución | [[Modelo de lenguaje de proteínas\|Modelos de lenguaje]] |
| **Estructura** | Forma y contactos | [[Docking molecular\|Docking]] y simulaciones |
| **Ensamble** | Estados y poblaciones | [[Dinámica molecular\|MD]] y muestreo |
| **Contexto celular** | Expresión y redes | Priorización de blancos |

La fila "Secuencia → modelos de lenguaje" es exactamente el tema de la clase 9: [[Modelos de lenguaje de proteínas y embeddings proteicos]].

---

## 4. LBDD: aprender de ligandos

> ¿Qué podemos inferir cuando conocemos moléculas y actividades?

### Similitud química

- **Hipótesis:** moléculas parecidas tienden a compartir actividad.
- **Riesgo:** un cambio pequeño puede producir un [[Activity cliff|*activity cliff*]].

La [[Similitud química]] se mide comparando fingerprints. La métrica estándar es el **coeficiente de Tanimoto**:

$$T_c = \frac{c}{a + b - c}$$

donde *a* y *b* son los bits encendidos en cada molécula y *c* los que comparten. El ejemplo de la clase: dos moléculas (A y B) que comparten un anillo fenólico y un grupo amino, pero A tiene además un ácido carboxílico:

```
A: 0 1 0 1 0 1     (3 bits encendidos)
B: 0 1 0 1 0 0     (2 bits encendidos)
       ^   ^       (2 en común)

Tc = 2 / (3 + 2 − 2) = 0.66
```

Hay otras métricas (Euclídea, Manhattan/Hamming, Dice, coseno, Russell–Rao, Forbes, Soergel), con rangos distintos; Tanimoto va de 0 a 1.

### Farmacóforos

Un [[Farmacóforo]] **abstrae la molécula como un patrón espacial de interacciones**: donor y aceptor de puente de hidrógeno, zona hidrofóbica, anillo aromático, grupo ionizable. El ejemplo: del **ácido salicílico** se extrae un triángulo de tres rasgos (aromático, aceptor de H, ionizable negativo) con sus distancias d₁, d₂, d₃; el **ácido acetilsalicílico** (aspirina) cumple ese patrón → *match*.

Es útil **cuando ligandos distintos comparten un modo de unión**, aunque no se parezcan como moléculas.

### QSAR

El [[QSAR]] (*relación cuantitativa entre estructura y actividad*) es un modelo supervisado:

```
estructura química → descriptores (X) → modelo ŷ = f(X) → actividad predicha
```

El ejemplo de la diapositiva: cinco moléculas con actividad experimental (7,2; 6,5; 5,9; 7,8; 6,1), descritas por MW, LogP, HBD, HBA y TPSA. Se separan en entrenamiento (70 %) y prueba (30 %), se ajusta el modelo, se evalúa con **R², Q² y RMSE** (gráfico predicho vs. observado) y se aplica a una molécula nueva: **pIC₅₀ = 6,8**.

### *Activity cliffs*

| Estructura | Actividad |
|---|---|
| Molécula A | **12 nM** |
| Molécula A + CH₃ | **8,4 µM** |

Un solo metilo empeora la actividad **700 veces**. Un [[Activity cliff]] es exactamente eso: **pequeña diferencia estructural, gran cambio biológico**. Es la falla de la hipótesis de similitud, y la razón por la que un modelo LBDD puede equivocarse feo justo donde parece más seguro.

### Virtual screening

El [[Virtual screening]] (VS) es la herramienta que usa el descubrimiento moderno de fármacos para **identificar nuevos *leads* y moléculas similares a fármacos** para intervenciones terapéuticas. Se dibuja como un **embudo**: cada nivel aplica un filtro más caro sobre menos moléculas, hasta llegar a las que se compran o sintetizan.

---

## 5. SBDD: la estructura del blanco

> ¿Qué cambia cuando conocemos o predecimos la forma tridimensional del blanco?

### ¿Cómo obtenemos la estructura de una proteína?

| Método experimental | Qué permite |
|---|---|
| **Cristalografía de rayos X** | Estructuras de alta resolución a partir de cristales de proteína |
| **RMN** (resonancia magnética nuclear) | Determinar estructuras **en solución**, con campos magnéticos |
| **Cryo-EM** (criomicroscopía electrónica) | Visualizar estructuras a nivel nanométrico **sin cristalizar** |

### ¿Y si la estructura no está en el PDB?

| Método predictivo | Cómo funciona |
|---|---|
| **[[Modelado por homología]]** | Compara la secuencia objetivo con proteínas de estructura conocida y transfiere la estructura por similitud |
| **[[Threading]]** | Alinea la secuencia contra estructuras de referencia, "encajándola" en un marco estructural conocido |
| **Métodos basados en IA** | [[AlphaFold]], basado en redes neuronales |

### AlphaFold cambió la disponibilidad estructural

| 2021 | 2024 |
|---|---|
| **AlphaFold2** amplió el acceso a modelos de proteínas | **AlphaFold3** abordó complejos con **ligandos, ácidos nucleicos e iones** |

Las predicciones de AlphaFold3 sobre cómo las proteínas se unen a ligandos coinciden estrechamente con los datos experimentales.

| Fortalezas de AlphaFold3 | Precauciones |
|---|---|
| Predicción **conjunta** de los componentes del complejo | Dependencia del entrenamiento |
| Mejor desempeño en varios *benchmarks* | Estados biológicos alternativos |
| Confianza por región e interfaz | **La afinidad sigue siendo difícil** |

Esa última fila es la bisagra de la clase: predecir *dónde* y *cómo* se une algo no es lo mismo que predecir *cuán fuerte* se une.

### Docking como problema de búsqueda

El [[Docking molecular]] se plantea en dos mitades:

1. **Generar poses** — explorar traslación, rotación y torsiones del ligando dentro del sitio.
2. **Ordenar poses** — agrupar (*clustering*) y clasificar las poses generadas.

### Flexibilidad del receptor

| Tratamiento | Costo | Qué representa |
|---|---|---|
| **Rígido** | Rápido | Un estado |
| ***Side chains*** | Intermedio | Ajuste local |
| ***Ensemble*** | Mayor costo | Estados discretos |
| ***Induced fit*** | Costoso | Cambio acoplado |

> Más flexibilidad aumenta la precisión **y** el espacio de búsqueda.

### Funciones de puntuación

Una [[Función de puntuación|función de scoring]] combina términos: **estérico**, **electrostático**, **puente de hidrógeno**, **hidrofobia** y **desolvatación**, y devuelve un *score* que sirve como **ranking dentro del protocolo**.

> [!warning] El score no es ΔG
> **No equivale automáticamente a la ΔG experimental.** Sirve para ordenar hipótesis dentro de un mismo protocolo, no como predicción de afinidad absoluta.

### VS jerárquico

El embudo con números:

| Nivel | Moléculas |
|---|---|
| Biblioteca | 10⁸–10¹⁰ |
| Docking rápido | 10⁵ |
| *Rescoring* | 10³ |
| **Ensayo** | **10–100** |

Siete a nueve órdenes de magnitud entre lo que se puede enumerar y lo que se puede medir.

### Caso de estudio: inhibidores de α-glucosidasa

Un trabajo que combina LBDD convencional y cribado virtual (Kushavah et al., *J. Mol. Model.* 30, 389, 2024).

**Objetivo:** identificar nuevos inhibidores de α-glucosidasa a partir de una serie conocida de **xantonas** y una biblioteca comercial.

**Flujo completo:**

```
51 xantonas → alineamiento 3D → farmacóforo → 3D-QSAR (PLS)
   → biblioteca Maybridge → docking con Glide → MD + bioensayo
```

El farmacóforo y el 3D-QSAR **reducen** la biblioteca; el docking **examina la pose**; el ensayo **confirma la actividad**.

**Resultados:** 51 xantonas iniciales → **8 compuestos** seleccionados para evaluación biológica → **4 compuestos activos** estudiados mediante [[Dinámica molecular|MD]].

### Caso 1: DRD4 y cribado ultragrande

El receptor dopaminérgico D4 (Lyu et al., *Nature* 2019):

| | |
|---|---|
| **138 M** | moléculas dockeadas |
| **81** | quimiotipos nuevos |
| **30** | activos submicromolares |
| **180 pM** | agonista optimizado |

Es el caso que muestra qué pasa cuando el embudo empieza con **cientos de millones** en lugar de decenas de miles.

---

## 6. Dinámica y energía

> ¿Qué cambia cuando tratamos la proteína como un conjunto de estados?

### Docking vs. dinámica molecular

El ejemplo de la clase es deliberadamente minimalista: **metanol (CH₃OH)** en un sitio de unión.

| | [[Docking molecular\|Docking]] | [[Dinámica molecular\|Dinámica molecular]] |
|---|---|---|
| Qué muestra | Una pose seleccionada | La misma molécula en distintos tiempos (t₀, t₁, … tₙ) |
| Resultado | Pose + puntuación | Trayectoria temporal |
| Qué describe | Una configuración | Movimiento y cambios en las interacciones |

En la MD, **el solvente y los residuos del sitio también cambian de posición**: no es solo el ligando el que se mueve. El docking sugiere una pose; la MD evalúa **cómo cambia con el tiempo**.

### Energía libre de unión

```
Afinidad ←→ ΔG° ←→ Kd
más favorable        menor Kd
```

> La relación termodinámica es **exacta**. La **estimación computacional** conserva incertidumbre.

Ver [[Energía libre de unión]].

### LBDD aplicado: *p*-quinonas contra Chagas

Trabajo del propio docente (Ballesteros-Casallas et al., *Eur. J. Med. Chem.* 2023): *Mode of action of p-quinone derivatives with trypanocidal activity studied by experimental and in silico models*.

**Diseño:** 19 compuestos en cuatro series (I–IV), derivados de *p*-quinonas con variaciones de anillo (naftoquinonas, benzofuranos, benzotiazoles, benzoxazoles) y sustituyentes ariloxi.

**Laboratorio húmedo** (el ciclo completo, 19 compuestos por etapa):

```
Bioactividad T. brucei (x19, tripomastigotes)
   → Bioactividad T. cruzi DM28c-luc (x4, amastigotes)
   → Biosensor redox hGrx-roGFP2 (x19)
   → Cálculos QM-DFT (x19)
```

**Resultado:** **4 hits** para *T. brucei* (compuestos 6, 9, 11, 14) y **2 hits** para *T. cruzi* (11 y 14), con EC₅₀ del orden de 0,9–2,7 µM y buenos índices de selectividad frente a macrófagos.

**Cálculos QM para obtener descriptores:** se calculan ΔG de formación de la **semiquinona** (Q·⁻) y de la **hidroquinona** (QH₂), y las energías de los orbitales **HOMO, LUMO y SUMO**, con base 6-311+G\*\* en todos los átomos, funcional M05-2X y solvente implícito SMD. Esos descriptores alimentan QSAR-2D, QSAR-3D y correlaciones.

**Lo que sale del QSAR:** grupos voluminosos y con carga negativa favorecen la actividad; grupos donores de electrones la mejoran; los anillos furano (serie II) y tiazol (serie III) son deseables y el benceno se tolera menos; el bromo se tolera bien en las series II y III; el sustituyente ariloxi es **perjudicial** para la actividad.

Es el ejemplo de que el "descriptor" no tiene que ser un fingerprint: puede ser una **energía calculada con química cuántica**, y eso conecta el LBDD con la física del mecanismo (en este caso, el ciclo redox de la quinona).

### Búsqueda computacional de blancos moleculares

El problema **inverso** al docking clásico: se tiene una molécula activa y se busca **contra qué blanco actúa**. Los nombres: [[Cribado virtual inverso|RVS (reverse virtual screening), target fishing, inverse docking]].

Segundo trabajo del docente (Ballesteros-Casallas et al., *Eur. J. Med. Chem. Reports* 2022), sobre derivados de **2,7-diarilpirazolo[1,5-a]pirimidina** con actividad antitumoral, sintetizados sin solvente (180 °C, microondas, 2 min, 9 ejemplos, 88–97 % de rendimiento).

El flujo es otro embudo, pero de **proteínas** en vez de moléculas:

```
PharmMapper → 379 PDB
   → Filtro 1: blanco común (75 % de las moléculas) → 178 PDB
   → Filtro 2: Docking XP + MM-GBSA
   → Filtro 3: 30 % top score → 45 proteínas
   → Filtro 4: blanco común (75 %) → 18 proteínas
   → control con moléculas inactivas + evidencia biológica → 7 proteínas
```

Del lado derecho, con las proteínas candidatas se caracterizan los sitios de unión y se hace **crecimiento de ligandos** (*growth of ligands*) para proponer moléculas nuevas. Los mejores scores del ejemplo: Glide_XP entre −10,7 y −14,0 con MM-GBSA entre −67,8 y −114,0 kcal/mol.

---

## 7. Inteligencia artificial

> ¿Qué cambió y qué sigue dependiendo de la física y el experimento?

### ¿Qué significa *AI-driven drug design*?

```
Datos → Modelo → Candidatos → Ensayo
   ↑_______________________________|
   la medición actualiza el modelo
```

> **IA-driven no significa 'IA sola': significa un ciclo de decisión guiado por aprendizaje.**

Es la misma estructura del ciclo diseñar–sintetizar–medir–aprender del principio de la clase, con el modelo en el lugar de la intuición del químico.

### Dónde interviene la IA en el CADD

| Etapa del CADD | Enfoque convencional | Aporte de la IA |
|---|---|---|
| **Representación molecular** | Descriptores y *fingerprints* definidos previamente | Representaciones **aprendidas** desde SMILES, grafos y estructuras 3D |
| **Predicción de propiedades** | Un modelo para cada propiedad | Modelos **multitarea** y **preentrenados** |
| **Exploración del espacio químico** | Búsqueda y puntuación de bibliotecas predefinidas | **Generación** de moléculas y priorización simultánea |
| **Modelado estructural** | Estructuras experimentales, modelado y docking | Predicción de estructuras, complejos, poses y afinidades |
| **Selección experimental** | Selección manual en rondas sucesivas | [[Aprendizaje activo]]: selecciona los compuestos **más informativos** |

> La IA puede intervenir en **todo el ciclo**: representa, predice, diseña y guía el siguiente experimento.

En el esquema del *Traditional Drug Design Workflow*, el diseño basado en IA se dibuja como una flecha que realimenta las etapas 2 (identificación de hits) y 3 (optimización de leads).

Del lado estructura–ligando, la IA aparece en cuatro lugares a la vez: **predicción del sitio de unión**, **predicción de la pose**, **función de scoring** y **cribado virtual mejorado**. La literatura de predicción/generación de poses ya es una familia entera: DiffDock (difusión), KarmaDock y CarsiDock (GNN + MDN, transformers), Uni-Mol, EquiBind, E3Bind, SurfDock, NeuralPLexer, AlphaFold3 y RoseTTAFold All-Atom — casi todos entrenados sobre [[PDBbind]] y evaluados sobre PoseBusters, CASF-2016 o DEKOIS.

### Cofolding

El [[Cofolding|co-plegado]] es predecir **el complejo entero de una sola vez**, en lugar de predecir la proteína y después dockear el ligando:

```
secuencias y componentes → modelo conjunto → complejo 3D
```

Modelos: **[[AlphaFold|AlphaFold3]]**, **Boltz-1/Boltz-1x**, **NeuralPLexer** y **RoseTTAFold All-Atom**. La figura compara estructuras de rayos X con predicciones de Boltz-1x superpuestas.

### QSAR con deep learning

El contraste entre el **QSAR tradicional** (descriptores → espacio químico → modelo → interpretación humana) y el **deep learning** (representaciones 1D/2D/3D/4D: SMILES, grafo molecular, confórmero, ensamble y evolución temporal → **espacio de embeddings** aprendido → *machine insight*). Es la misma jugada que el [[Módulo 3 - MOC|módulo]] repite en la clase 9 con proteínas: reemplazar descriptores diseñados a mano por representaciones aprendidas.

### Aprendizaje activo

> El [[Aprendizaje activo]] (AL) es un proceso **dinámico e iterativo de retroalimentación** que identifica y selecciona de manera eficiente los datos **más valiosos** dentro del espacio químico para ser etiquetados o evaluados.

El ciclo: datos seleccionados → entrenar el algoritmo → predicción con probabilidad → elegir *k* pares del pool no etiquetado → experimentos para obtener etiqueta → volver a entrenar. Las preguntas de diseño que plantea la figura: qué representación usar para fármacos y células, qué arquitectura, cómo elegir los pares y cuál es el impacto de *k*.

Aplicaciones en descubrimiento de fármacos: predicción de interacción compuesto–blanco (con datos desbalanceados), cribado virtual (ayudar al LBVS a encontrar *scaffolds* nuevos, *scaffold hopping*), generación y optimización de moléculas, y predicción de propiedades.

### VS + ML

Un ejemplo concreto de pipeline híbrido (sobre MAO):

- Los ligandos de MAO de **[[ChEMBL]]** se dockean y se generan **hipótesis farmacofóricas** de las mejores moléculas.
- En paralelo, los **fingerprints** (Avalon, Morgan, MACCS, Mordred, RDKit) y descriptores entrenan modelos de ML (**RF, SVM, ANN**) que predicen actividad y puntuaciones de docking.
- Los farmacóforos y los modelos de unión filtran **[[ZINC]]** para identificar los compuestos más prometedores.

### V-SYNTHES2

Cribado virtual en bibliotecas químicas de escala masiva (Nazarova et al., 2026): **3,8 M dockings aproximados** para representar un espacio de **36 mil millones** de moléculas. Cómo: enumeración jerárquica (biblioteca de enumeración mínima a partir del REAL Space, con fragmentos "capados"), selección geométrica de fragmentos (descartar los que chocan, quedarse con los prometedores), y validación prospectiva en dos blancos.

### Halicina: deep learning y reposicionamiento

| | |
|---|---|
| **2.335** | moléculas en el conjunto inicial |
| **> 107 M** | moléculas evaluadas virtualmente |

Una red neuronal de paso de mensajes (*directed message passing*) entrenada sobre un conjunto chico predijo actividad antibiótica sobre el Drug Repurposing Hub y la base ZINC15. **El modelo priorizó un candidato inesperado** —la halicina, un compuesto desarrollado originalmente para diabetes— **que después se validó**: bactericida de amplio espectro, activo contra *Acinetobacter baumannii* y *Clostridioides difficile*.

Es el caso emblemático de LBDD + IA: sin estructura, sin mecanismo, solo fenotipo y aprendizaje.

---

## 8. Cierre: cinco reglas para interpretar resultados

La clase cierra con las reglas que ordenan todo lo anterior:

1. **Cada método responde una pregunta concreta.**
2. **El *score* ordena hipótesis dentro de un protocolo** (no es una afinidad absoluta).
3. **La incertidumbre debe acompañar la predicción.**
4. **Física, IA y experimento funcionan mejor conectados.**

## Ideas para retener

- El problema real es de **priorización**: 10⁶ moléculas posibles contra 10 experimentos posibles. El cómputo ordena, el laboratorio decide.
- **[[Diseño basado en ligandos|LBDD]] vs. [[Diseño basado en estructura|SBDD]] no es una competencia**: es una decisión condicionada por la evidencia disponible. Si hay ligandos activos → LBDD; si hay estructura 3D → SBDD; si hay ambos → combinación; si no hay nada → generar evidencia.
- **La representación decide qué puede aprender el modelo**, tanto para moléculas (propiedades → SMILES → fingerprint → grafo → 3D) como para proteínas (secuencia → estructura → ensamble → contexto celular).
- Hay **órdenes de magnitud de distancia** entre el espacio químico enumerable (≈5·10¹⁰ en [[ZINC]]), lo que tiene actividad medida (≈3·10⁶ en [[ChEMBL]]) y lo que tiene estructura + afinidad (2,9·10⁴ en [[PDBbind]]). Esa asimetría condiciona qué modelos se pueden entrenar.
- Los [[Activity cliff|activity cliffs]] son el contraejemplo permanente a la hipótesis de similitud: un metilo puede costar tres órdenes de magnitud de actividad.
- Un **score de docking no es una ΔG experimental**. Ordena dentro de un protocolo.
- **[[AlphaFold]] cambió la disponibilidad estructural** (más modelos predichos que secuencias en UniProtKB), pero **la afinidad sigue siendo difícil**.
- **IA-driven no es IA sola**: es un ciclo de decisión guiado por aprendizaje, donde la medición actualiza el modelo. El [[Aprendizaje activo]] es la forma explícita de ese ciclo.

## Lecturas de la clase

| Lectura | Qué aporta |
|---|---|
| [[Wang et al 2024 - Active learning in drug discovery]] | La revisión detrás de la diapositiva de [[Aprendizaje activo]]: los cuatro componentes de un ciclo y la distinción explorar/explotar |
| [[Fang et al 2026 - A comprehensive review of AI in drug design]] | El mapa completo del AIDD (es el DOI que aparece en la diapositiva "Mapa de la IA en descubrimiento"), con una sección sistemática sobre **métricas de evaluación** |
| [[Nazarova et al 2026 - V-SYNTHES2]] | El paper de V-SYNTHES2, con la crítica a los modelos sustitutos: si cambiás de score a mitad del embudo, cambiaste de protocolo |
| [[Fahim 2026 - Structure-based design of antiviral and antihypertensive drugs]] | La versión larga de la diapositiva de casos de éxito: captopril, aliskiren, los inhibidores de proteasa del VIH, oseltamivir y Paxlovid, caso por caso |

## Conexiones

- Viene de → [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]] (clase 5, último del Módulo 2). El paralelo es directo: allá el [[Ciclo DBTL]] con modelos metabólicos, acá el ciclo diseñar–sintetizar–medir–aprender con modelos moleculares. En los dos casos, el cómputo **propone** y el laboratorio **valida**.
- Va hacia → [[Modelos de lenguaje de proteínas y embeddings proteicos]] (clase 9). La fila "secuencia → modelos de lenguaje" de la tabla de representaciones de proteínas es exactamente el tema de esa clase; y la lógica "reemplazar descriptores hechos a mano por representaciones aprendidas" es la misma que allá se aplica a las proteínas.
- Del Módulo 1 → el [[Basecalling]] de nanoporos y la [[Segmentación celular]] ya eran problemas de [[Deep Learning]]; acá el deep learning pasa de ser una herramienta de procesamiento a ser el motor del diseño.
- Índice → [[Módulo 3 - MOC]]
