---
tags: [herramienta, base-de-datos, quimioinformática]
area: Herramientas
aliases: [ZINC-22, ZINC15, base ZINC]
---

# ZINC

Biblioteca química de moléculas **comercialmente disponibles**, mantenida en la UCSF por los grupos de **John Irwin** y **Brian Shoichet**. Es la fuente estándar de compuestos para [[Virtual screening|cribado virtual]].

| | |
|---|---|
| Tipo de registro | Moléculas 2D enumeradas |
| Tamaño (corte 09/09/2026) | **≈ 54.900 millones** (ZINC-22) |
| Qué ofrece | Estructuras 2D/3D, propiedades y referencias a proveedores |
| Consulta típica | *¿Qué moléculas puedo comprar o encargar para evaluar este sitio?* |

## Por qué es tan grande

ZINC no es un depósito de frascos: la mayor parte de su contenido son moléculas **de síntesis bajo pedido** (*make-on-demand*), enumeradas combinatoriamente a partir de reacciones robustas y bloques de construcción disponibles. Por eso el tamaño creció de ~10⁷ (ZINC15) a ~5·10¹⁰ (ZINC-22) en pocos años, mientras las bases con actividad medida ([[ChEMBL]], [[BindingDB]]) siguen en el orden de 10⁶.

> [!warning] La advertencia de la clase
> **Un catálogo de síntesis bajo pedido no equivale a un inventario físico ni a actividad demostrada.** Que una molécula esté en ZINC significa que probablemente se pueda encargar, no que exista ni que sirva.

## Dónde entra en el flujo

Es la **boca del embudo** del [[Virtual screening|VS jerárquico]]: los 10⁸–10¹⁰ compuestos del primer nivel salen típicamente de ZINC. Los casos de cribado ultragrande de la clase —[[Casos de éxito del diseño computacional de fármacos|DRD4 con 138 millones de moléculas]], la [[Casos de éxito del diseño computacional de fármacos|halicina con >107 millones]], V-SYNTHES2 representando 36 mil millones— trabajan todos sobre ZINC o sobre espacios enumerables equivalentes (REAL Space de Enamine).

Ver también [[PubChem]] (la otra gran biblioteca química, orientada a identidad y bioactividad más que a compra).

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
