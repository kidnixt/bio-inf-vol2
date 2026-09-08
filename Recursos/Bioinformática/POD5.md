---
tags: [bioinformática, formato, nanoporos]
area: Bioinformática
aliases: [FAST5, pod5, fast5, formato de señal]
---

# POD5

El formato en el que [[Secuenciación con nanoporos|ONT]] almacena la **señal eléctrica cruda** ([[Squiggle|squiggle]]) de cada lectura. Reemplaza al formato anterior, **FAST5** (basado en HDF5), con mejor rendimiento de lectura y escritura y menor tamaño.

## Su lugar en el flujo

```
nanoporo → POD5 (señal) → basecaller → FASTQ / BAM (secuencia)
```

El [[Basecalling|basecaller]] toma los POD5 y produce [[FASTQ]] o BAM. Ver [[Dorado]].

## Por qué conservarlo importa

El POD5 es el **dato primario real** de un experimento de nanoporos; el FASTQ es una interpretación suya. Guardarlo permite:

- **Rebasecallear** con modelos más nuevos y ganar exactitud años después, sin repetir el experimento.
- Re-analizar [[Metilación del ADN|bases modificadas]] con modelos que quizás no existían al momento de la corrida.
- Auditar y **trazar** el resultado, requisito del [[Uso clínico y marco regulatorio|uso clínico]].

El costo es de almacenamiento: la señal ocupa bastante más que la secuencia, y decidir cuánto tiempo conservarla es una decisión real de infraestructura — la misma discusión de [[Almacenamiento y visualización]] que apareció en las clases anteriores del módulo.

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
