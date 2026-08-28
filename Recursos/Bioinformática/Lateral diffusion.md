---
tags: [concepto, bioinformática, espacial, artefacto]
area: Bioinformática
aliases: [difusión lateral]
---

# Lateral diffusion (difusión lateral)

Artefacto característico de los [[Métodos basados en secuenciación]] que capturan ARN sobre oligos en superficie, como [[Visium HD]].

## Qué ocurre

Para que el ARN llegue a los oligos de captura hay que **permeabilizar** el tejido. Durante ese proceso, las moléculas no bajan sólo verticalmente: también difunden **lateralmente** antes de anclarse.

```
posición real del ARN            posición registrada
        ●          ──difusión──►        ◌ ◌ ●  ◌
```

El [[Barcode espacial]] registra fielmente dónde se **capturó** la molécula, que no es necesariamente dónde **estaba**.

## Consecuencias

- La señal se "corre" respecto de su origen real.
- Se **difuminan los bordes** entre estructuras: en el límite entre dos regiones con perfiles distintos aparece una franja de perfil intermedio que no corresponde a ninguna población real.
- Limita la resolución efectiva: no sirve de nada tener bins de 2 µm si el ARN difundió 10 µm.
- Puede simular expresión de un [[Tipo celular]] en células vecinas, generando falsa evidencia de [[Neighborhoods]].

## El compromiso

Permeabilizar poco reduce la difusión pero también la sensibilidad; permeabilizar mucho mejora la captura y empeora la resolución. El tiempo de permeabilización se optimiza para cada tipo de tejido.

Es el problema análogo, en la familia de captura, al [[Optical crowding]] de la familia de imagen.

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
