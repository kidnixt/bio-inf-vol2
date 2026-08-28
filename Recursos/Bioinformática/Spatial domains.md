---
tags: [concepto, bioinformática, espacial, análisis]
area: Bioinformática
aliases: [dominios espaciales]
---

# Spatial domains (dominios espaciales)

Regiones **contiguas** del tejido con un perfil molecular coherente. Son el equivalente espacial de los clusters: donde el [[Clustering]] agrupa células por similitud transcriptómica, el dominio espacial agrupa **posiciones** por similitud transcriptómica **y** proximidad física.

## Ejemplos

- Las capas de la corteza cerebral
- Las zonas de un ganglio linfático (folículo, zona T)
- El núcleo, el borde invasivo y el estroma de un tumor
- Los gradientes metabólicos alrededor de un vaso ([[Célula endotelial]])

## Por qué no salen de un scRNA-seq

Un dominio no es un [[Tipo celular]]: puede contener varios tipos en proporciones características. Es una propiedad **emergente de la organización**, y por definición desaparece al disociar el tejido. Sólo la [[Transcriptómica espacial]] los recupera.

## Cómo se detectan

Métodos de clustering que incluyen la coordenada espacial como parte de la métrica de similitud, penalizando soluciones que fragmentan regiones contiguas. La idea de fondo: dos spots vecinos tienen a priori más probabilidad de pertenecer al mismo dominio que dos spots lejanos.

## Cuidado

Artefactos con estructura espacial —[[Lateral diffusion]], [[Autofluorescencia]] no uniforme, gradientes de permeabilización— pueden **simular** dominios. Un dominio detectado necesita una interpretación anatómica antes de tomarse en serio.

## Relacionado

[[Neighborhoods]], [[Spatial niches]].

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
