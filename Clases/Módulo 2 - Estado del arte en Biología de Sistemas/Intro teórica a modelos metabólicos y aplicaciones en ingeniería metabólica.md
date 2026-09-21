---
titulo: "Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica"
curso: Fronteras y Perspectivas en Bioinformática – Universidad ORT
modulo: Módulo 2 - Estado del arte en Biología de Sistemas
docente: Ingrid Persitz
fecha: 2026-09
año: 2026
clase: 5
tags:
  - clase
  - modulo-2
  - biologia-de-sistemas
  - modelos-metabolicos
  - ingenieria-metabolica
---

# Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica

> [!info] Ficha de la clase
> **Curso:** Fronteras y Perspectivas en Bioinformática – Universidad ORT (2026) · **Clase 5**
> **Módulo:** [[Módulo 2 - MOC|Módulo 2 - Estado del arte en Biología de Sistemas]]
> **Docente:** [[Ingrid Persitz]]
> **Fecha:** setiembre de 2026
> **Diapositivas:** [[Diapositivas - Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica.pdf]]
> **Resumen de la clase (material del curso):** [[Resumen - Modelos metabólicos.pdf]]
> **Lecturas:** [[Maarleveld et al 2013 - Basic concepts of stoichiometric modeling of metabolic networks|Maarleveld et al. 2013]] · [[Schneider et al 2022 - StrainDesign|Schneider et al. 2022]]
> **Clase previa (en el vault):** [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]] — de la clase 4 (primera del módulo 2) no hay material todavía.

## De qué va la clase

La clase tiene dos mitades:

1. **Teoría:** qué es un [[Modelo metabólico a escala genómica|modelo metabólico a escala genómica]] (GEM), cómo se construye, dónde se consigue, y cómo se lo interroga con [[Modelado basado en restricciones|modelado basado en restricciones]] y [[Flux Balance Analysis|FBA]].
2. **Aplicación:** cómo se usa ese modelo para hacer [[Ingeniería metabólica|ingeniería metabólica]] de forma sistemática, con el [[Diseño computacional de cepas|diseño computacional de cepas]] y la herramienta [[StrainDesign]]. El caso de estudio es obligar a la levadura [[Saccharomyces cerevisiae|*S. cerevisiae*]] a [[Co-consumo de azúcares|consumir tres azúcares a la vez]] (glucosa, xilosa y arabinosa).

La idea que atraviesa todo: pasar de modificar **una pieza por vez** a razonar sobre **la red metabólica completa**, que es exactamente el salto conceptual de la biología de sistemas.

> [!abstract] Cómo leer este resumen
> Sigue la estructura de las diapositivas. Lo que se **dijo en clase** y no está en las diapositivas (tomado del resumen del curso) va en recuadros *"En la clase"*.

> [!quote] En la clase — la docente y el caso
> [[Ingrid Persitz]] es Ingeniera en Biotecnología y Máster en Bioinformática y Biología de Sistemas. El caso de estudio de la segunda mitad es **su proyecto de tesis de maestría**. El problema industrial de fondo: la mezcla de glucosa, xilosa y arabinosa sale de la **hidrólisis de lignocelulosa**, y hay que consumirla entera de forma eficiente.

---

## 1. Ingeniería metabólica clásica y por qué no alcanza

### El enfoque clásico: de a una modificación a la vez

> **Un gen → una enzima → una [[Vía metabólica|vía metabólica]]**

La [[Ingeniería metabólica]] clásica interviene sobre un gen, que codifica una enzima, que cataliza un paso de una vía conocida. La diapositiva lo ilustra con un esquema típico del metabolismo fermentativo central (glucosa → glucosa-6-P → fructosa-1,6-diP → … → PEP → **piruvato**, y desde el piruvato las ramas a lactato, acetoína, formiato, acetil-CoA, etanol y acetato, con el lado de oxalacetato → fumarato → succinato). Sobre un mapa así, el ingeniero elige una flecha y la refuerza o la corta.

### Limitaciones

- **Visión limitada de los efectos:** una intervención local se propaga por toda la red (cofactores compartidos, metabolitos que alimentan varias vías), y eso no se ve mirando una vía aislada.
- **Modificaciones clave pueden no ser consideradas:** si el blanco relevante está lejos de la vía que uno está mirando, nunca se lo va a proponer.

El contraste visual de la diapositiva es la clave: al lado del esquemita de fermentación aparece el **mapa global de vías de [[KEGG]]**, una maraña con miles de reacciones interconectadas. El enfoque clásico mira un rincón de ese mapa.

### Nuevos avances que desbloquean posibilidades

| Frente | Qué aporta |
|---|---|
| **Avance de la [[Biología sintética\|biología sintética]]** | Modificar **varios genes a la vez**; experimentos **high throughput** |
| **Avances computacionales** | Ómicas ([[Integración de datos multiómicos\|integración multiómica]]: genómica, epigenómica, transcriptómica — métodos basados en ácidos nucleicos —, proteómica y metabolómica); **genome scale models**; [[Inteligencia Artificial\|IA]]/[[Machine Learning\|ML]] |

Es decir: ya se puede *construir* mucho más rápido y ya se puede *predecir* a escala de red. Falta juntar las dos cosas.

---

## 2. El ciclo Design–Build–Test–Learn

La clase ubica todo dentro del [[Ciclo DBTL]], el marco estándar de la biología sintética e ingeniería metabólica:

| Fase | Qué incluye (según el esquema de la clase) |
|---|---|
| **Design** | Definir el problema · selección del hospedero (*host selection*) · selección de vías (*pathway selection*) · diseño de experimentos (promotores, RBS, enzimas) · **modelado** |
| **Build** | Ensamblado de partes · modificación del hospedero · ensamblado combinatorio · automatización |
| **Test** | Química analítica · screening · automatización |
| **Learn** | Análisis de vías · reglas de diseño · rediseño de experimentos |

Los modelos metabólicos viven en la fase **Design** (y vuelven a aparecer en **Learn**, cuando los resultados experimentales se usan para refinar el diseño). Lo que sigue en la clase es cómo hacer esa fase de diseño de manera sistemática y no por intuición.

---

## 3. Genome-scale metabolic models (GEMs)

### Qué son

> **Un mapa metabólico formalizado matemáticamente para un organismo en particular.**

Un [[Modelo metabólico a escala genómica]] lista **todas** las reacciones metabólicas que el genoma de un organismo permite, con su estequiometría exacta, y las asocia a los genes que codifican las enzimas correspondientes.

### ¿De dónde sale?

La diapositiva muestra la cadena de reconstrucción:

```
Secuencia de ADN → Genoma anotado → Red metabólica → Modelo estequiométrico
                    (KEGG, KBase,       (reacciones y      (matriz S)
                     ModelSEED)          metabolitos,
                                         con compartimentos)
```

1. Se parte de la **secuencia de ADN** y se obtiene un **genoma anotado** (qué gen codifica qué función).
2. Con bases de datos y plataformas como [[KEGG]], [[ModelSEED y KBase|KBase y ModelSEED]], las funciones enzimáticas se traducen en reacciones → **red metabólica**. La red puede tener **compartimentos** (en el ejemplo de la diapositiva, *Compartment A* y *Compartment B*, con metabolitos que se transportan entre ellos y una reacción final de **biomasa**).
3. La red se formaliza como un **modelo estequiométrico** (1986): un sistema de ecuaciones diferenciales `dc/dt = S·v`, donde `c` son las concentraciones de metabolitos, `S` la [[Matriz estequiométrica|matriz estequiométrica]] y `v` el vector de flujos de reacción.

A partir de ahí la clase muestra tres formas históricas de analizar el modelo:

| Enfoque | Año | Qué hace |
|---|---|---|
| **[[Modelado basado en restricciones\|Constraint-based model]]** | — | Restricciones: `S·v = 0`, `v_j ≥ 0` (irreversibles), `v_j,min ≤ v_j ≤ v_j,max`. Define un cono/poliedro de flujos posibles |
| **[[Análisis de modos elementales\|Elementary Modes Analysis]]** | 1994 | Enumera las rutas mínimas (las "aristas" del cono) que atraviesan la red en estado estacionario |
| **[[Flux Balance Analysis]]** | 1993 | Busca, dentro del poliedro, el punto que maximiza un objetivo: `max z = w·v` |

### ¿Dónde están?

En bases de datos públicas de modelos curados. El ejemplo de la clase es [[BiGG Models]], con el modelo **iML1515**:

| Campo | Valor |
|---|---|
| Organismo | *[[Escherichia coli]]* str. K-12 substr. MG1655 |
| Genoma | NC_000913.3 |
| Metabolitos | **1877** |
| Reacciones | **2712** |
| Genes | **1516** |
| Descarga | [[SBML]] (`.xml`), JSON (`.json`), MAT (`.mat`) — "COBRA model" |

---

## 4. De la red a los flujos: cómo se interroga un GEM

La diapositiva central de la teoría (se repite dos veces, en español e inglés) muestra el recorrido completo en cinco pasos:

### Paso 1 — La célula como red

Un dibujo de célula con metabolitos (nodos) y reacciones (flechas), incluidas reacciones de **intercambio** que cruzan la membrana (entradas y salidas).

### Paso 2 — La red como lista de reacciones

```
R1 :  A + B → C
R2 :  C + D → E + F
R3 :  E + G → 2H
...
Rn :  X + Y → Z
```

### Paso 3 — Las reacciones como matriz

La [[Matriz estequiométrica]] **S** tiene una **fila por metabolito** y una **columna por reacción**. Cada entrada es el coeficiente estequiométrico: negativo si el metabolito se consume, positivo si se produce, cero si no participa.

| | R1 | R2 | R3 | … | Rn |
|---|---|---|---|---|---|
| A | −1 | 0 | 0 | … | 0 |
| B | −1 | 0 | 0 | … | 0 |
| C | +1 | −1 | 0 | … | 0 |
| D | 0 | −1 | 0 | … | 0 |
| E | 0 | +1 | −1 | … | 0 |
| F | 0 | +1 | 0 | … | 0 |
| G | 0 | 0 | −1 | … | 0 |
| H | 0 | 0 | **+2** | … | 0 |
| X | 0 | 0 | 0 | … | −1 |
| Y | 0 | 0 | 0 | … | −1 |
| Z | 0 | 0 | 0 | … | +1 |

Y el vector **v** = (v₁, v₂, …, vₙ) contiene el flujo (velocidad) de cada reacción. Cada flujo es un eje: una distribución de flujos es **un punto** en un espacio de n dimensiones.

### Paso 4 — Restricciones → espacio de flujos factible

Se imponen dos tipos de restricciones:

| Restricción | Significado |
|---|---|
| `S · v = 0` | **Estado estacionario** (*steady state*): cada metabolito interno se produce exactamente al mismo ritmo que se consume; no se acumula |
| `l_i ≤ v_i ≤ u_i` | **Límites en los flujos** (*flux bounds*): irreversibilidad, capacidad máxima, cuánto sustrato está disponible en el medio |

El resultado es un poliedro convexo: el [[Espacio de flujos factible|feasible flux space]]. Todo fenotipo metabólico que la célula *puede* tener, según el modelo, es un punto dentro de ese poliedro.

### Paso 5 — Optimización: FBA

> **max v_bio** sujeto a las restricciones anteriores

[[Flux Balance Analysis]] elige, dentro del espacio factible, el punto que **maximiza el flujo de la [[Reacción de biomasa|reacción de biomasa]]** (el crecimiento). Geométricamente es un vértice del poliedro (la flecha naranja de la diapositiva). Como es un problema de programación lineal, se resuelve en segundos incluso para modelos con miles de reacciones.

El supuesto implícito: la evolución llevó al organismo a crecer lo más rápido posible con lo que tiene disponible.

### Herramientas

| Herramienta | Para qué |
|---|---|
| [[openCOBRA]] | El ecosistema de software para modelado basado en restricciones (COBRA = *COnstraint-Based Reconstruction and Analysis*) |
| [[MetaCyc]] | Base de datos de vías y enzimas (buscador por gen, proteína, metabolito o vía) |
| [[BiGG Models]] | Repositorio de GEMs curados listos para usar |

> [!quote] En la clase — el ecosistema completo
> | Categoría | Herramientas / recursos |
> |---|---|
> | Bases de datos | [[BiGG Models]] (*E. coli* core, *E. coli* iML1515, etc.), [[MetaCyc]], **EcoCyc**, **BioCyc** |
> | Librerías de simulación | **COBRApy** (Python, parte de [[openCOBRA]]), **CBMPy**, **PySCeS** |
> | Visualización de flujos | **Escher** / Escher-FBA |
> | Solvers de optimización | **Gurobi**, **CPLEX** |
>
> FBA es un problema de **optimización lineal**; bajo el supuesto de estado estacionario vale `S · v = 0`.

> [!tip] Para profundizar
> [[Maarleveld et al 2013 - Basic concepts of stoichiometric modeling of metabolic networks|Maarleveld et al. (2013)]] desarrolla toda esta sección con una red de juguete y el modelo de *E. coli* iAF1260: espacio nulo, modos de flujo, FBA, **[[Flux Variability Analysis|FVA]]**, precios sombra, EFMs vs rutas extremas y los supuestos de optimalidad.

---

## 5. ¿Cómo usamos esto para ingeniería metabólica?

### El diseño computacional de cepas remodela el espacio factible

> **Computational strain design searches for genetic interventions that change which phenotypes are possible.**

El [[Diseño computacional de cepas]] busca intervenciones genéticas que **cambien la forma del espacio de flujos factible**, de modo que el fenotipo deseado quede adentro y los indeseados queden afuera. Hay dos tipos de intervención ([[Knock-out y knock-in]]):

| Intervención | Efecto en el modelo | Efecto en la red |
|---|---|---|
| **Gene KI** (knock-in) | **Agrega** nueva(s) reacción(es) | Añade funciones nuevas a la red (p. ej. una vía heteróloga) |
| **Gene KO** (knock-out) | **Elimina** reacción(es) (fija su flujo en 0) | Remueve funciones nativas |

### StrainDesign: una forma sistemática de encontrar esas intervenciones

[[StrainDesign]] es el método de **Schneider et al. (2022)** — ver la lectura [[Schneider et al 2022 - StrainDesign]]. Se basa en tres ideas:

1. **Algoritmo de [[Minimal Cut Sets|Generalized Minimal Cut Sets]]** (gMCS).
2. **Codificar el fenotipo deseado como regiones del espacio de flujos a PROTEGER (*PROTECT*) o SUPRIMIR (*SUPPRESS*).**
3. **Encontrar conjuntos de intervenciones irreducibles** que mantengan factible el fenotipo deseado y vuelvan infactibles los indeseados. *Irreducible* = si se quita cualquier intervención del conjunto, deja de funcionar.

El dibujo de la diapositiva lo muestra en tres pasos:

1. El poliedro original (espacio factible de la cepa salvaje).
2. Se marcan dos regiones: **P** (verde, *growth on glucose*: lo que queremos proteger) y **S** (rojo, *growth on bananas*: lo que queremos suprimir). El ejemplo es deliberadamente absurdo para que se entienda que las regiones las define uno.
3. **Espacio de flujos resultante:** tras aplicar las intervenciones, la región S desapareció, parte de P sigue siendo alcanzable, y aparece una región **R** (amarilla) que es donde efectivamente quedó el espacio factible de la cepa diseñada.

> **Flexible but underused framework.**

La diapositiva cierra con ese diagnóstico, que anticipa el final de la clase.

---

## 6. Caso de estudio: co-consumo forzado de tres azúcares en levadura

### El problema biológico

Los azúcares derivados de biomasa vegetal (*biomass-derived mixed sugars*, como dice uno de los títulos citados) vienen como una **mezcla**: glucosa y [[Pentosas|pentosas]] (xilosa, arabinosa).

- [[Saccharomyces cerevisiae|*S. cerevisiae*]] consume **glucosa preferentemente**, y las pentosas **lento, ineficientemente o directamente no**.

### Estrategias actuales

La literatura mostrada en la clase:

| Trabajo | Estrategia |
|---|---|
| Garcia Sanchez et al. (2010) — *Improved xylose and arabinose utilization by an industrial recombinant S. cerevisiae strain using evolutionary engineering* | [[Evolución adaptativa de laboratorio]] |
| Gao, Ploessl & Shao — *Enhancing the co-utilization of biomass-derived mixed sugars by yeasts* | Revisión de estrategias de co-utilización |
| Nijland & Driessen — *Engineering of pentose transport in S. cerevisiae for biotechnological applications* | Ingeniería de transportadores |
| Papapetridis et al. (2018) — *Laboratory evolution for forced glucose-xylose co-consumption enables identification of mutations that improve mixed-sugar fermentation…* | Evolución de laboratorio con co-consumo forzado |
| Wisselink et al. — *Engineering of S. cerevisiae for efficient anaerobic alcoholic fermentation of L-arabinose* | [[Vías de asimilación de pentosas\|Vías heterólogas]] |

Resumidas en tres estrategias de ingeniería:

- Introducir **vías heterólogas** para asimilar pentosas.
- **Ingeniería de transportadores**.
- **[[Evolución adaptativa de laboratorio]]** (ALE).

La docente subraya en rojo las palabras de los títulos: *Improved*, *Enhancing*, *improve*, *Efficient*. Todas apuntan a **mejorar** o **habilitar** el consumo de pentosas. De ahí la frase clave:

> **Enabling co-consumption is not enforcing co-consumption.**

Que la levadura *pueda* consumir xilosa no significa que lo *haga*: si tiene glucosa, va a seguir prefiriéndola.

> **Instead of only enabling co-consumption, can we make co-consumption required for growth?**

### La formulación del problema

> **Encontrar conjuntos de KO/KI que hagan que el crecimiento sea posible *solo* cuando se consumen los tres azúcares.** No debe quedar ninguna distribución de flujos factible donde el crecimiento se sostenga con un solo azúcar o con cualquier par de azúcares.

Es decir, convertir el [[Co-consumo de azúcares|co-consumo]] en una condición **necesaria** para crecer (acoplamiento al crecimiento).

### El diseño del experimento computacional

| Bloque | Configuración |
|---|---|
| **Condiciones** | Modelo: [[Yeast9]] · condición **aeróbica o anaeróbica** · se permite captación de glucosa, xilosa y arabinosa |
| **Candidatos KI y KO** | **KI:** 13 reacciones heterólogas para metabolismo de xilosa y arabinosa · **KO:** todos los genes nativos del modelo Yeast9 |
| **Módulos SUPPRESS (×9)** | Suprimir toda distribución de flujos con: crecimiento + captación de **un** azúcar · crecimiento + captación de **dos** azúcares · crecimiento + captación **marginal** de algún azúcar |
| **Módulo PROTECT (×1)** | Proteger al menos una distribución de flujos con crecimiento + captación de **los tres** azúcares |
| **Simulaciones** | 30 corridas independientes de StrainDesign · límite de 30 min cada una · 32 núcleos de CPU, 128 GB de memoria · costo máximo de intervención: 55 |

Los nueve módulos SUPPRESS salen de las combinaciones: tres casos de "un solo azúcar", tres de "un par de azúcares" y tres de "captación marginal" de cada azúcar (que un azúcar esté presente solo testimonialmente también cuenta como hacer trampa).

### Verificación, ranking y análisis de diseños

- **Balance score** = la **menor contribución** de un azúcar, considerando todos los azúcares y todos los órdenes de minimización de captación. Un diseño con balance score alto obliga a que *los tres* azúcares aporten una fracción relevante; uno con balance score cercano a 0 técnicamente cumple pero con algún azúcar casi irrelevante.
- **Descomposición en eCAT, pCAT y ANA** siguiendo **Remeijer et al.**: separar el metabolismo del diseño en [[Catabolismo y anabolismo|catabolismo energético, catabolismo de precursores y anabolismo]] para ver qué papel juega cada azúcar.

---

## 7. Resultados

### Resultados generales

| Resultado | Valor |
|---|---|
| Diseños aeróbicos encontrados | **729** |
| Diseños anaeróbicos encontrados | **158** |
| Mínimo de intervenciones que alcanza para forzar co-consumo | **13** |
| Diseños aeróbicos con balance score > 5 % | **332** (los otros 397 quedan por debajo) |
| Diseños anaeróbicos con balance score > 5 % | **0** → *desafío de relevancia industrial* |

Los gráficos muestran cada diseño como una barra (altura = número total de intervenciones, KI + KO), ordenados por balance score:

- **Aeróbico:** el balance score llega hasta ~17,5 %; los diseños necesitan entre ~13 y ~60 intervenciones. Está marcado el **diseño seleccionado**, entre los de mejor balance y con pocas intervenciones (~14).
- **Anaeróbico:** el balance score máximo ronda **3,5 %**, y ningún diseño cruza el umbral de 5 %. La clase lo marca como un **desafío de relevancia industrial**.

Dos conclusiones:

> **StrainDesign encuentra conjuntos de intervenciones que fuerzan el co-consumo.**

> **Es computacionalmente imposible enumerar todas las soluciones. Las simulaciones corridas dan una *muestra* del espacio de soluciones.**

### Un diseño aeróbico seleccionado

**Los KI introducen rutas de asimilación de pentosas** (ver [[Vías de asimilación de pentosas]]):

- **Arabinosa → vía de la isomerasa bacteriana:** ARAI (arabinosa isomerasa) → L-ribulosa → RBK_L1 (ribuloquinasa) → L-ribulosa-5-P → RBP4E (epimerasa) → **D-xilulosa-5-P**, que entra a la [[Vía de las pentosas fosfato]].
- **Xilosa → vía de Weimberg:** XYLOR → D-xilonolactona → XYLLN → D-xilonato → DXYLTD → 2-ceto-3-desoxi-D-xilonato → 2D3DDAD → α-cetoglutarato semialdehído → 2OGSAD → **α-cetoglutarato**. Es una ruta oxidativa que lleva la xilosa directo al ciclo de Krebs, **sin pasar** por la vía de las pentosas fosfato.

**Los KO bloquean rutas alternativas:**

| KO | Qué bloquea |
|---|---|
| **PGL, PGI** | La entrada de glucosa a la [[Glucólisis\|glucólisis]] (y a la rama oxidativa de las pentosas fosfato) |
| **PGK, TPI** | La producción de piruvato derivada de arabinosa y la producción de ATP por el **bypass de metilglioxal** |
| **XYLTD_D** | La entrada de xilosa a la vía de las pentosas fosfato (vía xilitol → D-xilulosa-5-P), dejando solo la ruta de Weimberg |
| **FDH** | Rutas alternativas (vía formiato) que permitirían crecer sin xilosa |

En total son 8 KI + 6 KO = 14 intervenciones, lo que coincide con la altura de la barra del diseño seleccionado.

**El resultado: cada azúcar queda con un rol exclusivo.**

| Azúcar | A qué queda destinado |
|---|---|
| **Glucosa** | Solo a **glucanos** (pared celular: β-1,3 y β-1,6-glucano, glucógeno, trehalosa) — ya no puede entrar a glucólisis |
| **Arabinosa** | D-xilulosa-5-P → pentosas fosfato → **adenosina** (nucleótidos) y **aminoácidos aromáticos** (vía corismato: tirosina, fenilalanina, triptófano) |
| **Xilosa** | α-cetoglutarato → **precursores derivados de AKG** (glutamato, etc.) y, por respiración, la mayor parte de **NADH, ATP y NADPH** |

> **Los precursores y los [[Cofactores energéticos|transportadores de energía cargados]] que produce un azúcar no pueden ser reemplazados por completo por los otros. Los tres azúcares se vuelven complementarios.**

Esa es la lógica del diseño: si falta cualquiera de los tres, falta algo esencial para la [[Reacción de biomasa|biomasa]], y la célula no crece.

### El mapa completo del diseño (figura A)

La figura de detalle muestra los flujos predichos para cada reacción. La captación queda en **15,39 de xilosa, 2,52 de arabinosa y 1,64 de glucosa**: la xilosa es, lejos, la principal fuente de carbono. La **ecuación global** del diseño:

```
30,81 O₂ + 15,39 xilosa + 2,52 arabinosa + 1,64 glucosa
+ 6,37 NH₄ + 0,28 fosfato + 0,086 sulfato + iones
        →
50,57 H₂O + 38,32 CO₂ + 4,46 acetato + 1 biomasa + 2,87 etanol
+ 0,57 formiato + 0,073 tirosol
```

### La descomposición eCAT / pCAT / ANA (figura B)

La descomposición según Remeijer et al. muestra el mismo diseño en tres bloques de [[Catabolismo y anabolismo]]:

- **Catabolismo energético (eCAT):** alimentado por xilosa y O₂; genera ATP y libera CO₂, etanol y acetato.
- **Catabolismo de precursores (pCAT):** alimentado sobre todo por xilosa (y algo de arabinosa); produce NADPH, NADH y bloques de construcción (L-cisteína, isoleucina, acetil-CoA, L-glutamato, L-homocisteína, piruvato, fumarato); libera formiato, tirosol, CO₂ y acetato.
- **Anabolismo (ANA):** recibe ATP, cofactores reducidos y precursores, más **arabinosa y glucosa directamente**; devuelve ADP, CoA, NAD, NADP, α-cetoglutarato, succinato y L-malato al catabolismo.

> [!quote] En la clase
> En los diseños destacados, **cada azúcar se canaliza hacia vías esenciales e interdependientes** (formación de glucanos, síntesis de aminoácidos aromáticos, generación de energía): ninguna puede cubrirse con otro azúcar, y por eso la célula se ve obligada a consumir los tres.

### El paisaje de soluciones

Mirando **qué KO aparecen con más frecuencia** en todos los diseños muestreados:

- **Algunos KI candidatos nunca fueron elegidos** en los diseños muestreados.
- **PGI es el KO más frecuente** tanto en aeróbico (~93 % de los diseños) como en anaeróbico (~87 %).
- **RPE** (ribulosa-5-fosfato epimerasa, [[Vía de las pentosas fosfato|pentosas fosfato]]) también aparece con frecuencia.
- En aerobiosis, detrás de PGI siguen FBA/FBA2/FBA3 (aldolasa, glucólisis), XYLR y ARABR (interconversión de pentosas y glucuronato), XYLTD_D, GND, PGL, G6PDH2r…
- En anaerobiosis aparece un conjunto muy distinto: reacciones del metabolismo de **purinas y pirimidinas** (NDP1, NDP3, NDP7, NTP5, NTP7, NTP10, IDPA, CDPPH), triptófano, arginina y prolina, ésteres de ácidos grasos.

La conexión con la literatura: **Papapetridis et al. (2018)** diseñaron una cepa dependiente de co-consumo glucosa-xilosa **"basándose en la observación"** de que inactivar **PGI1** bloquea la entrada de glucosa-6-P a la glucólisis, e inactivar **RPE1** impide la entrada de ribulosa-5-P a la rama no oxidativa de las pentosas fosfato; una cepa *pgi1Δ rpe1Δ* no puede crecer en glucosa sola. StrainDesign **redescubre** esa lógica por sí mismo.

> **La lógica de KO conocida aparece en el conjunto de soluciones, pero el método además revela blancos no obvios.**

> **Mediante análisis "humano" de los mapas de vías, estos serían muy probablemente imposibles de encontrar.**

No todos los KO tienen un efecto obvio al inspeccionar las vías, y justamente ahí está el valor del enfoque a escala de red frente a la ingeniería metabólica clásica de la sección 1.

---

## 8. Otras aplicaciones de StrainDesign

> **¡Cualquiera que se nos ocurra!**

Los pasos son siempre los mismos:

1. Armar la **lista de reacciones** candidatas.
2. **Agregarlas al modelo.**
3. **Definir los fenotipos deseados** (qué proteger, qué suprimir).
4. **Correr el modelo.**

Ejemplo mencionado: **fijación de CO₂ en *[[Escherichia coli|E. coli]]***.

El gráfico que acompaña es una proyección del espacio de flujos del modelo *core* de *E. coli*: crecimiento (`BIOMASS_Ecoli_core_w_GAM`, eje x) contra exportación de un producto (`EX_14bdo_e`, 1,4-butanodiol, eje y), con el espacio dividido en regiones de colores, que es la forma típica de visualizar qué zonas protege o suprime un diseño.

---

## 9. La brecha: estos métodos no llegan al laboratorio

> **These type of methods do not reach the experimental metabolic engineers. There is a gap to bridge.**

Es el "flexible but underused" de la sección 5 hecho problema: los ingenieros metabólicos experimentales no usan estas herramientas porque requieren saber programar, manejar modelos y solvers.

La respuesta que muestra la clase es una interfaz: [[PECA|PECA — Pathway Engineering & Co-consumption Assistant]] (con un pulpo científico como mascota y un guiño a la IA). Es un asistente paso a paso:

1. **Host** — elegir el modelo hospedero: modelos precargados (`PECA_toy.xml`, `iMM904.xml`, `yeast9_anaerobic_biggids.xml`) o subir uno propio en [[SBML]] (`.xml`) o COBRA JSON (`.json`). *"El modelo define todas las reacciones y genes disponibles."*
2. **Sugars** — qué azúcares.
3. **Candidates** — candidatos KI (reacciones) y KO (por defecto, todas las reglas gen-reacción).
4. **Settings** — solver (backend **glpk**), costo máximo y número de soluciones.
5. **Run.**

---

## 10. Cierre: limitaciones y oportunidades

La última diapositiva de contenido son dos cajas vacías, **Limitaciones** y **Oportunidades**, planteadas para discutir en clase. A partir de lo que la propia clase fue mostrando, quedan sobre la mesa:

| Limitaciones | Oportunidades |
|---|---|
| El espacio de soluciones **no se puede enumerar**: solo se obtiene una muestra | Encontrar **blancos no obvios** que el análisis manual no vería |
| En **anaerobiosis** (la condición industrial) ningún diseño logra buen balance | Formular **cualquier** fenotipo como regiones a proteger/suprimir (p. ej. fijación de CO₂) |
| Las predicciones son del **modelo**: la calidad depende del GEM y hay que validarlas experimentalmente (fase *Test* del [[Ciclo DBTL]]) | Integrar el diseño computacional al ciclo DBTL, junto a la biología sintética high throughput |
| Herramientas **poco usadas** por quienes trabajan en el laboratorio | Interfaces como [[PECA]] para **cerrar la brecha** entre modeladores y experimentales |

---

> [!quote] En la clase — limitaciones que señaló la docente
> - **Dinámica y regulación:** los modelos estequiométricos de FBA estándar **no incluyen parámetros cinéticos** (K_m, V_max) **ni regulación** de la expresión génica.
> - **Sesgo en los knock-ins:** los candidatos heterólogos se **preseleccionan a mano** a partir de la literatura.
> - **Complejidad computacional:** la búsqueda combinatoria de intervenciones exige mucha capacidad de cómputo y límites de tiempo por simulación.

## Ideas para retener

- Un [[Modelo metabólico a escala genómica|GEM]] es la red metabólica completa de un organismo escrita como una [[Matriz estequiométrica|matriz S]]. Con `S·v = 0` y límites en los flujos define un [[Espacio de flujos factible|espacio de flujos factible]]: todos los fenotipos que el organismo *puede* tener.
- [[Flux Balance Analysis|FBA]] elige un punto de ese espacio (el de máximo crecimiento). El [[Diseño computacional de cepas|diseño computacional de cepas]] hace algo más ambicioso: **cambia la forma del espacio** con KO y KI.
- [[StrainDesign]] traduce "lo que quiero" en regiones **PROTECT** y "lo que no quiero" en regiones **SUPPRESS**, y busca conjuntos mínimos de intervenciones con [[Minimal Cut Sets|minimal cut sets]].
- **Habilitar no es forzar.** Una levadura que *puede* comer xilosa sigue prefiriendo glucosa. El diseño fuerza el co-consumo haciendo que cada azúcar aporte algo que los otros no pueden reemplazar.
- El método **redescubre** diseños conocidos (PGI, RPE) y **propone blancos no obvios**. Ese es el argumento a favor del enfoque de sistemas frente a la ingeniería metabólica de "una pieza por vez".
- El cuello de botella ya no es solo computacional: es que estas herramientas **lleguen** a quienes hacen los experimentos.

## Lecturas de la clase

| Lectura | Qué aporta |
|---|---|
| [[Maarleveld et al 2013 - Basic concepts of stoichiometric modeling of metabolic networks]] | La base matemática del modelado estequiométrico: de la matriz S al FBA, FVA y modos elementales |
| [[Schneider et al 2022 - StrainDesign]] | El paper de la herramienta: qué algoritmos integra (OptKnock, RobustKnock, OptCouple, MCS), tipos de intervención y preprocesamiento |

## Conexiones

- Viene de → [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]] (último del Módulo 1; la clase 4 aún no está en el vault)
- Del Módulo 1 → el cierre de [[Biología espacial - mapeando la expresión génica a su entorno]] planteaba el paso de *datos a conocimiento* vía integración; los GEMs son justamente una forma de integrar el genoma anotado en un modelo predictivo
- Índice → [[Módulo 2 - MOC]]
