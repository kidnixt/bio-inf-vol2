---
tags: [concepto, técnica, ingeniería-metabólica]
area: Técnicas
aliases: [co-consumo, co-consumption, co-utilización, co-utilization, balance score, consumo simultáneo de azúcares]
---

# Co-consumo de azúcares

Que un microorganismo consuma **varios azúcares a la vez** en lugar de uno después del otro. Es el objetivo del caso de estudio de la clase.

## El problema

Los azúcares derivados de biomasa vegetal vienen como mezcla de glucosa y [[Pentosas|pentosas]] (xilosa, arabinosa). Pero *[[Saccharomyces cerevisiae|S. cerevisiae]]*:

- consume **glucosa preferentemente**;
- consume pentosas **lento, ineficientemente o directamente no**.

El resultado es consumo secuencial: primero la glucosa, y recién después (mal y lento) el resto.

## Habilitar ≠ forzar

> **Enabling co-consumption is not enforcing co-consumption.**

Las estrategias clásicas — [[Vías de asimilación de pentosas|vías heterólogas]], ingeniería de transportadores, [[Evolución adaptativa de laboratorio|ALE]] — hacen que la levadura **pueda** consumir pentosas. Pero mientras exista una distribución de flujos donde crecer solo con glucosa sea posible, la célula la va a tomar.

De ahí la reformulación de la clase:

> **¿Y si hacemos que el co-consumo sea *requisito* para crecer?**

Se traduce a [[Minimal Cut Sets|módulos PROTECT/SUPPRESS]]: suprimir toda distribución de flujos donde el crecimiento se sostenga con uno o dos azúcares (o con captación marginal de alguno), y proteger al menos una donde se consuman los tres.

## Balance score

La métrica con la que se rankean los diseños:

> **Balance score = la menor contribución de un azúcar, considerando todos los azúcares y todos los órdenes de minimización de captación.**

Un diseño puede cumplir formalmente el co-consumo pero con un azúcar aportando casi nada; el balance score penaliza eso. En el caso de estudio, 332 de 729 diseños aeróbicos superan el 5 %, y **ningún diseño anaeróbico lo logra** (máximo ~3,5 %): un desafío de relevancia industrial.

## Cómo se logra en el diseño seleccionado

Haciendo que cada azúcar aporte algo insustituible a la [[Reacción de biomasa|biomasa]]: glucanos de pared (glucosa), nucleótidos y aminoácidos aromáticos (arabinosa), precursores derivados de α-cetoglutarato y [[Cofactores energéticos|energía]] (xilosa).

> **Los tres azúcares se vuelven complementarios.**

## Aparece en

- [[Intro teórica a modelos metabólicos y aplicaciones en ingeniería metabólica]]
