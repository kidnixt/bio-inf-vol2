---
tags: [concepto, bioinformática, análisis]
area: Bioinformática
aliases: [DEG, DEGs, genes diferencialmente expresados, análisis de expresión diferencial]
---

# Expresión diferencial

Identificar los genes cuya expresión difiere significativamente entre dos grupos. Es el análisis más clásico de la transcriptómica y sigue siendo central en single cell.

## Dos usos distintos en scRNA-seq

| Comparación | Para qué sirve |
|---|---|
| **Entre clusters** | Encontrar genes marcadores → [[Anotación de tipos celulares]] |
| **Entre condiciones** | Encontrar la respuesta biológica (tratado vs control, sano vs enfermo) dentro de un mismo [[Tipo celular]] |

Son estadísticamente muy distintos, aunque se usen las mismas herramientas.

## La trampa de las pseudo-réplicas

Al comparar **entre condiciones**, tratar cada célula como una réplica independiente es un error grave: las células de un mismo individuo no son independientes entre sí. Con 10.000 células por muestra, el n aparente es enorme y **cualquier diferencia da significativa**. Los p-valores resultantes son basura.

La solución que menciona la clase es el [[Pseudobulk]]: agregar las células por muestra y por tipo celular, y hacer el test sobre las réplicas biológicas reales.

> Comparar **entre clusters** dentro de una misma muestra no sufre este problema de la misma manera, pero tiene otro: los clusters se definieron a partir de las mismas diferencias de expresión que después se testean (*double dipping*), lo que también infla la significancia.

## Downstream

Las listas de DEGs suelen interpretarse con enriquecimiento funcional — ver [[Gene Ontology]].

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
