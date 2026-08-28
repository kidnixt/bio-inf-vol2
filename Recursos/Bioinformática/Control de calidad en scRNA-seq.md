---
tags: [concepto, bioinformática, single-cell]
area: Bioinformática
aliases: [QC, control de calidad, quality control]
---

# Control de calidad en scRNA-seq

El primer paso del análisis después de obtener la [[Matriz de conteo]]: decidir **qué columnas de la matriz corresponden a células reales y sanas**. La clase presenta las tres métricas canónicas, que se inspeccionan por célula.

## Las tres métricas

### 1. Número de [[UMI]] por célula

Cuántas moléculas distintas se detectaron.

| Valor | Interpretación probable |
|---|---|
| Muy bajo | Gota vacía o célula rota (sólo ARN ambiental) |
| Muy alto | **Doblete**: dos células en la misma gota |

### 2. Número de genes por célula

Complejidad de la librería. Correlaciona con el número de UMIs, pero no es redundante: una célula con muchos UMIs concentrados en pocos genes es sospechosa (por ejemplo, un eritrocito lleno de hemoglobina, o una célula estresada).

### 3. Fracción de [[Genes mitocondriales]]

Proxy de estrés y muerte celular. Cuando la membrana plasmática se compromete, el ARN citoplasmático se escapa y los transcriptos mitocondriales —protegidos dentro de la mitocondria— quedan sobrerrepresentados.

## Cómo se usan

Se grafican como distribuciones (violin plots) y se fijan umbrales. La advertencia importante: **los umbrales no son universales**. Dependen del tejido, del protocolo y de la [[Profundidad de secuenciación]]. Un umbral de 5% de genes mitocondriales es razonable en muchos tejidos y desastroso en cardiomiocitos, que son legítimamente ricos en mitocondrias.

Filtrar de más elimina tipos celulares reales (las [[Neurona|neuronas]] frágiles, por ejemplo); filtrar de menos deja dobletes y basura que después aparecen como "clusters" espurios en el [[Clustering]].

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
