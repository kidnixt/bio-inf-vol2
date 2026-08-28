---
tags: [concepto, bioinformática, análisis]
area: Bioinformática
---

# Pseudobulk

Estrategia para hacer [[Expresión diferencial]] **entre condiciones** en datos de [[scRNA-seq]] sin caer en el problema de las pseudo-réplicas: se **agregan** (suman o promedian) los conteos de todas las células de un mismo tipo celular dentro de cada muestra, reconstruyendo un perfil tipo bulk por muestra y por tipo.

```
10.000 células × 6 muestras
        ↓ agrupar por (muestra, tipo celular)
6 valores por gen para las neuronas
6 valores por gen para los astrocitos
...
        ↓ test estadístico con n = 6 muestras
```

## Por qué es lo correcto

La unidad de replicación biológica es **la muestra o el individuo**, no la célula. Las células de un mismo donante comparten genotipo, ambiente y procesamiento técnico: no son independientes. Tratarlas como réplicas infla el n de miles de veces y produce p-valores absurdamente pequeños para diferencias triviales.

## Lo que se gana además

- Se puede usar todo el arsenal maduro del [[Bulk RNA-seq]] (DESeq2, edgeR), pensado precisamente para conteos con pocas réplicas.
- La agregación **reduce la [[Sparsity]]**: sumar miles de células convierte una matriz llena de ceros en conteos robustos.

## Lo que se pierde

La distribución dentro del tipo celular. Si sólo una subpoblación responde al tratamiento, el promedio la diluye — que es exactamente la limitación del bulk que motivó el single cell. Por eso el pseudobulk no reemplaza al análisis por célula: lo complementa para la parte inferencial.

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
