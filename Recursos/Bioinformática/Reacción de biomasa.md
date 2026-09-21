---
tags: [concepto, bioinformática, modelado]
area: Bioinformática
aliases: [biomasa, biomass, v_bio, función objetivo, biomass reaction]
---

# Reacción de biomasa

Una reacción artificial de un [[Modelo metabólico a escala genómica]] que representa **fabricar una unidad de célula nueva**: consume, en las proporciones medidas experimentalmente, todos los componentes necesarios (aminoácidos, nucleótidos, lípidos, polisacáridos de pared, cofactores, ATP de mantenimiento) y "produce" biomasa.

## Por qué importa

- Es la **función objetivo** habitual de [[Flux Balance Analysis|FBA]]: `max v_bio`. Su flujo es la tasa de crecimiento predicha.
- Es lo que define qué significa **crecer** en el modelo. Si un precursor necesario para la biomasa no puede producirse, el crecimiento es 0.

En el ejemplo de [[StrainDesign]] con *E. coli core*, la reacción se llama `BIOMASS_Ecoli_core_w_GAM` (GAM: *growth-associated maintenance*, el ATP asociado al crecimiento).

## Su rol en el caso de co-consumo

El diseño seleccionado en la clase funciona **porque** la biomasa necesita componentes que cada azúcar aporta de forma exclusiva:

| Componente de biomasa | Azúcar que lo aporta en el diseño |
|---|---|
| Glucanos de pared (β-1,3 y β-1,6-glucano), glucógeno, trehalosa | Glucosa |
| Nucleótidos (adenosina) y aminoácidos aromáticos | Arabinosa |
| Precursores derivados de α-cetoglutarato y la mayor parte del ATP, NADH y NADPH | Xilosa |

Si falta cualquiera de los tres azúcares, falta un componente de la biomasa y el flujo de crecimiento cae a 0. Ver [[Co-consumo de azúcares]] y [[Cofactores energéticos]].

En la ecuación global del diseño, la biomasa aparece normalizada a **1** y todo lo demás se expresa relativo a ella.

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
