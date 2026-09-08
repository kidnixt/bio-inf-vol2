---
tags: [biología, microbiología, genómica]
area: Biología
aliases: [plásmidos, elementos móviles, mobile genetic elements, pQEB1]
---

# Plásmido

Molécula de ADN —típicamente circular— que se replica de forma independiente del cromosoma bacteriano y puede transferirse entre células, incluso **entre especies distintas**.

Junto con transposones, integrones y profagos forma el conjunto de **elementos genéticos móviles**, el vehículo principal de la diseminación de [[Resistencia antimicrobiana|genes de resistencia]].

## Por qué son un problema bioinformático

Un plásmido está lleno de secuencias repetidas, insertadas y compartidas con otros plásmidos y con el cromosoma. Con [[Secuenciación de segunda generación|lecturas cortas]] esas repeticiones fragmentan el [[Ensamblaje de novo|ensamblado]]: se sabe que el gen de resistencia está en la muestra, pero no si está en el cromosoma o en un plásmido, ni cómo es ese plásmido.

Con [[Secuenciación de tercera generación|lecturas largas]] el plásmido se **cierra en una sola pieza**, y entonces se puede responder la pregunta epidemiológica real:

> ¿Es el mismo plásmido el que está en el paciente A, en el paciente B y en el lavatorio de la sala?

## En los casos de la clase

- **pQEB1 / KPC-2 (2024)**: transmisión de plásmidos de resistencia **entre especies**, con resolución de los elementos móviles implicados.
- **Sauerborn et al. (2026)**: persistencia y reservorios de resistencia entre pacientes y ambiente.

Por eso "reconstrucción de plásmidos/AMR" figura entre las cuatro cosas que aporta ONT en [[Vigilancia genómica hospitalaria|vigilancia hospitalaria]].

## Y en metagenómica

Asignar un plásmido a su bacteria hospedadora dentro de una comunidad es difícil: su composición de bases suele diferir de la del cromosoma. Una de las soluciones que habilita ONT es usar la firma de [[Metilación del ADN|metilación]] como huella para vincularlos ([[Nanodisco]]).

## Aparece en

- [[Aplicaciones de la secuenciación con nanoporos en (meta)genómica]]
