---
tags: [bioinformática, calidad, ensamblaje]
area: Bioinformática
aliases: [polishing, pulido, corrección de errores, error correction, Medaka]
---

# Pulido de secuencias

Corregir los errores residuales de un ensamblado o de una [[Secuencia consenso|secuencia consenso]] volviendo a alinear las lecturas contra él y reevaluando cada posición. Junto con el [[Ensamblaje de novo|ensamblaje]] y el análisis de [[Variantes estructurales|variantes]], es una de las familias de herramientas que nacieron con la [[Secuenciación de tercera generación|tercera generación]].

## Por qué existe

El [[Perfil de error|error]] de una lectura individual de nanoporos es de ~0,25% (Q26) en simplex. El de un ensamblado bien pulido es varios órdenes de magnitud menor. Toda esa diferencia la produce el posprocesamiento: **la exactitud del consenso no es la exactitud de las lecturas**.

En la clase esto aparece como el bloque C de los factores de calidad —**cobertura y posprocesamiento**—, que *"afecta sobre todo la exactitud del consenso, no la de cada read individual"*.

## Dos variantes

| Enfoque | Qué usa |
|---|---|
| **Pulido con las mismas lecturas** | Re-mapea las reads ONT y corrige con un modelo del error de la plataforma — es lo que hace **Medaka**, entrenada sobre el perfil de error de cada química y modelo de [[Basecalling\|basecalling]] |
| **Pulido híbrido** | Usa lecturas cortas de [[Illumina]] de alta exactitud para corregir el esqueleto largo de ONT |

Que Medaka esté entrenada por química y por modelo de basecalling refuerza el punto sobre **trazabilidad**: la versión del software forma parte del resultado.

## Su límite

El pulido corrige errores **aleatorios**. Los errores **sistemáticos** —los que se repiten en todas las lecturas del mismo contexto, típicamente en [[Homopolímeros|homopolímeros]] o alrededor de [[Metilación del ADN|bases modificadas]]— sobreviven al pulido, porque más cobertura del mismo error no lo revela como error. Para esos hace falta cambiar la química, el modelo o el modo de lectura.

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
