---
tags: [concepto, bioinformática, farmacología]
area: Bioinformática
aliases: [ADME, ADME-Tox, absorción distribución metabolismo excreción]
---

# ADMET

**Absorción, Distribución, Metabolismo, Excreción y Toxicidad**: el destino de una molécula en el organismo. Es una de las cuatro propiedades que el ciclo de diseño intenta optimizar a la vez.

| Propiedad | Qué mide |
|---|---|
| **Afinidad** | Fuerza de unión al blanco ([[Energía libre de unión]]) |
| **Potencia** | Concentración necesaria para un efecto |
| **Selectividad** | Preferencia entre blancos |
| **ADMET** | **Destino en el organismo y toxicidad** |

## Por qué está en la clase

Porque es donde mueren la mayoría de los candidatos. La frase de la primera diapositiva de contenido lo dice sin rodeos:

> **Afinidad y potencia ayudan. La exposición y la seguridad condicionan el beneficio.**

Una molécula que se une perfecto al blanco pero no se absorbe, se metaboliza en minutos, no llega al tejido o es tóxica, **no es un fármaco**. Por eso el [[Descubrimiento y desarrollo de fármacos|desarrollo]] tiene una etapa preclínica entera dedicada a *exposición y seguridad*, y por eso el diseño computacional intenta anticipar ADMET desde el principio en vez de dejarlo para el final.

## Cómo se predice

- **Filtros heurísticos** sobre propiedades fisicoquímicas: ver [[Reglas de drug-likeness]] (logP, PSA y peso molecular son proxies clásicos de absorción y permeabilidad).
- **Modelos [[QSAR]]** entrenados sobre datos de [[ChEMBL]], que incluye datos ADMET.
- **Modelos multitarea** de [[Deep Learning|deep learning]]: el aporte de la IA que la clase señala es pasar de *un modelo para cada propiedad* a **modelos multitarea y preentrenados**, que aprovechan la correlación entre propiedades.

En los pipelines de [[Virtual screening]] a gran escala aparece como filtro final: V-SYNTHES2, por ejemplo, filtra los hits por PAINS y ADME-Tox antes de seleccionar los 100 compuestos para ensayo.

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
