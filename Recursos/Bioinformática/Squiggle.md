---
tags: [bioinformática, nanoporos, señal]
area: Bioinformática
aliases: [señal cruda, corriente iónica, traza de corriente, raw signal]
---

# Squiggle

El nombre informal de la **traza de corriente iónica** que registra un nanoporo mientras una molécula lo atraviesa: la señal cruda, antes de cualquier interpretación como secuencia.

Es literalmente lo que dibujó [[David Deamer]] en su cuaderno el 25 de junio de 1989: una línea escalonada con las letras de las bases debajo.

## Qué contiene

Cada nivel de la traza corresponde al bloqueo de corriente producido por un **[[K-mer|k-mer]]** ocupando la región sensible del poro. La secuencia de niveles y la duración de cada uno son lo que el [[Basecalling|basecaller]] tiene que decodificar.

De ahí que el squiggle contenga **más información que la secuencia**: la duración de cada estado, la forma de las transiciones y desviaciones sutiles del nivel esperado llevan información sobre [[Metilación del ADN|bases modificadas]], velocidad de translocación y estructura de la molécula. La secuencia en [[FASTQ]] es una proyección con pérdida de ese objeto.

## Dónde vive

Se almacena en formato [[POD5]] (antes FAST5). Conservarlo es lo que permite **rebasecallear** después con modelos mejores.

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
