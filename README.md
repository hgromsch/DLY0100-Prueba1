# Clasificación de caracteres Kuzushiji con una Red Neuronal (MLP)

**Evaluación Parcial N° 1 — Deep Learning (DLY0100) · Duoc UC**

Implementación de una **red neuronal artificial multicapa (MLP)** en Python con **TensorFlow/Keras** para clasificar imágenes de caracteres cursivos japoneses (**Kuzushiji-MNIST**) en 10 clases de hiragana. El proyecto aplica experimentos controlados de hiperparámetros, comparación experimental de funciones de activación/pérdida, técnicas de regularización y evaluación con métricas de clasificación.

---

## 📋 Contenido del repositorio

| Archivo / carpeta | Descripción |
|---|---|
| `EP1_DLY0100_Kuzushiji_MLP.ipynb` | **Cuaderno Jupyter principal** (informe): todo el desarrollo documentado con Markdown, código y visualizaciones. |
| `EP1_Presentacion_Kuzushiji_MLP.pptx` | Presentación de la defensa oral (18 láminas). |
| `modelo_final_kmnist.keras` | Modelo final entrenado (serializado con Keras). |
| `data/` | Dataset Kuzushiji-MNIST (archivos `.npz` y mapa de clases). Se descarga automáticamente si no existe. |
| `figs/` | Gráficos y tablas generados por el notebook (usados en la presentación). |

---

## 🗂️ Dataset

**Kuzushiji-MNIST** (del dataset [anokas/kuzushiji](https://www.kaggle.com/datasets/anokas/kuzushiji), creado por CODH — Center for Open Data in the Humanities):

| Característica | Valor |
|---|---|
| Imágenes de entrenamiento | 60.000 |
| Imágenes de prueba | 10.000 |
| Tamaño | 28×28 píxeles, escala de grises |
| Clases | 10 (お, き, す, つ, な, は, ま, や, れ, を) |
| Balance | 6.000 ejemplos por clase |

> Licencia CC BY-SA 4.0. Referencia: Clanuwat et al. (2018), *Deep Learning for Classical Japanese Literature* ([arXiv:1812.01718](https://arxiv.org/abs/1812.01718)).

---

## 🧠 Metodología (resumen)

1. **Carga y preprocesamiento:** normalización a [0,1], aplanado 28×28→784, one-hot encoding, división 54.000 train / 6.000 validación / 10.000 test.
2. **Modelo base MLP:** 784 → 128 (ReLU) → 64 (ReLU) → 10 (Softmax), Adam, cross-entropy.
3. **Experimentos controlados** (un parámetro a la vez): tasa de aprendizaje {0.1, 0.01, 0.001, 0.0001}, batch size {32, 64, 128, 256}, número de épocas (diagnóstico de sobreajuste).
4. **Comparación de funciones:** activaciones (ReLU vs sigmoid vs tanh) y pérdidas (cross-entropy vs MSE).
5. **Regularización:** Dropout(0.3), Batch Normalization y Early Stopping, comparados con/sin optimización.
6. **Evaluación:** accuracy, precision, recall y F1-score (macro) sobre test + matriz de confusión y análisis de errores.

## 📊 Resultado del modelo final

| Configuración | ReLU + Softmax + Cross-entropy · Adam (lr=0,001) · batch 64 · Dropout(0,3) + BatchNorm + Early Stopping |
|---|---|

| Métrica (test) | Valor |
|---|---|
| **Accuracy** | **0,8845** |
| Precision (macro) | 0,8856 |
| Recall (macro) | 0,8845 |
| F1-score (macro) | 0,8844 |

Accuracy en validación: **0,9543**. Los errores se concentran en pares de caracteres cursivamente similares (na↔re, ya↔re, su↔na).

---

## 🚀 Cómo ejecutar el proyecto

### Requisitos
- Python 3.10+
- Paquetes: `tensorflow`, `numpy`, `pandas`, `matplotlib`, `seaborn`, `scikit-learn`

```bash
pip install tensorflow numpy pandas matplotlib seaborn scikit-learn
```

### Ejecución local

```bash
# 1. Clonar el repositorio
git clone https://github.com/hgromsch/DLY0100-Prueba1
cd DLY0100-Prueba1

# 2. Abrir el notebook
jupyter notebook EP1_DLY0100_Kuzushiji_MLP.ipynb
```

El dataset se **descarga automáticamente** en la carpeta `data/` al ejecutar la celda de carga (no requiere credenciales de Kaggle).

### Ejecución en Google Colab

1. Subir `EP1_DLY0100_Kuzushiji_MLP.ipynb` a [Google Colab](https://colab.research.google.com).
2. Ejecutar todas las celdas (*Entorno de ejecución → Ejecutar todas*). El dataset se descarga solo.
3. Los gráficos y tablas se guardan en `figs/` y el modelo en `modelo_final_kmnist.keras`.

---

## 👥 Autores

- Heinrich Werner Gromsch Sanz

**Docente:** Victor Andres Trigo Rojas — Asignatura DLY0100 Deep Learning, Duoc UC, 2026.
