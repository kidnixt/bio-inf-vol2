---
tags: [técnica, secuenciación, nanoporos]
area: Técnicas
aliases: [nanopore sequencing, secuenciación por nanoporos, ONT sequencing, nanoporos]
---

# Secuenciación con nanoporos

Tecnología de [[Secuenciación de tercera generación|tercera generación]] que lee una molécula **nativa** de ADN o ARN haciéndola pasar por un poro proteico de escala nanométrica y registrando los **cambios en la corriente iónica** que produce a su paso.

Es la única de las plataformas comparadas en la clase que **no usa fluorescencia ni síntesis**: la señal es eléctrica y directa.

## El principio

Una membrana aislante separa dos compartimentos con electrolito (*cis* y *trans*). Se aplica una diferencia de potencial, y como la membrana no deja pasar iones libremente, la corriente circula **por el nanoporo**. Cuando una hebra de ácido nucleico ocupa el poro, obstruye parcialmente ese flujo, y la magnitud de la obstrucción depende de qué nucleótidos hay dentro de la región sensible.

> El detalle que lo condiciona todo: **no se lee una base por vez**, sino un [[K-mer|k-mer]] completo situado simultáneamente en la zona sensible. La corriente codifica un *contexto*, no un carácter.

La traza de corriente resultante se llama [[Squiggle|squiggle]], se almacena en formato [[POD5]] y se traduce a secuencia por [[Basecalling|basecalling]].

## Los tres componentes del sistema

| Componente | Función |
|---|---|
| **Membrana** | Aísla eléctricamente y fuerza a que la corriente pase por el poro. En las flow cells comerciales es **polimérica**, compatible con arrays, automatización, almacenamiento y transporte |
| **Nanoporo** | Deja pasar la molécula y genera la señal. El actual es una versión ingenierizada de **CsgG** (R10.4.1, con doble región sensible) |
| **Proteína motora** | Unida al adaptador de secuenciación; desenrolla el dúplex y **regula la velocidad de translocación** para que la señal sea muestreable. Hoy se usan helicasas/translocasas; históricamente, polimerasas (φ29) |

> La membrana aísla, el poro ayuda a pasar la molécula y generar la señal eléctrica, y la proteína motora regula el tiempo en que está en el poro.

## La evolución de los poros

| Poro | Aporte | Límite |
|---|---|---|
| **α-hemolisina** | Autoensamblaje estable, paso de ADN monocatenario, cambios detectables de corriente | Canal largo: demasiadas bases influyen a la vez |
| **MspA** | Constricción muy corta y estrecha, alta densidad de corriente concentrada | — |
| **CsgG** | Constricción estrecha, apertura vestibular amplia, **ingenierizable por mutagénesis**, buena interacción con el complejo ADN–motora | — |

El poro **R10.4.1** (CsgG–CsgF) tiene **dos regiones sensibles** en lugar de una, lo que mejora la resolución especialmente en [[Homopolímeros|homopolímeros]]. Con la química R10.4.1 + V14, ONT reporta **Q20+ en simplex y Q30+ en [[Secuenciación dúplex|dúplex]]**.

## Qué la distingue

| Propiedad | Consecuencia |
|---|---|
| Lecturas **largas** (de 20 pb a >4 Mb) | Resuelve [[Plásmido\|plásmidos]], elementos móviles, repeticiones y [[Variantes estructurales\|variantes estructurales]] |
| Lee **ADN nativo** | La [[Metilación del ADN\|metilación]] viene incluida, sin bisulfito ni ensayo aparte |
| Señal **guardada** ([[POD5]]) | Se puede **rebasecallear** años después con modelos mejores |
| **[[Secuenciación en tiempo real\|Tiempo real]]** | Datos analizables mientras la corrida ocurre |
| Equipos portátiles (130 g) | [[Vigilancia genómica hospitalaria\|Vigilancia descentralizada]] |
| [[Perfil de error]] propio | Indels en homopolímeros; exactitud simplex por debajo de [[Illumina]] y [[PacBio]] |

## Historia

Nace del cuaderno de [[David Deamer]] del **25 de junio de 1989**, y de la convergencia de seis líneas de trabajo (translocación, motores, poros proteicos, reconocimiento de nucleótidos, control del movimiento, traducción tecnológica). Ver la línea de tiempo 1995–2015 en la clase.

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
