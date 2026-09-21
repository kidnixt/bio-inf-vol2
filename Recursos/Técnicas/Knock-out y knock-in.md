---
tags: [concepto, técnica, ingeniería-metabólica]
area: Técnicas
aliases: [KO, KI, knock-out, knock-in, gene KO, gene KI, knockout, knockin]
---

# Knock-out y knock-in

Los dos tipos de intervención genética que maneja el [[Diseño computacional de cepas]].

| Intervención | Qué se hace | Efecto en el modelo | Efecto en la red |
|---|---|---|---|
| **Knock-in (KI)** | Introducir uno o más genes, normalmente heterólogos (de otro organismo) | **Agrega** reacción(es) a la [[Matriz estequiométrica]] | Añade funciones nuevas |
| **Knock-out (KO)** | Inactivar o eliminar un gen nativo | **Elimina** reacción(es): se fija su flujo en 0 (`l = u = 0`) | Remueve funciones nativas |

Geométricamente, un KI **expande** el [[Espacio de flujos factible]] (aparecen distribuciones antes imposibles) y un KO lo **recorta**.

## En el caso de estudio

- **Candidatos KI:** 13 reacciones heterólogas de metabolismo de xilosa y arabinosa ([[Vías de asimilación de pentosas]]).
- **Candidatos KO:** todos los genes nativos del modelo [[Yeast9]].
- **Diseño seleccionado:** 8 KI (ARAI, RBK_L1, RBP4E, XYLOR, XYLLN, DXYLTD, 2D3DDAD, 2OGSAD) + 6 KO (PGL, PGI, PGK, TPI, XYLTD_D, FDH).

## Un matiz importante

Un KO no es "apagar una vía": es apagar **una reacción**, y la célula puede tener rutas alternativas para el mismo objetivo. Buena parte del trabajo de [[Minimal Cut Sets|los algoritmos de cut sets]] consiste justamente en encontrar el conjunto de KO que cierra **todas** las alternativas a la vez. Por eso aparecen KO cuyo efecto no es obvio mirando el mapa de vías.

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
