---
tags: [bioinformática, formato]
area: Bioinformática
aliases: [fastq, formato FASTQ]
---

# FASTQ

El formato estándar para secuencias con calidad por base. Cada lectura ocupa cuatro líneas: identificador, secuencia, separador y una cadena de caracteres que codifica el [[Calidad Phred|Q-score]] de cada base.

Es la salida del [[Basecalling|basecalling]] a partir de los [[POD5]], y el punto de entrada de casi toda la bioinformática posterior: filtrado, [[Alineamiento de secuencias|alineamiento]], [[Ensamblaje de novo|ensamblaje]], [[Clasificación taxonómica|clasificación taxonómica]].

## En el contexto de nanoporos

[[Dorado]] puede emitir directamente **BAM o CRAM** en lugar de FASTQ, y en la práctica lo hace cuando se piden [[Metilación del ADN|bases modificadas]]: las probabilidades de modificación viajan como *tags* **MM/ML**, que FASTQ no puede representar. El FASTQ, en ese sentido, se queda corto para el dato que ONT genera.

Que las [[Plataformas emergentes de nanoporos|plataformas emergentes]] declaren que "algunas herramientas creadas para ONT pueden aceptar su FASTQ" muestra el otro rol del formato: es el **lenguaje común** que permite que un ecosistema de software construido para una plataforma funcione con otra.

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
