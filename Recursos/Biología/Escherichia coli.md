---
tags: [organismo, biología, bacteria]
area: Biología
aliases: [E. coli, coli, iML1515]
---

# Escherichia coli

La bacteria modelo por excelencia, y el organismo de los ejemplos de modelado de la clase.

## iML1515

El [[Modelo metabólico a escala genómica]] de *E. coli* que muestra la clase, alojado en [[BiGG Models]]:

| Campo | Valor |
|---|---|
| Organismo | *Escherichia coli* str. K-12 substr. MG1655 |
| Genoma | NC_000913.3 |
| Metabolitos | 1877 |
| Reacciones | 2712 |
| Genes | 1516 |
| Formatos | [[SBML]] (`.xml`), JSON, MAT |

Existe también una versión reducida, el modelo *core*, que se usa para ejemplos y pruebas rápidas: en la diapositiva de otras aplicaciones de [[StrainDesign]] aparecen sus identificadores `BIOMASS_Ecoli_core_w_GAM` (la [[Reacción de biomasa]]) y `EX_14bdo_e` (exportación de 1,4-butanodiol).

## Como hospedero de diseño

La clase menciona la **fijación de CO₂ en *E. coli*** como ejemplo de otra aplicación posible del mismo método: armar la lista de reacciones candidatas, agregarlas al modelo, definir los fenotipos deseados y correr.

El primer esquema de la clase — glucosa → piruvato con las ramas a lactato, acetato, etanol, formiato, acetoína y succinato — es también el metabolismo fermentativo típico de este tipo de bacterias.

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
