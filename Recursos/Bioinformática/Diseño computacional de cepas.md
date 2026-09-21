---
tags: [concepto, bioinformática, ingeniería-metabólica]
area: Bioinformática
aliases: [computational strain design, strain design, diseño de cepas]
---

# Diseño computacional de cepas

> **Computational strain design searches for genetic interventions that change which phenotypes are possible.**

Buscar con un algoritmo, sobre un [[Modelo metabólico a escala genómica]], las intervenciones genéticas que **remodelan el [[Espacio de flujos factible]]** para que el fenotipo deseado quede posible y los indeseados queden imposibles.

## Las intervenciones

Ver [[Knock-out y knock-in]].

| Intervención | En el modelo | En la red |
|---|---|---|
| **Gene KI** | Agrega reacción(es) | Suma funciones nuevas |
| **Gene KO** | Elimina reacción(es) | Quita funciones nativas |

## Por qué no alcanza con FBA

[[Flux Balance Analysis|FBA]] predice el comportamiento de una cepa dada. El diseño de cepas invierte la pregunta: dado el comportamiento que quiero, ¿qué cepa lo garantiza? Y "garantizar" es clave: no basta con que el fenotipo sea **posible** (eso es *habilitar*), tiene que ser **el único** posible (eso es *forzar*). En el caso de la clase: *enabling co-consumption is not enforcing co-consumption*.

## Frente a la ingeniería metabólica clásica

| Clásica | Computacional |
|---|---|
| Un gen, una enzima, una vía | Toda la red a la vez |
| Blancos elegidos por inspección de mapas | Blancos elegidos por un algoritmo |
| Puede pasar por alto efectos lejanos | Encuentra blancos no obvios |

En el caso de estudio, el método **redescubrió** la lógica PGI/RPE de Papapetridis et al. (2018) y además propuso KO que, según la clase, *"por análisis humano de los mapas de vías serían muy probablemente imposibles de encontrar"*.

## Herramientas

- [[StrainDesign]] (Schneider et al., 2022), basado en [[Minimal Cut Sets]].
- [[PECA]], una interfaz para que ingenieros experimentales puedan usarlo.

> **Flexible but underused framework.**

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
- [[Schneider et al 2022 - StrainDesign]] *(lectura)*
