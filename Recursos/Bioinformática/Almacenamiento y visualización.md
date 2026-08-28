---
tags: [concepto, bioinformática, espacial, desafío]
area: Bioinformática
aliases: [storage and visualization, almacenamiento, visualización]
---

# Almacenamiento y visualización

> **Storage and visualization!**

Uno de los desafíos que la clase de [[Biología espacial - mapeando la expresión génica a su entorno|biología espacial]] plantea con signo de exclamación, y que suele subestimarse por parecer "sólo un problema de ingeniería".

## Por qué explota el volumen

Un experimento espacial no es una [[Matriz de conteo]]: es una matriz **más** un conjunto de imágenes de alta resolución **más** una tabla de coordenadas, todo alineado entre sí.

- Un corte de [[CosMx SMI]] genera cientos de imágenes por ronda de hibridación, por múltiples rondas, en múltiples canales, en varios planos Z.
- [[Visium HD]] genera bins de 2 µm sobre centímetros cuadrados de tejido: cientos de miles a millones de observaciones por corte.
- Los [[Atlas celulares]] espaciales multiplican esto por cientos o miles de cortes.

Se pasa de gigabytes a **terabytes por experimento**.

## Por qué la visualización es un problema en sí

No alcanza con generar una figura: el análisis espacial es **exploratorio y visual**. Hay que poder navegar el tejido, hacer zoom desde el órgano hasta la célula, superponer expresión génica sobre histología, y hacerlo de forma interactiva. Eso exige infraestructura tipo mapa web (formatos piramidales, teselado, carga por niveles) más que herramientas estadísticas.

## El punto de fondo

Es la mitad concreta del diagnóstico con el que cierra la clase:

```
datos  ────────────────────────►  conocimiento
        almacenamiento
        visualización
        integración
```

Conecta directamente con el [[Módulo 4 - MOC|Módulo 4: Desarrollo y despliegue]].

## Aparece en

- [[Biología espacial - mapeando la expresión génica a su entorno]]
