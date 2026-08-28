---
tags: [técnica, single-cell, proteómica]
area: Técnicas
aliases: [single cell proteomics, scProteomics, proteómica single-cell]
---

# Proteómica de célula única

Medición de las **proteínas** presentes en células individuales — el producto final del [[Dogma central de la biología molecular]] y, en última instancia, el que ejecuta la función celular.

## Los tres desafíos que destaca la clase

### 1. No podemos amplificar

No existe una PCR para proteínas. En [[scRNA-seq]] el problema de tener poco material se resuelve amplificando el ADNc (y corrigiendo el sesgo con [[UMI]]). En proteómica, lo que hay es lo que hay: unos pocos cientos de miles a millones de copias de las proteínas abundantes, y unas decenas de las raras.

### 2. Rango dinámico muy amplio

Aún más extremo que en ARN — ver [[Rango dinámico]]. Las proteínas más abundantes pueden superar a las menos abundantes por 7 órdenes de magnitud, y dominan por completo la señal del espectrómetro de masas.

### 3. Adsorción en superficies

Con volúmenes de nanolitros y cantidades de femtomoles, una fracción significativa del material **se pega a las paredes** del tubo, la punta de pipeta o el capilar, y nunca llega al detector. Esto obliga a miniaturizar todo el flujo de trabajo y a usar superficies de bajo binding.

## Estado del campo

Es la ómica single-cell menos madura de las cuatro. Su integración con [[scRNA-seq]] y [[scATAC-seq]] es uno de los objetivos de la [[Integración de datos multiómicos]].

## Aparece en

- [[Aproximaciones ómicas con resolución de célula única]]
