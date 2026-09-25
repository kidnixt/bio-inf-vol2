---
tags: [lectura, modulo-3, fármacos, cribado-virtual]
area: Lecturas
tipo: research article
autores: Antonina L. Nazarova, Anastasiia V. Sadybekov, Arman A. Sadybekov, Mykola Protopopov, Dmytro S. Radchenko, Yurii S. Moroz, Olga O. Tarkhanova, Vsevolod Katritch
año: 2026
revista: npj Drug Discovery 3, 21
doi: 10.1038/s44386-026-00053-6
aliases: [Nazarova 2026, V-SYNTHES2, V-SYNTHES, CapSelect, "V-SYNTHES2 - the next generation tool for structure-based virtual screening of giga-scale chemical spaces"]
---

# Nazarova et al. (2026) — *V-SYNTHES2: the next generation tool for structure-based virtual screening of giga-scale chemical spaces*

> [!info] Ficha de la lectura
> **Tipo:** research article — *npj Drug Discovery* (acceso abierto)
> **Autores:** University of Southern California, con Chemspace y Enamine (Kyiv)
> **Clase asociada:** [[Métodos para el diseño computacional de fármacos]] (clase 6)
> **PDF:** [[Nazarova et al 2026 - V-SYNTHES2.pdf]]

## En una frase

Cómo cribar un espacio químico de **36 mil millones** de compuestos dockeando solo **3,8 millones**: enumeración jerárquica por síntones en vez de enumerar todo.

## Por qué leerla después de la clase

La clase lo muestra como una diapositiva de números (3,8 M de dockings para representar 36 mil millones). El paper explica **la decisión de diseño que lo hace distinto** de los otros métodos de aceleración — y esa decisión es exactamente el tema que atraviesa el módulo: **qué función de puntuación se usa, y sobre qué**.

---

## 1. El cuello de botella

Los espacios *on-demand* como el **REAL Space** de Enamine crecieron a decenas de miles de millones de compuestos sintetizables (80 % de éxito de síntesis en 4 semanas). El costo de cribarlos se volvió **el** cuello de botella del descubrimiento de hits.

Las estrategias existentes —docking en GPU, embudos de rápido a refinado, iteraciones con deep learning— comparten un supuesto: **enumerar el espacio**, al menos como SMILES.

## 2. La crítica metodológica (lo más interesante del paper)

> Las estrategias basadas en embudos y en *active learning* usan **modelos sustitutos** para evaluar todo el espacio, y aplican la [[Función de puntuación|función de puntuación]] basada en física solo a un subconjunto chico seleccionado en etapas tempranas.

El problema: cuando el espacio llega a decenas de miles de millones, **una divergencia modesta entre el sustituto y el objetivo físico puede excluir sistemáticamente ligandos de alto score o quimiotipos subrepresentados** antes de que sean evaluados con el método fiel.

V-SYNTHES2, en cambio, **conserva el docking basado en física como criterio primario en toda la jerarquía**, y reduce el espacio por **descomposición química** en vez de filtrado por sustituto.

> [!note] El eco con la clase y con el resto del vault
> Es la regla 2 de la clase 6 —*"el score ordena hipótesis dentro de un protocolo"*— llevada a su consecuencia operativa: si cambiás de score a mitad del embudo, **cambiaste de protocolo**, y lo que descartaste con el score barato ya no es recuperable. El mismo problema aparece en el capítulo 1 de la tesis de Johny, del lado de las proteínas: **el filtro mueve el ranking más que el modelo**.

## 3. Cómo funciona

1. Generar una **MEL** (*Minimal Enumeration Library*): fragmentos que representan todas las combinaciones síntón-scaffold, con los otros puntos de unión "tapados" con metilo o fenilo. Son **1,7 M** de fragmentos para reacciones de 2 componentes y **140 K** para las de 3.
2. Dockear la MEL y seleccionar los fragmentos top **y productivos**.
3. Enumerar síntones en el siguiente punto de unión.
4. Re-dockear. Para reacciones de 3 componentes, repetir.

**CapSelect** es la novedad: automatiza el paso 2b evaluando la **geometría** de la pose — si el grupo tapado queda con espacio para crecer (productivo) o contra una pared del bolsillo (no productivo). En la versión anterior esto requería que el usuario definiera residuos de contacto indeseados, o sea **conocimiento experto del blanco**. Procesa 30.000 fragmentos en 10–20 min.

## 4. Los números

| | |
|---|---|
| Espacio representado | **36 mil millones** (164 reacciones, 112.514 reactivos) |
| Dockings efectivos | ~3,8 M (2 M enumerados + 1,8 M de MEL) |
| Reducción | **> 10.000×** |
| Reproducibilidad de poses | **> 90 %** para los 100 K mejores |
| Tiempo típico | ~48 h con 320 núcleos CPU |
| Costo estimado | ~**US$ 380** contra ~**US$ 3,6 M** y ~130 años de reloj del docking directo |

Validado en blancos difíciles —bolsillos poco profundos, sitios de unión a ARN, GPCRs, enzimas que unen fosfolípidos— y prospectivamente en dos blancos nuevos (cPLA2 y el receptor de angiotensina AT2), con validación experimental en estudios acompañantes.

## 5. Qué aporta respecto de la clase

- **El argumento contra los modelos sustitutos**, que es una crítica a la estrategia dominante y no aparece en la diapositiva.
- **El costo en dólares y en años de reloj**, que vuelve tangible la escala del [[Virtual screening|embudo jerárquico]].
- **CapSelect como ejemplo de automatizar juicio experto**: pasar de "el usuario define qué contactos no quiere" a un criterio geométrico general.

## Conceptos del vault

[[Virtual screening]] · [[Docking molecular]] · [[Función de puntuación]] · [[Diseño basado en estructura]] · [[ZINC]] · [[Aprendizaje activo]] · [[Diseño de fármacos asistido por computadora]] · [[ADMET]]

## Aparece en

- [[Métodos para el diseño computacional de fármacos]]
- [[Módulo 3 - MOC]]
