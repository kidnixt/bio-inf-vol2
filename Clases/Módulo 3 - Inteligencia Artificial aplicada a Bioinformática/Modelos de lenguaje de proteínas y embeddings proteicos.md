---
titulo: "Modelos de Lenguaje de Proteínas y Embeddings Proteicos"
curso: Fronteras y Perspectivas en Bioinformática – Universidad ORT
modulo: Módulo 3 - Inteligencia Artificial aplicada a Bioinformática
docente: Ignacio Ferrés
fecha: 2026-09
año: 2026
clase: 9
tags:
  - clase
  - modulo-3
  - PLM
  - embeddings
  - proteínas
  - IA
---

# Modelos de lenguaje de proteínas y embeddings proteicos

> [!info] Ficha de la clase
> **Curso:** Fronteras y Perspectivas en Bioinformática – Universidad ORT (2026) · **Clase 9**
> **Módulo:** [[Módulo 3 - MOC|Módulo 3 - Inteligencia Artificial aplicada a Bioinformática]]
> **Docente:** [[Ignacio Ferrés]] — Universidad ORT Uruguay
> **Subtítulo:** *Del alfabeto de 20 letras al diseño de novo*
> **Fecha:** setiembre de 2026
> **Diapositivas:** [[Diapositivas - Modelos de lenguaje de proteínas y embeddings proteicos.pdf]]
> **Resumen de la clase (material del curso):** — no hay
> **Lecturas:** — no hay lecturas asignadas; la clase cierra con una lista *"Para seguir explorando"* (ver al final)
> **Clase previa (en el vault):** [[Métodos para el diseño computacional de fármacos]] (clase 6, mismo módulo)

## De qué va la clase

La clase está explícitamente organizada como una **línea de tiempo**, y el patrón que la recorre es uno solo:

> **Cada salto agrega contexto.** Primero una letra, después su entorno, después la secuencia entera, después la forma — y finalmente la función.

| Módulo | Qué se lleva |
|---|---|
| 1. Leer una proteína como si fuera un texto | Un vocabulario compartido |
| 2. Embeddings estáticos | Qué es un vector y de dónde sale: word2vec y ProtVec |
| 3. Los vectores y el contexto | El vector deja de ser fijo: ELMo y SeqVec |
| 4. Llega la atención | Qué es un transformer y por qué ganó |
| 5. La estructura emerge | El modelo predice estructura a partir de la secuencia primaria |
| 6. La forma se vuelve texto | Comparar y anotar estructura con modelos de lenguaje |
| 7. Secuencia, estructura y función | El salto generativo: ESM3 |
| 8. Casos de aplicación | Cuatro casos reales, uno de ellos local |
| Cierre | Los límites: la mesada sigue mandando |

La línea de tiempo que se va completando diapositiva a diapositiva:

| pre-2013 | 2013 | 2017 | 2019 | 2021 | 2024 | 2025 |
|---|---|---|---|---|---|---|
| Era clásica | Vectores | Recurrentes | Transformer | Estructura | Multimodal | Generativo |
| Reglas, frecuencias y alineamientos | [[Word2vec]], [[ProtVec]] | [[ELMo y SeqVec\|ELMo]], [[ELMo y SeqVec\|SeqVec]] | [[Transformer]], [[ProtT5 y ProtBERT]] | [[ESM-1b y ESM-2\|ESM-1b / ESM-2]], [[ESMFold]] | [[ProstT5]], [[Foldseek]] | [[ESM3]] |

> [!abstract] Cómo leer este resumen
> Sigue la estructura de las diapositivas. Esta clase no tiene PDF de resumen del curso, así que no hay recuadros *"En la clase"*.

---

## 1. Leer una proteína como si fuera un texto

### Una proteína es texto

| Ingeniería (lenguaje natural) | Biotecnología (proteínas) |
|---|---|
| Alfabeto de ~27 letras → palabras → oraciones | 20 aminoácidos → motivos → proteínas |

La misma cadena de símbolos se puede leer en cuatro niveles, y la analogía con el lenguaje es exacta:

| Nivel biológico | Equivalente en lenguaje | Qué captura |
|---|---|---|
| **Estructura primaria** | Texto plano | El orden de los símbolos |
| **Estructura secundaria** | Morfología | Patrones locales |
| **Estructura terciaria** | Sintaxis y gramática | Elementos **distantes** que se relacionan |
| **Función biológica** | Semántica | El significado global |

La fila de la estructura terciaria es la que justifica todo lo que viene después: **posiciones lejanas en la cadena que están cerca en el espacio** es exactamente el problema de las dependencias a larga distancia en lenguaje natural.

### Cuando el texto cambia

Si una proteína es texto, se puede hablar de **ediciones** al texto. Hay tres, y **no son equivalentes**:

| Edición | Ejemplo | Qué significa |
|---|---|---|
| **1 · Mutación puntual** | `MKVLAG` → `MKVFAG` | Cambia **una letra**; el resto queda igual: el "error tipográfico". Puede ser **silencioso o destruir la función** |
| **2 · [[Permutación circular]]** | `MKVAG` → `AGMKV` | Se corta y se **reordena**: las mismas letras, otro orden. Solo es inocua si los extremos N y C ya estaban **juntos en el espacio** |
| **3 · [[Homología]]** | humano `MKVLAG` / ratón `MKILSG` | No es un error: es **divergencia** desde un ancestro común. El texto cambió y **la función se conservó** |

> **Por qué importa para un modelo de lenguaje:** los tres casos producen secuencias parecidas pero significan cosas distintas. Un modelo que solo **cuente letras** no los distingue. Uno que aprenda **contexto** —el resto de la frase y su estructura— sí. Esa es la diferencia entre [[ProtVec]] y todo lo que viene después.

---

## 2. Embeddings estáticos

### ¿Qué es un embedding?

La traducción literal sería *"incrustación"*: el concepto se **incrusta** en un espacio de muchas dimensiones. Pero se usa **"representación vectorial"**, que describe mejor lo que hace: representar algo con una lista de números.

El ejemplo de la clase (tomado de material de Google) es una app de recetas con 5.000 comidas:

**Paso 1 · cada ítem recibe una posición.** Un modelo solo manipula números, así que cada comida necesita su lugar.

**Paso 2 · [[One-hot encoding|one-hot]]: un 1 y el resto 0s.** Cada comida es un vector de 5.000 posiciones: un 1 en la propia y 0 en las otras 4.999.

> **El problema:** todos los 1s están **a la misma distancia**, así que *borscht* y *shawarma* quedan igual de lejanos que *borscht* y *pizza*. Y son vectores de 5.000 números casi todos 0s: enormes y vacíos.

El [[Embedding]] es lo que viene después: **comprime eso y aprende qué se parece a qué**.

### Cómo se entrena: de 1s y 0s a relaciones

1. **Tapar una palabra** — *"Como te gustan los panqueques, te recomendamos los __"*.
2. **Adivinar** — antes de entrenar, al azar (*borscht* ✗); tras millones de intentos, *crepes* ✓.
3. **Ajustar los pesos** — el error es la señal: las conexiones que llevaron al error se debilitan, las que acercaban a la respuesta se refuerzan.

> **El salto:** one-hot solo sabe **contar** —cuántos 1s y dónde—. El embedding sale de millones de intentos como este: cada ítem termina con una **posición**, y quedar cerca o lejos **significa algo**.

### Las dimensiones son rasgos que nadie diseña

Con **un eje** imaginario (la *"sandwicheidad"*), la sopa y la pizza quedan lejos; el hot dog y el shawarma, cerca. Con **dos ejes** (*sandwicheidad* y *postreidad*) el mapa se vuelve un plano:

- **Cada eje captura un rasgo**, no una categoría cerrada.
- **La posición es el significado**: la distancia ya es información.
- **Nadie diseña los ejes.** En un embedding real hay cientos o miles de dimensiones así, y **las descubre el modelo**.

> Una dimensión ordena en una línea; dos arman un mapa; **N** dimensiones permiten comparar parecidos que ningún eje solo podría describir.

### Las relaciones son direcciones

En un espacio de embeddings, **una relación es una dirección**. Y en los embeddings estáticos son **fijas**: la misma palabra ocupa siempre el mismo lugar, aparezca donde aparezca.

| Relación | Ejemplo | Lo que se generaliza |
|---|---|---|
| **Género** | `rey → reina` | La misma distancia que `hombre → mujer` |
| **Tiempo verbal** | `caminando → caminó` | El mismo salto que `nadando → nadó` |
| **País → capital** | `Chile → Santiago` | Doce países, la misma dirección |

> **La idea:** el modelo **nunca vio la palabra "capital"**. Aprendió la dirección que separa un país de su capital, y esa dirección sirve para todos.

### Word2vec: el origen de todo

[[Word2vec]] (Mikolov et al., 2013, Google). Antes de las proteínas, la idea se inventó para el lenguaje natural.

> **Era un truco, no un objetivo.** Nadie quería predecir palabras: eso es un **problema ficticio**. Se inventó solo como excusa para obligar a la red a aprender algo útil en el camino. **La predicción se descarta; los vectores se quedan.**

1. **La tarea inventada** — tapa una palabra y trata de adivinarla por las que la rodean.
2. **Lo que aprende** — para acertar, la red **tiene** que descubrir qué palabras van juntas.
3. **El premio real** — se tira la salida y se guardan los **pesos internos**: eso es el embedding.

Dos formas de plantear el juego, con talentos distintos:

| Modelo | Cómo | Significado | Forma |
|---|---|---|---|
| **CBOW** | Tapa el medio, adivina por el contexto | 24 % | **64 %** |
| **Skip-gram** | Al revés: con una palabra, adivina qué la rodea | **55 %** | 59 % |

*(acierto en el test de relaciones, Mikolov et al. 2013, Tabla 3)*

**Skip-gram más que duplica a CBOW en significado**, pero pierde en forma. Por eso **la familia de proteínas se apoya en Skip-gram**: en una proteína importa el significado, no la forma superficial.

Por qué fue noticia: **6.000 millones de palabras** del corpus Google News, vocabulario de **1 millón**, entrenadas en **menos de un día** — la red **no tiene capa oculta**, y esa simpleza es lo que permitió la escala.

Y la compresión: de un vector disperso de **50.000 posiciones casi todas en cero** a uno denso de **100–300 números todos con valor**. Misma palabra, **167 veces menos números**, y ahora con información.

> Y el vector **sale de la nada**: no hay una capa oculta que "calcule" — la **matriz de pesos es la tabla**. Buscar una palabra es buscar su fila. Por eso es tan barato.

### ProtVec: el punto de partida

[[ProtVec]] (Asgari & Mofrad, 2015) es la primera traducción de word2vec a proteínas:

- Parte la secuencia en **[[K-mer|3-meros]]**: `MKV`, `KVL`, `VLA`… (en tres marcos superpuestos).
- Cada 3-mero es una **"palabra"**.
- Aprende **un vector por palabra**.

La secuencia se vuelve una **bolsa de palabras**: la misma jugada que en lenguaje natural, contar vecinos frecuentes.

> [!warning] Su límite
> El vector de `MKV` es **siempre el mismo**, aparezca donde aparezca. **No hay contexto.** Y una ventana de 3 residuos es demasiado corta para ver estructura.

---

## 3. Los vectores y el contexto

*De un vector fijo por palabra a un vector que **depende de sus vecinos**.*

### ELMo: la arquitectura que hace posible el contexto

[[ELMo y SeqVec|ELMo]] (Peters et al., 2018, Allen AI). SeqVec no la inventa: **la aplica** a proteínas.

**Dos LSTM, entrenadas juntas:** una pasada hacia adelante y otra hacia atrás. Se entrenan de forma conjunta (comparten la capa de entrada y la de salida), pero **cada dirección tiene sus propios parámetros** de LSTM.

**El vector se concatena:** en cada posición se pegan las dos direcciones, `[→h ; ←h]`. **No es una sola pasada que ve todo**: son dos recorridos unidos al final.

**Lo que lo hizo distinto:** no usa solo la última capa. **Combina todas** con pesos que aprende cada tarea — las capas bajas capturan sintaxis, las altas semántica.

Los números: 2 capas de biLSTM por dirección, 4096 unidades con proyección a 512, 5 representaciones por token (entrada + 2 adelante + 2 atrás), y **entrada por caracteres**, no por palabras.

> **Entrada por caracteres:** como lee letra por letra, ELMo puede representar palabras que **nunca vio** en el entrenamiento. En proteínas esto es todavía más natural: el "vocabulario" son 20 letras.

### SeqVec: aparece el contexto

[[ELMo y SeqVec|SeqVec]] (Heinzinger et al., 2019) — el mismo autor que después haría [[ProstT5]].

- **Ya no hay 3-meros:** se lee la secuencia completa.
- **El vector depende del entorno:** cada residuo mira a sus vecinos.
- **Bidireccional:** dos pasadas, una por sentido (ELMo) — *no* masked.

El hallazgo de la figura (proyección [[t-SNE]], coloreada por localización celular y por membrana): **los embeddings sin entrenar ya agrupan proteínas por función** — una señal que el modelo **nunca recibió**. Entrenarlo solo mejora la separación.

Y el contexto se traduce en rendimiento, misma tarea y misma secuencia de entrada, cambiando solo la representación:

| Tarea | Resultado |
|---|---|
| **Estructura secundaria** (Q3) | SeqVec queda cerca de los mejores métodos, **sin usar alineamientos** |
| **Predicción de membrana** | Salta de **77,6** ([[ProtVec]]) a **92,3** (DeepLoc con SeqVec) |

---

## 4. Llega la atención

*De leer en orden a mirar **todo a la vez**. El salto que habilita la escala.*

### El Transformer

[[Transformer]] (Vaswani et al., 2017, Google). La arquitectura detrás de todos los modelos que siguen —en texto y en proteínas— y también de los LLMs actuales.

**El problema que resolvió:** los modelos previos (RNN, LSTM) leían **en orden**, símbolo por símbolo. Eso los hacía **lentos** (no se podían paralelizar) y **olvidaban lo lejano**: la posición 5 y la 500 apenas se conectaban.

**La idea: [[Self-attention]].** Cada posición **mira a todas las demás a la vez** y decide cuánto le importa cada una. Sin leer en orden, sin recurrencia. La distancia entre dos posiciones cualesquiera es **un solo paso** (en una RNN eran hasta *n* pasos).

| Pieza | Qué hace |
|---|---|
| **Q · K · V** | Cada símbolo se proyecta en *consulta*, *clave* y *valor*. El parecido entre consulta y clave decide cuánto se mezcla cada valor |
| **Multi-head** (8 cabezas) | Ocho atenciones en paralelo, cada una mirando un tipo de relación distinto. Se concatenan al final |
| **Posición explícita** | Como no hay orden implícito, la posición se **suma** al vector: senos y cosenos de distinta frecuencia |

> **Por qué nos importa:** el Transformer **no sabe de biología**, solo de secuencias y relaciones a distancia. Es exactamente el problema de la estructura terciaria: posiciones lejanas en la cadena que están cerca en el espacio.

*(Configuración original: 6 capas, 512 dimensiones, 8 cabezas.)*

### Las tres formas de leer una secuencia

La misma secuencia `MLVAGRR`, tres maneras de procesarla. Cambia **qué puede ver cada residuo** — y por lo tanto para qué sirve el modelo:

| | Cómo lee | Para qué sirve | Modelos |
|---|---|---|---|
| **A · Autorregresiva** | Una sola dirección: p(xₜ \| x₁…xₜ₋₁). Solo mira lo anterior | **Generar** — inventar secuencias nuevas | ProtGPT2, ProGen |
| **B · Bidireccional** | Dos pasadas *independientes* que después se concatenan | **Etiquetar cada residuo** — estructura secundaria, accesibilidad al solvente, sitios activos | [[ELMo y SeqVec\|ELMo, SeqVec]] |
| **C · [[Masked language modeling\|Masked]]** | Toda la secuencia a la vez; se tapa un residuo y se predice. Cada posición ve **todo el resto en una sola pasada** | **Representar** — embeddings de alta calidad para clasificar | BERT, [[ESM-1b y ESM-2\|ESM]], [[ProtT5 y ProtBERT\|ProtBERT]] |

> ¿Querés **entender** una proteína que ya existe? → **C** (o **B** si te importa cada residuo). ¿Querés **inventar** una nueva? → **A**.

### Por qué la atención cambió todo

| RNN / LSTM | Transformer |
|---|---|
| Leen de a un elemento | Mira toda la secuencia |
| Lo lejano se desvanece | Lo lejano en 1D puede estar **cerca en 3D** |
| No se paraleliza | Se paraleliza → **escala** |

### El mismo símbolo, dos significados

*"Chile es un país"* / *"el chile es picante"*. *"Un señor sentado en un banco"* — pero no en el mismo sentido que un banco de plaza.

Un **embedding fijo no puede distinguir** estos significados. Uno **contextual**, sí. Y lo mismo pasa con un aminoácido: **su comportamiento depende de quién lo rodea** en la cadena.

Sobre una secuencia lineal de 24 residuos, cada paso del entrenamiento **tapa un sector distinto**: así aprende el modelo. Las últimas capas ocultas **reescriben el vector de cada aminoácido según toda la secuencia**. Entra un símbolo; sale un **vector situado** — y la forma deja de ser un dibujo aparte.

### Cómo se extrae el vector de una proteína

```
ENTRA                    EL MODELO              SALE
MKVLAGD        →         PLM (ESM-2)     →      un vector por residuo
secuencia lineal                                 (matriz residuos × dimensiones)
de aminoácidos
                                          → media por fila →  1 vector para toda la proteína
```

**Dos formas de usar la salida:**

- **Por residuo** — predecir posición por posición (estructura secundaria, sitios activos).
- **Promedio** (*mean pooling*) — clasificar la proteína entera (por ejemplo, su localización subcelular).

> [!note] El vocabulario no es el alfabeto
> La biología tiene **20** aminoácidos, pero ESM-2 usa **33 tokens**: los 13 extra son símbolos de control — inicio, fin, relleno, la **máscara**, `X` para desconocidos, y aminoácidos ambiguos. *(Verificado en `facebook/esm2_t33_650M_UR50D`: 1280 dimensiones, 33 capas.)*

### ProtT5 y ProtBERT

El proyecto **ProtTrans** ([[ProtT5 y ProtBERT]], Elnaggar et al., 2021) entrena transformers a gran escala sobre secuencias.

| Modelo | Arquitectura | Objetivo |
|---|---|---|
| **ProtBERT** | Solo *encoder* | *Masked* |
| **ProtT5** | *Encoder-decoder* | *Denoising* |

**Lo que demostró:** un PLM **sin MSA** ni información evolutiva explícita **iguala o supera** a los métodos clásicos, y sus embeddings alimentan **clasificadores simples**.

> **Sin alineamientos.** La información evolutiva que los métodos clásicos sacaban de un [[Alineamiento múltiple de secuencias|MSA]], el modelo **la aprende de haber visto millones de secuencias**.

---

## 5. La estructura emerge del entrenamiento

*Nadie le enseñó 3D, y sin embargo la atención **la encuentra**.*

### ESM-1b: la estructura está adentro

[[ESM-1b y ESM-2|ESM-1b]] (Rives et al., 2021). El hallazgo que cambió la percepción de estos modelos: **nadie le enseñó estructura, y sin embargo quedó codificada**.

La atención de un residuo **apunta a residuos lejanos en la secuencia pero cercanos en el espacio**. Eso es lo que permite que se conecten. Del [[Mapa de contactos]] recuperado de ESM-1b se ve que compite con el método clásico CCMpred.

> [!note] Hace falta una sonda
> La información **está** en las representaciones, pero para leerla hace falta una **sonda entrenada** —una proyección lineal o un clasificador chico—. Nadie le pasó un solo contacto durante el entrenamiento: **los aprendió de rellenar máscaras**. Es el mismo patrón del caso de Puglia (módulo 8): *embeddings congelados + un clasificador simple*.

### ESM-2: más escala, más estructura

[[ESM-1b y ESM-2|ESM-2]] (Lin et al., 2023). La misma receta llevada al extremo: de **8 millones a 15.000 millones** de parámetros. La **perplejidad** baja de **10,45 a 6,37** (el azar sería ~20) y la precisión de contactos mejora en todos los tramos.

Y de ahí sale **[[ESMFold]]**: la secuencia entra al ESM-2 preentrenado, pasa por el *Folding Trunk* y el *Structure Module*, y sale la estructura con su confianza. El ***recycling*** vuelve a pasar el resultado: **se refina sobre su propio borrador**.

| | [[AlphaFold]] 2 | [[ESMFold]] |
|---|---|---|
| ¿Necesita MSA? | **Sí** | **No** |
| Velocidad | Lento | **Muy rápido** |
| De dónde sale la señal | De los homólogos | **Del PLM** |

**14,2 s** para 384 residuos en una V100. Por eso se pudo hacer a escala. Comparado con AlphaFold 2 predicen casi lo mismo **sin que ESMFold vea alineamientos**; y contra el PDB, acierta una proteína metagenómica que **no se parecía a nada conocido**.

### ESM Atlas: el "lado oscuro" de las proteínas

Meta AI (2022). Si predecir estructura es tan rápido y no hace falta alineamiento, **se puede hacer en masa**: predecir la estructura de *todo* lo que se ha secuenciado.

| La escala del [[ESM Atlas\|Atlas]] | |
|---|---|
| Estructuras metagenómicas | **más de 600 millones** |
| Tamaño relativo | **3×** la mayor base anterior |
| Cómputo | 2 semanas en un clúster de ~2.000 GPUs |
| Con alta confianza | solo el **~10 %** — el resto es exploración |

> **Por qué se llama "lado oscuro":** son proteínas de microbios del suelo, del océano y de nuestro cuerpo. **No se parecen a nada conocido**, así que no había forma de estudiarlas. Ahora cada una tiene una estructura.

**El cambio de método:** la escala no es solo "más datos". Cambia **cómo se investiga** — antes se elegía *una* proteína interesante y se le dedicaba un doctorado; ahora se predice el catálogo entero y **después** se busca qué mirar.

---

## 6. La forma se vuelve texto

*Si la estructura se escribe con letras, un modelo de lenguaje **la puede leer**.*

### Paréntesis: Foldseek y el alfabeto 3Di

Antes de [[ProstT5]] hubo un problema práctico: hay **cientos de millones** de estructuras predichas (214 M en AlphaFold DB + 617 M en ESM Atlas). **Compararlas era el cuello de botella.**

> **La idea:** si puedo **escribir la forma con letras**, puedo comparar estructuras con **algoritmos de secuencia**, optimizados por décadas.

Cómo se discretiza el [[Alfabeto 3Di|3Di]]: 10 rasgos geométricos por residuo → se agrupan en **20 estados** → un símbolo por residuo → una **"secuencia" de forma**. El 3Di describe el contacto entre un residuo y **el más cercano en el espacio** (no el vecino en la cadena).

> **Por qué importa:** dos proteínas pueden tener secuencias **totalmente distintas** y aun así **la misma forma**. Comparando forma se detectan parentescos que la secuencia sola ya no ve.

### Foldseek: el resultado

[[Foldseek]] (van Kempen et al., 2024, *Nature Biotechnology* 42:243–246):

| | |
|---|---|
| vs. TM-align y Dali | **> 4.000×** más rápido |
| vs. CE | **> 21.000×** más rápido |
| En bases grandes | hasta **180.000×** |

Y **sin perder sensibilidad**: 86 % de Dali, 88 % de TM-align y **133 % de CE**.

> **Por qué es tan rápido:** no compara geometría, **compara texto**. Convierte un problema carísimo en uno que ya sabíamos resolver rápido.

### ProstT5: cuando la estructura se vuelve texto

Los modelos anteriores leen **solo la secuencia**. Pero una proteína también **es** una estructura 3D. [[ProstT5]] (Heinzinger et al., 2024) usa el **alfabeto 3Di de Foldseek**: como son 20 símbolos, **un PLM lo lee sin cambiar de arquitectura**.

**Traducción en dos sentidos:**

- `<AA2fold>` — secuencia → forma
- `<fold2AA>` — forma → secuencia

| Secuencia → estructura | Estructura → secuencia |
|---|---|
| Predecir el 3Di de una proteína **sin calcular su estructura**, y buscar con eso | ***Inverse folding***: proponer secuencias que adopten una forma dada |
| **×1000 más rápido** que extraer el 3Di de una estructura predicha | Diseño guiado por **la forma**, no por la secuencia |

> **El resultado más fuerte:** el 3Di **predicho** es tan bueno que, pasado a Foldseek, detecta **[[Homología remota|homología remota]]** —proteínas muy divergentes con la misma forma— **casi al nivel de usar estructuras experimentales**. Sin MSA y sin predecir coordenadas 3D: la señal estructural **ya está en los embeddings**.

> [!warning] Ojo con los nombres
> **ProtT5** lee secuencia (1D). **ProstT5** lee secuencia *y* estructura (3D).

### Phold: cuando la estructura anota genomas

Un caso real que combina exactamente las dos piezas anteriores: **ProstT5** (secuencia → 3Di) y **Foldseek** (buscar por forma). Bouras et al. (2026), *Nucleic Acids Research* 54:gkaf1448.

**El problema:** anotar genomas de **[[Bacteriófago|bacteriófagos]]** — los virus más abundantes del planeta y los más difíciles de anotar. Evolucionan tan rápido que **más del 65 %** de sus proteínas no se pueden anotar por homología de secuencia.

**Cómo lo resuelve [[Phold]]:**

1. ProstT5 genera embeddings de **1024 dimensiones por residuo** (encoder de 1000 millones de parámetros).
2. Una **CNN de dos capas** predice el token 3Di de cada residuo.
3. **Foldseek** busca esa "secuencia de forma" contra una base de **1,36 millones** de estructuras predichas.

**El resultado**, sobre 16.460 CDS de fagos:

| Método | % anotado |
|---|---|
| MMseqs2 (secuencia) | 34,7 % |
| PyHMMER (perfil HMM) | 37,7 % |
| **Phold** (estructura) | **49,4 %** |

Y con estructuras de ColabFold sube a **51,5 %**.

> **Lo que demuestra:** la forma **conserva señal que la secuencia ya perdió**. Los fagos con más anotación son justamente los de metabolismo de ácidos nucleicos y funciones enzimáticas.

Es el mismo hallazgo de ESM-1b **llevado a producción**: sin MSA y sin predecir coordenadas 3D, un PLM más un buscador de formas resuelve un problema real. Código abierto en `github.com/gbouras13/phold`.

---

## 7. Secuencia, estructura y función en un mismo modelo

### El siguiente salto: ESM3

Si [[ProstT5]] une **dos** modalidades, [[ESM3]] une **tres** en un mismo vocabulario (Hayes et al., 2025, *Science*):

| Secuencia | Estructura | Función |
|---|---|---|
| Las 20 letras | Coordenadas 3D **como tokens** | Palabras clave, sitios catalíticos |

**98.000 millones de parámetros**, más de 10²⁴ FLOPS: un orden de magnitud más grande que ESM-2. Las tres pistas entran como **tokens discretos** y se fusionan en un solo **espacio latente**; el primer bloque lleva **atención geométrica**, que permite condicionar por coordenadas atómicas.

**Se enmascara todo y se rellena posición por posición.** El diseño se puede **guiar** dando parte de la secuencia, parte de la estructura, o una palabra de función.

### esmGFP: una proteína que no existía

Se le dio **solo la estructura de los residuos del núcleo** de una GFP natural (los que forman y catalizan el cromóforo). ESM3 razonó en cadena, probó **96 generaciones** y encontró proteínas que **fluorescen de verdad**, medidas en lisado de *E. coli*.

Desde el pocillo B8 (57 % de identidad) siguió la cadena hasta C10: **esmGFP**, con **58 % de identidad** y **96 mutaciones sobre 229 aminoácidos**. El equivalente, según los autores, a **≈ 500 millones de años** de evolución.

> [!note] Matiz importante
> No es que el modelo **"sepa" biología**. Simula evolución porque **predecir el token enmascarado lo obliga** a aprender cómo se mueve la evolución en el espacio de proteínas posibles.

### ¿Qué aprende de las secuencias sin etiquetar?

Se entrena **solo con secuencias sin etiquetar**. Nadie le dice qué es la hidrofobicidad. Y sin embargo aprende:

- **Propiedades biofísicas** — hidrofobicidad, carga, peso.
- **Estructura secundaria** — hélices y láminas.
- **Contactos 3D** — qué residuos están cerca.

> **Por qué funciona:** la evolución **ya resolvió el problema**. Las secuencias que existen son las que **se pliegan y funcionan**. El modelo absorbe esas restricciones sin que nadie se las explicite.

De la fidelidad al *prompt* (figura 2A del paper) sale un matiz útil: **promptear por estructura funciona muy bien** (cRMSD bajo con pTM alto), mientras que **SASA y palabras clave son las pistas más flojas**.

---

## 8. Un caso de aplicación: ¿dónde actúa la proteína?

El trabajo de tesis de **Juan Diego Puglia** (ORT) — predecir la **localización subcelular** de proteínas bacterianas.

**El flujo:**

```
secuencia aminoacídica
   → ProstT5 | ESM-C 300m | ESM-C 600m        (tres PLMs)
   → embeddings (un vector por proteína)
   → Random Forest | SVM                       (clasificadores clásicos)
   → evaluación → interfaz gráfica (Tkinter)
```

**Los datos:** **ePSORTdb 4.0** (localización determinada *experimentalmente*), 11.781 entradas, descartando las de ubicación múltiple. Partición 67 % entrenamiento / 33 % evaluación con `train_test_split` de scikit-learn, **estratificada** (`stratify=y`) para conservar la proporción de clases.

> **No hace falta entrenar un modelo gigante**: un PLM **ya entrenado** más un clasificador clásico resuelve el problema.

**Los resultados** (F1 ponderado sobre el conjunto de prueba):

| Clasificador | F1 ponderado |
|---|---|
| **SVM** | **96,02 %** |
| Random Forest | 94,50 % |

Los dos pasaron el 90 % con **todos** los modelos de lenguaje probados. El mejor: **ESM-C 300m** — el más chico de los tres.

**Dónde acierta y dónde no:**

| Clase | Verdaderos positivos | % del dataset |
|---|---|---|
| *Cytoplasmic* | 98 % | 61 % |
| *Cellwall* | 83 % | — |
| *Periplasmic* | 82 % | **0,93 %** |

> El error se concentra en las **clases minoritarias**: no es que el modelo no sepa, es que **hay pocos ejemplos**.

**El contraste que importa:** un clasificador clásico sobre **embeddings congelados** saca 96 %. No hizo falta entrenar nada grande — **hizo falta el vector adecuado**. Y quedó usable: una interfaz gráfica en Python donde se pega una secuencia en FASTA y devuelve la localización, publicada en `huggingface.co/jpuglia/ProteinLocationPredictor`.

### ¿Más grande, o mejor diseñado?

| La narrativa del *scaling* | Ankh: el contrapunto |
|---|---|
| Más parámetros → representaciones más ricas | Optimiza **para proteínas** en vez de escalar |
| Tendencia dominante | Estado del arte con **< 10 %** de parámetros |
| Cuesta cómputo, dinero y energía | **< 7 %** de inferencia · **< 30 %** de dimensión |

> **La accesibilidad importa:** un modelo que corre en hardware modesto **democratiza la investigación**. *(Elnaggar et al., arXiv:2301.06568)*

Es el mismo mensaje que el resultado de Puglia desde otro ángulo: el modelo más chico fue el mejor.

---

## 9. Cierre: los límites

### Lo que estos modelos *no* hacen

> **No "entienden" biología.** Aprenden **correlaciones estadísticas de la evolución**. No simulan física, ni química, ni termodinámica.

| Situación | Qué pasa |
|---|---|
| Proteína **sin homólogos** conocidos | Poco de dónde aprender |
| Mutación que cambia **la física** | Puede no anticiparla |
| Condiciones ***in vivo*** reales | Fuera de su alcance |

> **Un buen *score in silico* es una hipótesis, no un resultado.**

Es exactamente la misma conclusión de la clase 6 sobre los scores de docking.

### De la laptop al supercómputo

| Usar un PLM | Entrenar un PLM |
|---|---|
| Pesos preentrenados (HuggingFace) | Miles de GPU-hora |
| Inferencia en una GPU de consumo | Clusters especializados |
| **Accesible hoy** | **Barrera real de entrada** |

> **Entrenar es de pocos; usar es de casi todos.** Ahí es donde podés aportar hoy.

### Tres ideas para llevarse

1. **Una proteína es texto en 20 símbolos**, y su gramática **conecta posiciones lejanas**.
2. **Un embedding vuelve geometría el significado**; el contexto **reescribe el vector**.
3. **Los PLMs aprenden evolución acumulada, no física.** *La mesada sigue mandando.*

## Ideas para retener

- El hilo de toda la clase es **cuánto contexto ve el modelo**: una letra ([[ProtVec]]) → su entorno ([[ELMo y SeqVec|SeqVec]]) → la secuencia entera ([[Transformer]], [[ESM-1b y ESM-2|ESM]]) → la forma ([[ProstT5]]) → la función ([[ESM3]]).
- La **tarea de predecir el token tapado es un pretexto**: lo que se guarda son los pesos internos, no la predicción. Eso vale desde word2vec hasta ESM3.
- **La arquitectura define el uso:** autorregresiva para *generar*, bidireccional para *etiquetar residuos*, *masked* para *representar*.
- **La estructura emerge sin que nadie la enseñe** — pero hace falta una **sonda entrenada** (un clasificador chico) para leerla de los embeddings.
- **Escribir la forma con letras** ([[Alfabeto 3Di|3Di]]) convierte la comparación estructural en comparación de texto: 4 órdenes de magnitud más rápido, y habilita anotar por forma lo que la secuencia ya no alcanza ([[Phold]]).
- **Sin MSA.** La información evolutiva que los métodos clásicos sacaban de un alineamiento, el modelo la aprendió de ver millones de secuencias. Eso es lo que hace a [[ESMFold]] rápido y lo que permitió el [[ESM Atlas]].
- **Embeddings congelados + clasificador simple** resuelve tareas reales con 96 % de F1. Y el modelo más chico puede ganarle al más grande.
- El límite es honesto: **correlaciones de la evolución, no física**. Un score in silico es una hipótesis.

## Para seguir explorando

**Revisiones y papers**

| Referencia | Sobre qué |
|---|---|
| Pérez-Villanueva et al. (2026). *Descifrando el Lenguaje de las Proteínas*. TIES, UNAM | Revisión en español |
| Leclercq & Droit (2025). *Protein Language Models*. J. Proteome Res. | Revisión general |
| Elnaggar et al. (2023). *Ankh*. arXiv:2301.06568 | El contrapunto al *scaling* |
| Heinzinger et al. (2024). *ProstT5: bilingual sequence–structure*. NAR Genom. Bioinform. 6(4), lqae150 | El modelo bilingüe |
| van Kempen et al. (2024). *Foldseek*. Nat. Biotechnol. 42:243–246 | El alfabeto 3Di |
| Hayes et al. (2025). *ESM3*. Science | El salto multimodal y generativo |

**Modelos**

| Modelo | Dónde |
|---|---|
| ESM / ESM-2 / ESMFold | `huggingface.co/facebook` |
| ESM-C | `huggingface.co/EvolutionaryScale` |
| ESM3 (1.4B abierto, MIT) | `github.com/evolutionaryscale/esm` |
| ProtT5 / ProtBERT | `huggingface.co/Rostlab` |
| **ProstT5** (secuencia + estructura) | `huggingface.co/Rostlab/ProstT5` |
| ProtGPT2 · ZymCTRL | `huggingface.co/nferruz` · `huggingface.co/AI4PD` |
| Foldseek (alfabeto 3Di) | `search.foldseek.com` |
| AggrescanAI (caso aplicado) | `gitlab.com/bioinformatics-fil/aggrescanai` |

## Conexiones

- Viene de → [[Métodos para el diseño computacional de fármacos]] (clase 6). Allá, la tabla de **representaciones de proteínas** ponía "secuencia → modelos de lenguaje" como una fila: esta clase es esa fila desplegada. Y el argumento de fondo es el mismo: **reemplazar descriptores diseñados a mano por representaciones aprendidas**.
- El puente concreto entre las dos clases es [[AlphaFold]]: en la clase 6 aparece como la solución al problema de "¿y si la estructura no está en el PDB?"; acá aparece como el punto de comparación de [[ESMFold]], que hace lo mismo **sin alineamientos**.
- Del Módulo 1 → [[Basecalling]] y [[Segmentación celular]] ya eran deep learning aplicado a datos biológicos; acá el modelo deja de procesar señales y pasa a **representar y generar** biología.
- Índice → [[Módulo 3 - MOC]]
