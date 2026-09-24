---
tags: [lectura, modulo-3, estructura, búsqueda]
area: Lecturas
tipo: brief communication
autores: Michel van Kempen, Stephanie S. Kim, Charlotte Tumescheit, Milot Mirdita, Jeongjae Lee, Cameron L. M. Gilchrist, Johannes Söding, Martin Steinegger
año: 2024
revista: Nature Biotechnology 42, 243–246
doi: 10.1038/s41587-023-01773-0
aliases: [van Kempen 2024, Foldseek paper, "Fast and accurate protein structure search with Foldseek"]
---

# van Kempen et al. (2024) — *Fast and accurate protein structure search with Foldseek*

> [!info] Ficha de la lectura
> **Tipo:** *Brief Communication* — *Nature Biotechnology*
> **Autores:** Söding (Max Planck, Göttingen) y Steinegger (Seoul National University)
> **Clase asociada:** [[Modelos de lenguaje de proteínas y embeddings proteicos]] (clase 9)
> **PDF:** [[van Kempen et al 2024 - Foldseek.pdf]]
> **Servidor:** `search.foldseek.com`

## En una frase

El paper de **[[Foldseek]]** y del **[[Alfabeto 3Di|alfabeto 3Di]]**: describir las interacciones terciarias de una proteína como una **secuencia sobre un alfabeto estructural** convierte la búsqueda de estructuras en búsqueda de texto, con 4–5 órdenes de magnitud de aceleración.

## Por qué leerla después de la clase

La clase lo presenta como un "paréntesis" antes de [[ProstT5]], y es exacto: sin el 3Di no hay ProstT5 ni [[Phold]]. El paper explica **por qué** los alineadores estructurales clásicos eran lentos, que es la parte que la diapositiva comprime.

---

## 1. El problema

Las bases de estructuras predichas se volvieron el cuello de botella:

- **214 millones** de estructuras en [[AlphaFold DB]] (EBI, al momento del paper).
- **617 millones** en el [[ESM Atlas]].

Los alineadores estructurales (TM-align, Dali, CE) son lentos por dos razones que el paper detalla: las herramientas de búsqueda de secuencias usan **prefiltros rápidos y sensibles** para ganar órdenes de magnitud, y en estructura no había un equivalente.

## 2. La solución

Describir las **interacciones terciarias entre aminoácidos** como secuencias sobre un alfabeto estructural de **20 estados**: para cada residuo, se caracteriza geométricamente su relación con **el residuo más cercano en el espacio** (no en la cadena), con 10 rasgos que se agrupan en 20 clases.

Con eso, toda la maquinaria de alineamiento de secuencias —prefiltros, k-mers, Smith-Waterman— se aplica directamente.

## 3. Los números

| Comparación | Aceleración | Sensibilidad retenida |
|---|---|---|
| vs. **TM-align** | > 4.000× | **88 %** |
| vs. **Dali** | > 4.000× | **86 %** |
| vs. **CE** | > 21.000× | **133 %** |
| En bases grandes | hasta **180.000×** | — |

Un ejemplo que da el paper para dimensionar: una comparación todos-contra-todos de 100 millones de secuencias le tomaría a MMseqs2 alrededor de **una semana** en el mismo clúster.

## 4. Qué aporta respecto de la clase

- **La explicación del cuello de botella**, que es lo que justifica el diseño. La diapositiva dice "compararlas era el cuello de botella"; el paper dice *por qué* — faltaba el prefiltro.
- **El detalle de que 3Di describe el vecino más cercano en el espacio**. Eso es lo que hace que el alfabeto codifique información **terciaria** y no local, y por lo tanto lo que permite detectar [[Homología remota|homología remota]].
- **Que sea de 20 letras no es casualidad ni mera coincidencia estética**: es lo que después permite que [[ProstT5]] lo lea *sin cambiar de arquitectura*. Foldseek lo inventó; ProstT5 lo aprendió.

## Conceptos del vault

[[Foldseek]] · [[Alfabeto 3Di]] · [[Homología remota]] · [[AlphaFold DB]] · [[ESM Atlas]] · [[ProstT5]] · [[Phold]] · [[Alineamiento de secuencias]]

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
- [[Módulo 3 - MOC]]
