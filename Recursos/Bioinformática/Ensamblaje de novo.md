---
tags: [bioinformática, ensamblaje, genómica]
area: Bioinformática
aliases: [de novo assembly, ensamblado, ensamblaje, genoma cerrado, haplotipo-resuelto]
---

# Ensamblaje de novo

Reconstruir un genoma a partir de las lecturas **sin usar una referencia**. Es una de las tres familias de herramientas que hubo que rediseñar cuando llegó la [[Secuenciación de tercera generación|tercera generación]], junto con la [[Pulido de secuencias|corrección y pulido]] y el análisis de [[Variantes estructurales|variantes]].

## Por qué las lecturas largas lo cambiaron todo

El ensamblaje con [[Secuenciación de segunda generación|lecturas cortas]] es un problema de resolución de ambigüedades: cada vez que una repetición es más larga que la lectura, el grafo se bifurca y el ensamblado se fragmenta en contigs. Con una lectura que **atraviesa entera** la repetición, la ambigüedad desaparece por construcción.

De ahí el salto que enuncia la clase:

> **De secuenciar genomas a obtener genomas completos**: bacterianos, e incluso genomas humanos completos y **haplotipo-resueltos**.

"Completo" aquí significa cerrado: un cromosoma bacteriano circular en una sola pieza, con sus [[Plásmido|plásmidos]] resueltos por separado. "Haplotipo-resuelto" significa poder separar las dos copias parentales de cada cromosoma en lugar de colapsarlas en un consenso.

## En el flujo de nanoporos

El ensamblaje se apoya en la [[Secuencia consenso|secuencia consenso]] y el [[Pulido de secuencias|pulido]] para compensar el [[Perfil de error]] de las lecturas individuales. En el flujo de [[Metagenómica clínica|metagenómica clínica]] de la clase, la etapa de ensamblaje/consenso usa **minimap2** para el mapeo y **Medaka** y **bcftools** para variantes y consenso, y es la que habilita después el tipado y la [[Vigilancia genómica hospitalaria|vigilancia]].

Su límite en metagenómica es la cobertura: *"no siempre se recupera cobertura suficiente para ensamblado"*, y eso **limita AMR, tipado y vigilancia**.

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
