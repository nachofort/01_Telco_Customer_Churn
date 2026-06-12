# 📊 Predicción de Churn en Telecomunicaciones (Telco Customer Churn)

Este proyecto desarrolla un modelo predictivo robusto y parsimonioso utilizando **Regresión Logística** para identificar de forma proactiva a los clientes con alta probabilidad de abandonar la compañía (*Churn*). El enfoque combina una rigurosa selección de características estadísticas con una optimización del umbral de decisión orientada al retorno de inversión (ROI) del negocio.

---

## 🎯 Objetivos del Proyecto
* **Identificar los disparadores clave del Churn:** Analizar el impacto de factores estructurales (contratos, cargos mensuales, antigüedad).
* **Aplicar el Principio de Parsimonia:** Simplificar el modelo eliminando variables ruidosas o redundantes sin degradar su capacidad predictiva.
* **Optimizar el Umbral de Decisión:** Ajustar el modelo para maximizar la sensibilidad (*Recall*) y capturar la mayor cantidad de bajas posibles con un coste comercial eficiente.

---

## 🛠️ Tecnologías Utilizadas
* **Lenguaje:** Python 3.x
* **Manipulación de Datos:** `pandas`, `numpy`
* **Modelado Estadístico:** `statsmodels` (Regresión Logística)
* **Evaluación de Modelos:** `scikit-learn` (Métricas de clasificación, curvas ROC/AUC)
* **Visualización de Datos:** `seaborn`, `matplotlib`

---

## 🔄 Pipeline del Proyecto

### 1. Análisis Exploratorio y Selección de Características (Feature Selection)
Para evitar la multicolinealidad y el ruido en el modelo, se segmentaron los análisis por tipo de variable:
* **Variables Categóricas:** Se utilizó la **V de Cramér** sobre tablas de contingencia para medir la fuerza de asociación con el Churn. Se descartaron servicios adicionales redundantes o de bajo impacto (< 0.10) como `StreamingTV` o `OnlineBackup`.
* **Variables Numéricas:** Se analizaron mediante **Diagramas de Caja (Boxplots)** y matrices de correlación lineal, confirmando que la antigüedad (`tenure`) y los cargos mensuales (`MonthlyCharges`) eran predictores clave libres de dependencia lineal entre sí.

### 2. Entrenamiento del Modelo
Se entrenó un modelo de Regresión Logística a través de `statsmodels.Logit`. El modelo depurado final arrojó un excelente ajuste estadístico con un **Pseudo R-squared de 0.2775** y un **AUC-ROC global de 0.836**, demostrando que vaciar el modelo de variables "paja" no afectó a su capacidad de discriminación.

### 3. Optimización del Umbral de Decisión (Estrategia de Negocio)
Se evaluó el rendimiento del modelo en el conjunto de validación (*Test*) simulando diferentes umbrales operativos (0.2, 0.3 y 0.5) para encontrar el equilibrio perfecto entre costes comerciales (Falsos Positivos) y fugas inadvertidas (Falsos Negativos).

---

## 📊 Resultados del Modelo Óptimo (Umbral 0.3)

Tras el análisis de sensibilidad, se seleccionó el **umbral operativo de 0.3** como el *sweet spot* estratégico para la compañía:

* **Exactitud Global (Accuracy):** 74.52%
* **Sensibilidad (Recall - Clase 1):** 75.13% *(Atrapa a 3 de cada 4 clientes en riesgo)*
* **Precisión (Clase 1):** 51.37% *(Más de la mitad de las alertas son casos reales)*

### Matriz de Confusión Final en Validación:

| | Predicción: No se va (0) | Predicción: Se va (1) |
|---|:---:|:---:|
| **Realidad: Se queda (0)** | **769** (Verdaderos Negativos) | **266** (Falsas Alarmas) |
| **Realidad: Se marcha (1)** | **93** (Fugas inadvertidas) | **281** (Fugas capturadas) |

---

## 💡 Conclusiones Clave para el Negocio
1. **Los Contratos a Largo Plazo salvan la cartera:** Los clientes con contratos de uno o dos años presentan los coeficientes de protección más fuertes contra la fuga en la Regresión Logística.
2. **El precio y la tecnología disparan el riesgo:** Tarifas elevadas (`MonthlyCharges`) y servicios de Fibra Óptica correlacionan positivamente con el abandono, señalando posibles problemas de competitividad o estabilidad del servicio.
3. **Eficiencia Comercial:** El umbral de 0.3 permite **ahorrar 90 ofertas promocionales innecesarias** en comparación con un umbral agresivo de 0.2, manteniendo un blindaje de cartera óptimo del 75.13%.

---

## 🚀 Cómo ejecutar este proyecto
1. Descarga el dataset oficial desde [Kaggle - Telco Customer Churn](https://www.kaggle.com/datasets/blastchar/telco-customer-churn).
2. Clona este repositorio:
   ```bash
   git clone https://github.com/nachofort/telco-customer-churn-prediction.git
