---
tags: [biología, epigenética, microbiología]
area: Biología
aliases: [metiloma, 6mA, 4mC, 5mC, 5hmC, bases modificadas, epigenética bacteriana, modificaciones de bases]
---

# Metilación del ADN

Adición de grupos metilo a determinadas bases del ADN, sin cambiar la secuencia. En bacterias los tres tipos principales son:

| Modificación | Base |
|---|---|
| **6mA** | N6-metiladenina |
| **4mC** | N4-metilcitosina |
| **5mC** | 5-metilcitosina |

## Qué hace en bacterias

Clásicamente se la asocia a los sistemas de **restricción-modificación**: la bacteria metila su propio ADN en motivos específicos, y degrada el ADN extraño que no lleva esa marca. Es un sistema inmune primitivo.

Pero el trabajo sobre comunidades bacterianas y virales del **hielo marino** que cita la clase encontró más que eso: allí la metilación **no solo participa en la defensa frente a ADN extraño**, sino que podría **regular la adaptación metabólica** bacteriana y **mediar las interacciones entre fagos y hospedadores**.

*Kanaan & Deming, ISME J 2025*

## Por qué los nanoporos la leen gratis

La [[Secuenciación con nanoporos|secuenciación con nanoporos]] lee **ADN nativo**: una base metilada tiene distinta forma y volumen, y por lo tanto produce un bloqueo de corriente sutilmente distinto en el [[Squiggle|squiggle]]. La información **ya está en la señal**.

- [[Dorado]] puede realizar **conjuntamente** el [[Basecalling|basecalling]] y la inferencia de modificaciones, con modelos preentrenados; las probabilidades salen como *tags* MM/ML en el BAM.
- En ARN se detectan además m6A, m5C, pseudouridina, inosina y 2'-O-metilaciones.
- La condición es que la [[Preparación de bibliotecas de secuenciación|biblioteca]] sea de **ADN nativo**: cualquier paso de PCR borra las modificaciones.

Contrasta con el método clásico (conversión con bisulfito), que requiere un ensayo aparte, destruye ADN y no distingue 6mA ni 4mC.

## Su uso en metagenómica: huellas epigenéticas

ONT permite descubrir **directamente y *de novo*** los tres tipos de metilación, tanto en bacterias individuales como en microbiomas — de ahí la herramienta [[Nanodisco]].

> Las metilaciones se utilizan principalmente como **huellas epigenéticas naturales para identificar y relacionar componentes del metagenoma**.

Cada especie tiene su propio repertorio de metiltransferasas y por lo tanto su propia firma de motivos metilados. Esa firma permite asignar contigs y [[Plásmido|plásmidos]] a su genoma hospedador, un problema de *binning* que la composición y la cobertura solas no resuelven.

## Su costo

La contracara aparece en el [[Perfil de error]]: 5mC, 6mA y otras modificaciones **alteran la señal y pueden inducir errores puntuales** si el modelo de basecalling no las contempla. Un benchmark de [[Plataformas emergentes de nanoporos|CycloneSEQ]] reporta justamente errores de sustitución asociados a metilación.

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
- [[Stuart and Satija 2019 - Integrative single-cell analysis]] *(lectura)*
