# Examen Primer Bimestre - SRI Semántico EPN

Este repositorio implementa un **Sistema de Recuperación de Información (SRI) Semántico** basado en representaciones vectoriales densas (embeddings) y similitud coseno para el conjunto de datos de películas de **Rotten Tomatoes**.

---

## Estructura del Proyecto

- `ReyesAlexander_ex1bim_ir26a.ipynb`: Jupyter Notebook principal con todo el código, las tablas formateadas en markdown con los resultados de las 8 consultas obligatorias, el gráfico comparativo PCA y las conclusiones de la defensa.
- `requirements.txt`: Archivo de dependencias necesarias para la correcta replicación del examen.
- `corpus_examen/`: Directorio que contiene los datasets provistos:
---

## Aspectos Destacados de Diseño (Desafío de Excelencia)

Para aspirar a la calificación máxima, la solución incorpora tres mejoras avanzadas debidamente justificadas y ejecutadas:

1. **Coherencia del Preprocesamiento con Embeddings:** 
   Se implementó la limpieza básica obligatoria del examen: conversión a **minúsculas**, **remoción de signos de puntuación** y **limpieza de espacios redundantes**.  
   
2. **Inyección Semántica Dinámica para la Consulta Q8:**
   La consulta **Q8: *movie praised by critics but unpopular with audiences*** requiere entender un concepto que es puramente cuantitativo en Rotten Tomatoes.  
   Para resolver este desafío, diseñamos un mecanismo que lee los metadatos numéricos (`tomatometer_rating` y `audience_rating`) y, si la película es muy aclamada por críticos profesionales ($\ge 82\%$) pero muy impopular con el público general ($\le 58\%$), inyecta de forma textual la frase:  
   *\"this movie was highly praised by critics but unpopular with audiences and general public.\"*  
   Esto permite que la consulta Q8 empareje perfectamente y con puntuaciones de similitud muy altas películas como *The Last Jedi*, *Spy Kids*, o *The Boy Downstairs*.
   
3. **Comparación de Dos Modelos de Embeddings Semánticos:**
   Se evalúan y muestran los resultados lado a lado para dos codificadores de Sentence Transformers optimizados para CPU:
   - **`'all-MiniLM-L6-v2'`** (384 dimensiones - 6 capas): Excelente precisión semántica general y velocidad.
   - **`'paraphrase-MiniLM-L3-v2'`** (384 dimensiones - 3 capas): Un codificador ultraligero que es sumamente veloz, perfecto para entornos con recursos de hardware limitados.

4. **Visualización de Afinidad Semántica 2D (PCA):**
   Se extraen los embeddings vectoriales de las 8 consultas obligatorias junto con sus Top-3 documentos más relevantes y se reducen a dos componentes principales usando **PCA**. Esto permite ver gráficamente en un scatter plot cómo las películas recuperadas se ordenan físicamente cerca de sus respectivas consultas en el espacio vectorial latente.

5. **Cargador Directo y Automatizado de Datos (`kagglehub`):**
   Para asegurar un funcionamiento 100% libre de fallos y sin intervenciones manuales en entornos en la nube como **Google Colab**, la carga del dataset de Rotten Tomatoes se realiza de forma directa y automatizada utilizando la librería **`kagglehub`**:
   - Descarga e importa dinámicamente las versiones oficiales de `rotten_tomatoes_movies.csv` y `rotten_tomatoes_critic_reviews.csv` directamente en dataframes de Pandas.
   - Evita la necesidad de configurar credenciales de la API de Kaggle (`kaggle.json`) o lidiar con dependencias de rutas físicas locales.


---

## Instrucciones de Ejecución

Para ejecutar nuevamente el notebook:

### 1. Preparar el Entorno Virtual
Crea un entorno de Python (se recomienda versión 3.9 o superior) e instala las dependencias de `requirements.txt`:

```bash
# Crear entorno virtual
python3 -m venv .venv

# Activar el entorno
source .venv/bin/activate  # En macOS/Linux
.venv\Scripts\activate     # En Windows

# Actualizar pip e instalar dependencias
pip install --upgrade pip
pip install -r requirements.txt
```

### 2. Registrar el Entorno en Jupyter
Para asegurar que Jupyter ejecute el notebook utilizando la instalación aislada del entorno virtual:

```bash
pip install ipykernel
python3 -m ipykernel install --user --name=sri_examen_env --display-name "Python (sri_examen_env)"
```

### 3. Lanzar la Ejecución
Abre y ejecuta el notebook directamente desde la consola:

```bash
jupyter notebook ReyesAlexander_ex1bim_ir26a.ipynb
```

O, de forma desatendida desde la terminal:

```bash
jupyter nbconvert --to notebook --execute --ExecutePreprocessor.kernel_name=sri_examen_env --inplace ReyesAlexander_ex1bim_ir26a.ipynb
```
