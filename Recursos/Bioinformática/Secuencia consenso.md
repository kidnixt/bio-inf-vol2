---
tags: [bioinformática, calidad, ensamblaje]
area: Bioinformática
aliases: [consenso, cobertura, consensus, profundidad de cobertura]
---

# Secuencia consenso

La secuencia que resulta de combinar **muchas lecturas que cubren la misma posición**, en lugar de confiar en una sola. Es la distinción operativa más importante para entender la calidad en [[Secuenciación con nanoporos|nanoporos]].

## Lectura individual ≠ consenso

| | Lectura individual | Consenso |
|---|---|---|
| Qué la determina | Poro y química, modelo y versión de [[Basecalling\|basecalling]], modo simplex o [[Secuenciación dúplex\|dúplex]] | **Cobertura**, corrección previa de errores, [[Pulido de secuencias\|pulido]], calidad inicial de las lecturas |
| Valor típico ONT | [[Calidad Phred\|Q26]] simplex, Q30+ dúplex | Muy superior con buena cobertura |

Una plataforma con lecturas de Q26 puede producir genomas bacterianos de altísima exactitud, siempre que la cobertura sea suficiente y los errores sean **aleatorios**. Si los errores son **sistemáticos** —[[Homopolímeros|homopolímeros]], contextos metilados— la cobertura no los corrige: los confirma.

## Cobertura

La cobertura (o profundidad) es cuántas lecturas independientes respaldan cada posición. Es el parámetro que el analista puede subir sin cambiar de tecnología, y por eso es la primera palanca cuando se necesita más exactitud.

En [[Metagenómica clínica|metagenómica]] es también el límite práctico: la fracción microbiana es pequeña, la cobertura por organismo es baja, y por eso *"no siempre se recupera cobertura suficiente para ensamblado"*, lo que limita AMR, tipado y [[Vigilancia genómica hospitalaria|vigilancia]].

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
