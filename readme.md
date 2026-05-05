# Recuperación de Información: Ejercicios 03 y 04

## Descripción

Este repositorio contiene la resolución de los ejercicios 03 y 04 de la materia de Recuperación de Información, implementando y comparando dos modelos fundamentales: **TF-IDF** (Modelo Vectorial) y **BM25** (Modelo Probabilístico).

El corpus utilizado corresponde a **1000 libros del Proyecto Gutenberg** en inglés.

---

## Ejercicio 03: Modelo Vectorial TF-IDF

### Objetivo
Implementar un sistema de recuperación de información usando TF-IDF y similitud coseno.

### Modelo: TF-IDF

TF-IDF representa documentos como vectores numéricos donde cada término tiene un peso basado en:

- **TF (Term Frequency):** cuántas veces aparece un término en un documento
- **IDF (Inverse Document Frequency):** qué tan raro o común es ese término en todo el corpus

```
TF-IDF(t, d) = TF(t, d) × IDF(t)
IDF(t) = log(N / df(t))
```

### Resultados

| Consulta | Documento | Score TF-IDF |
|----------|-----------|-------------|
| war politics revolution | 1804.txt | 0.414321 |
| war politics revolution | 1946.txt | 0.344842 |
| war politics revolution | 1946-8.txt | 0.344840 |

---

## Ejercicio 04: Modelo Probabilístico BM25

### Objetivo
Comparar TF-IDF con BM25, analizando diferencias en los rankings y visualizando resultados.

### Partes

| Parte | Descripción |
|-------|-------------|
| **Parte 0** | Carga del corpus Gutenberg 1000 desde Google Drive |
| **Parte 1** | Cálculo de TF, DF, IDF y matriz TF-IDF con sklearn |
| **Parte 2** | Ranking de documentos usando similitud coseno TF-IDF |
| **Parte 3** | Implementación de BM25 desde cero (k1, b, IDF probabilístico) |
| **Parte 4** | Comparación visual TF-IDF vs BM25 con gráfico de barras |

### Modelo: BM25

BM25 mejora TF-IDF introduciendo:

- **Saturación de términos:** evita que palabras muy frecuentes dominen el score
- **Normalización por longitud:** penaliza documentos muy largos
- **Parámetros ajustables:** `k1` (saturación) y `b` (normalización de longitud)

```
BM25(t, d) = IDF(t) × [TF(t,d) × (k1+1)] / [TF(t,d) + k1 × (1 - b + b × |d|/avgdl)]
```

---

## Estructura del Proyecto

```
recuperacion-informacion/
├── ejercicio-03-tfidf.ipynb   # Modelo Vectorial TF-IDF
├── ejercicio-04-bm25.ipynb    # Modelo Probabilístico BM25
└── README.md
```

---

## Dataset

- **Corpus Gutenberg**: 1000 libros en inglés del Proyecto Gutenberg

Acceso al dataset:
https://drive.google.com/drive/folders/133fRRkPFZzhFhSp52m2ijQ5GOO3S-tzx

---

## Requisitos

```bash
pip install pandas scikit-learn matplotlib numpy nltk
```

---

## Ejecución

1. Montar Google Drive con los datasets en `/content/drive/MyDrive/data/`
2. Abrir el notebook en Google Colab
3. Ejecutar las celdas en orden

---

## Conclusión

- **TF-IDF** es un modelo vectorial simple y efectivo, pero puede sobrevalorar términos frecuentes en documentos largos.
- **BM25** corrige esto con saturación de términos y normalización por longitud, obteniendo rankings más equilibrados y precisos en colecciones grandes.

---

## Autor

**Lenin Reyes**
Escuela Politécnica Nacional
lenin.reyes@epn.edu.ec
