---
tags: [técnica, metagenómica, clínica]
area: Técnicas
aliases: [depleción de ADN del hospedador, host depletion, eliminación de ADN humano]
---

# Depleción de ADN humano

Paso de laboratorio que reduce selectivamente el ADN del hospedador en una muestra clínica antes de secuenciar, para que la fracción microbiana ocupe una proporción mayor de las lecturas.

## Por qué es necesario

En una muestra respiratoria, sangre o tejido, la enorme mayoría del ADN es **humano**. Sin depleción, la [[Metagenómica clínica|metagenómica]] gasta casi todo el rendimiento del secuenciador leyendo el genoma del paciente. La clase lo señala como **el principal cuello de botella** de la metagenómica clínica, junto con la reproducibilidad del análisis.

## Cómo se complementa con la bioinformática

La depleción física (lisis diferencial, captura de ADN metilado del hospedador, digestión) se complementa siempre con una **depleción computacional**: alinear las lecturas contra **GRCh38** y descartar las que mapean. Esa etapa cumple además una función de **privacidad**, no solo de eficiencia.

## Su costo

> La depleción de ADN humano **puede reducir también material microbiano**, y el rendimiento varía según el tipo de muestra.

Es una de las seis limitaciones de la metagenómica clínica listadas en la clase: mejora la señal pero introduce un sesgo de composición que afecta especialmente a los microorganismos poco abundantes.

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
