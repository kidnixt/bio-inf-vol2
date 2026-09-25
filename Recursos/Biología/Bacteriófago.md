---
tags: [concepto, biología, virus, microbiología]
area: Biología
aliases: [bacteriófagos, fago, fagos, phage, phages]
---

# Bacteriófago

Virus que infecta bacterias. Son **los virus más abundantes del planeta** — y, para la bioinformática, **los más difíciles de anotar**.

## El problema de anotación

Evolucionan tan rápido que **más del 65 % de sus proteínas no se pueden anotar por [[Homología|homología]] de secuencia**: no hay con qué compararlas. Los métodos estándar de anotación funcional —búsqueda por secuencia (MMseqs2), perfiles HMM (PyHMMER)— se quedan en torno al 35 %.

Es el escenario donde la bioinformática clásica **toca fondo**: sin homólogos no hay [[Alineamiento múltiple de secuencias|MSA]], sin MSA no hay perfil, sin perfil no hay anotación.

## Por qué aparece en la clase

Porque es el caso de uso de [[Phold]], el trabajo que combina [[ProstT5]] y [[Foldseek]] para anotar **por forma** en vez de por secuencia:

| Método | % anotado (sobre 16.460 CDS de fagos) |
|---|---|
| MMseqs2 (secuencia) | 34,7 % |
| PyHMMER (perfil HMM) | 37,7 % |
| **Phold** (estructura) | **49,4 %** |

> **La forma conserva señal que la secuencia ya perdió.**

Los fagos con más ganancia de anotación son justamente los de **metabolismo de ácidos nucleicos y funciones enzimáticas** — dominios estructuralmente conservados cuya secuencia divergió más allá de lo detectable.

Conecta además con el [[Módulo 1 - MOC|Módulo 1]]: los fagos son parte del universo microbiano que la [[Metagenómica clínica|metagenómica]] muestrea y que la [[Secuenciación con nanoporos|secuenciación]] hace accesible — pero que hasta ahora quedaba en gran parte sin interpretar.

## Aparece en

- [[Modelos de lenguaje de proteínas y embeddings proteicos]]
- [[Bouras et al 2026 - Phold]] *(lectura)*
