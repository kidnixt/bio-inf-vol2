---
tags: [bioinformática, metagenómica, microbiología]
area: Bioinformática
aliases: [asignación taxonómica, taxonomic classification, LCA, Centrifuge, Kraken2, MEGAN6, SILVA]
---

# Clasificación taxonómica

Asignar cada lectura (o cada contig) al organismo del que proviene. Es el paso central de la [[Metagenómica clínica|metagenómica]] y de la [[Secuenciación 16S|secuenciación 16S]], y el que convierte secuencias en una respuesta biológica.

## Dos estrategias

| Estrategia | Cómo funciona | Ejemplos en la clase |
|---|---|---|
| **Por [[K-mer\|k-mers]]** | Compara los k-mers de la lectura contra un índice precomputado de genomas de referencia. Muy rápido | **Centrifuge** (flujo de metagenómica clínica), Kraken |
| **Por alineamiento + LCA** | Alinea la lectura contra una base de referencia y asigna el **ancestro común más bajo** compatible con todos sus buenos alineamientos | **Minimap2 + MEGAN6 LCA** contra **SILVA**, en [[Porefile]] |

La lógica del **LCA** (*lowest common ancestor*) es una forma explícita de honestidad: si una lectura es igualmente compatible con tres especies del mismo género, se la asigna al **género**, no a una especie elegida arbitrariamente. La resolución del resultado refleja la resolución real del dato.

## Lo que depende de la base de datos

La clasificación es tan buena como la referencia: no se puede identificar lo que no está en la base. De ahí que la clase liste, entre los requisitos para la aplicación clínica, **"bases de datos curadas y actualizadas"** — y que el flujo del NHS use *"Centrifuge + base curada"*, no una base genérica.

En [[Uso clínico y marco regulatorio|contexto clínico]] esto se combina con **umbrales de reporte**: cuántas lecturas de un organismo hacen falta para informarlo. Ese umbral es una decisión clínica disfrazada de parámetro bioinformático.

## Su límite conceptual

> **detección ≠ infección**

Clasificar correctamente un microorganismo no dice si es la causa de la enfermedad, si estaba vivo, o si es contaminación. El estudio suizo de 16S encontró que el 23,8% de las muestras daban señal compatible con contaminación — clasificada correctamente, y clínicamente irrelevante.

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
