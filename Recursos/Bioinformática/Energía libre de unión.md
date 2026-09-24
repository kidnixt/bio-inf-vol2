---
tags: [concepto, bioinformática, física, fármacos]
area: Bioinformática
aliases: [ΔG, delta G, afinidad, Kd, energía libre, FEP, MM-GBSA]
---

# Energía libre de unión

La magnitud termodinámica que describe **cuán fuerte** se une un ligando a su blanco.

```
Afinidad  ←→  ΔG°  ←→  Kd
más favorable        menor Kd
```

> **La relación termodinámica es exacta. La estimación computacional conserva incertidumbre.**

Esa frase de la clase es la distinción clave: ΔG° y Kd están relacionados por una ecuación (ΔG° = −RT ln K), no por una aproximación. Lo incierto es **calcular** ΔG, no la relación.

## Por qué es difícil

Predecir *dónde* y *cómo* se une una molécula es un problema geométrico, y ahí los métodos modernos ([[Docking molecular|docking]], [[AlphaFold|AlphaFold3]], [[Cofolding|cofolding]]) andan bien. Predecir *cuán fuerte* requiere contabilizar entropía, desolvatación y la flexibilidad de ambos socios — y ahí siguen fallando.

De hecho, "**la afinidad todavía es difícil**" es una de las tres precauciones que la propia clase le pone a AlphaFold3.

Hay una razón estructural: los datos. Hay ~5·10¹⁰ moléculas enumerables en [[ZINC]], ~3·10⁶ compuestos con actividad medida en [[ChEMBL]], y solo **2,9·10⁴ complejos con estructura y afinidad** en [[PDBbind]]. Es el conjunto de entrenamiento más chico para el problema más difícil.

## No confundir con el score

Una [[Función de puntuación|función de puntuación]] de docking devuelve un número que **ordena hipótesis dentro de un protocolo**. **No equivale automáticamente a ΔG experimental**, aunque sus unidades a veces lo sugieran (kcal/mol).

Los métodos que sí apuntan a ΔG —perturbación de energía libre (FEP), MM-GBSA, integración termodinámica— se construyen sobre trayectorias de [[Dinámica molecular|MD]] y son órdenes de magnitud más caros. En el trabajo de [[Andrés Ballesteros]] sobre búsqueda inversa de blancos, los valores de **MM-GBSA** (−67,8 a −114,0 kcal/mol) acompañan a los de Glide_XP como un segundo criterio de ordenamiento.

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
