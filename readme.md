# Ejercicio 03: Modelo Vectorial TF-IDF

## Descripción

Este proyecto corresponde a la resolución del Ejercicio 03 de Recuperación de Información, enfocado en el Modelo Vectorial utilizando TF-IDF (Term Frequency - Inverse Document Frequency).

El objetivo es implementar un sistema de recuperación de información que permita encontrar documentos relevantes a partir de una consulta, utilizando dos corpus:

- **Corpus de turismo**: 500 documentos en español sobre turismo en Ecuador
- **Corpus Gutenberg**: 1000 libros en inglés del Proyecto Gutenberg

---

## Modelo Implementado: TF-IDF

TF-IDF representa documentos como vectores numéricos donde cada término tiene un peso basado en:

- **TF (Term Frequency):** cuántas veces aparece un término en un documento
- **IDF (Inverse Document Frequency):** qué tan raro o común es ese término en todo el corpus

### Fórmula

```
TF-IDF(t, d) = TF(t, d) × IDF(t)
IDF(t) = log(N / df(t))
```

Donde `N` es el número total de documentos y `df(t)` es el número de documentos que contienen el término `t`.

---

## Preprocesamiento

Se aplicó el siguiente pipeline a ambos corpus:

1. Conversión a minúsculas
2. Eliminación de caracteres especiales
3. Tokenización por espacios
4. Eliminación de stopwords (español para turismo, inglés para Gutenberg)

---

## Estructura del Proyecto

```
recuperacion-informacion/
├── ejercicio-03-tfidf.ipynb   # Notebook principal del ejercicio
├── ejercicio-04-bm25.ipynb    # Notebook con resolución completa
└── README.md
```

---

## Dataset

Los datos utilizados corresponden a:

- `01_corpus_turismo_500.txt`: 500 frases sobre turismo en Ecuador
- `corpus_limpio.zip`: 1000 libros del Proyecto Gutenberg (en inglés)

Acceso al dataset:
https://drive.google.com/drive/folders/133fRRkPFZzhFhSp52m2ijQ5GOO3S-tzx

---

## Requisitos

```bash
pip install pandas scikit-learn nltk
```

---

## Ejecución

1. Montar Google Drive con los datasets en la ruta `/content/drive/MyDrive/data/`
2. Abrir el notebook en Google Colab
3. Ejecutar las celdas en orden

---

## Resultados

### Corpus Turismo (español)
- Matriz TF-IDF: **500 documentos × 95 términos**
- Se eliminaron stopwords en español con NLTK

### Corpus Gutenberg (inglés)
- Matriz TF-IDF: **1000 documentos × 5000 términos**
- Se limitó a `max_features=5000` para eficiencia

### Función `buscar()`

Permite ingresar una consulta en lenguaje natural y retorna los documentos más relevantes ordenados por score TF-IDF:

```python
buscar("war politics revolution", top_n=5)
```

| Documento  | Score TF-IDF |
|------------|-------------|
| 1804.txt   | 0.414321    |
| 1946.txt   | 0.344842    |
| 1946-8.txt | 0.344840    |
| 1864.txt   | 0.235072    |
| 1484.txt   | 0.207470    |

---

## Conclusión

TF-IDF es un modelo vectorial efectivo para recuperación de información. La ponderación por frecuencia inversa permite destacar términos discriminativos, logrando rankings relevantes tanto en corpus pequeños (turismo) como en colecciones grandes (Gutenberg).

---

## Autor

**Lenin Reyes**
Escuela Politécnica Nacional
lenin.reyes@epn.edu.ec
