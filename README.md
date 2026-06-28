# 📊 Predicción de Churn en Telecomunicaciones (Telco Customer Churn)

Este proyecto desarrolla un modelo predictivo robusto y parsimonioso utilizando **Regresión Logística** para identificar de forma proactiva a los clientes con alta probabilidad de abandonar la compañía (*Churn*). El enfoque combina metodologías avanzadas de selección algorítmica de variables (Wrapper y Embebidos) con una optimización del umbral de decisión orientada al retorno de inversión (ROI) del negocio.

---

## 🎯 Objetivos del Proyecto
* **Identificar los disparadores clave del Churn:** Analizar el impacto de factores estructurales (contratos, cargos mensuales, antigüedad).
* **Aplicar el Principio de Parsimonia:** Simplificar el modelo eliminando variables ruidosas, redundantes o colineales sin degradar su capacidad predictiva.
* **Optimizar el Umbral de Decisión:** Ajustar el modelo bajo un enfoque de Machine Learning para maximizar la sensibilidad (*Recall*) y capturar la mayor cantidad de bajas posibles con un coste comercial eficiente.

---

## 🛠️ Tecnologías Utilizadas
* **Lenguaje:** Python 3.x
* **Manipulación de Datos:** `pandas`, `numpy`
* **Modelado y Estadística:** `statsmodels` (Regresión Logística y análisis inferencial)
* **Algoritmos de Selección (Wrapper):** `mlxtend` (Sequential Feature Selector)
* **Evaluación y Regularización:** `scikit-learn` (GridSearchCV, Métricas de clasificación, curvas ROC/AUC)
* **Visualización de Datos:** `seaborn`, `matplotlib`

---

## 🔄 Pipeline del Proyecto (Estructura del Notebook)

### 1. Preparación de datos (Fase Inicial)
Consolidación, limpieza del dataset original y preprocesamiento de características.

### 2. Modelo Base de Regresión Logística
* **Ajuste Inicial:** Entrenamiento con el conjunto completo de variables para establecer un *baseline*.
* **Análisis de Umbrales:** Evaluación del rendimiento con el umbral estándar (0.5) y exploratorio (0.2).
* **Ajuste Estratégico:** Determinación del **umbral operativo de negocio (0.3)** como el punto óptimo de decisión.

### 3. Selección de Variables: Métodos de Filtro Estadístico
* **Diagnóstico de Multicolinealidad:** Cálculo del **VIF (Variance Inflation Factor)** para expulsar variables con alta dependencia lineal.
* **Importancia Relativa:** Análisis inferencial de la fuerza de los predictores.

### 4 & 5. Selección de Variables: Métodos Algorítmicos Wrapper (Envoltura)
* **Sequential Forward Selection (SFS):** Selección hacia adelante evaluando inicialmente la métrica *Accuracy*.
* **Descubrimiento del Modelo Campeón:** Optimización iterativa mediante la métrica **ROC-AUC**, reduciendo el ruido informático de manera drástica.

### 6. Estrategia Avanzada: Sequential Backward Selection (SBS)
* **Enfoque Estadístico:** Eliminación regresiva basada estrictamente en la significancia de los p-valores.
* **Enfoque de Machine Learning:** Selección hacia atrás optimizando por *Accuracy* y posteriormente por *ROC-AUC*. 
* *Nota de robustez:* Tanto el algoritmo hacia adelante (SFS) como hacia atrás (SBS) convergieron de manera exacta en las mismas variables.

### 7. Métodos Embebidos: Regularización de Coeficientes
* **Regularización L1 (LASSO):** Modelado manual con castigo de coeficientes para forzar la eliminación de variables no esenciales.
* **Regularización L2 (Ridge) + GridSearchCV:** Búsqueda en rejilla hiperparamétrica optimizando la constante $C$ a través de la métrica *ROC-AUC*.

---

## 📊 Resultados del Modelo Campeón (11 Variables - Umbral 0.3)

Tras someter los datos a todo el pipeline experimental, el modelo óptimo definitivo se consolidó con un subconjunto de **11 variables esenciales**, logrando un ajuste estadístico con un **Pseudo R-squared de 0.2767** y situándose en un rango de excelencia predictiva.

* **Área Bajo la Curva (AUC-ROC):** **0.844 (84.4%)**
* **Exactitud Global (Accuracy):** **77.00%**
* **Sensibilidad (Recall - Clase 1):** **77.00%** *(Captura a casi 8 de cada 10 clientes en fuga)*
* **Precisión (Clase 1):** **54.00%**

### Matriz de Confusión Final (Datos Reales de Entrenamiento):

| | Predicción: Se queda (0) | Predicción: Se va (1) |
|---|:---:|:---:|
| **Realidad: Se queda (0)** | **3,168** (56.23%) | **971** (17.23%) |
| **Realidad: Se marcha (1)** | **345** (6.12%) | **1,150** (20.41%) |

---

## 💎 Las 11 Variables Críticas Detectadas (Óptimo Global)
El proceso algorítmico demostró que el ecosistema mínimo y más potente para vigilar el Churn está compuesto por:
1. **Antigüedad del cliente:** `tenure` (El factor de retención orgánico más fuerte).
2. **Factores Económicos:** `MonthlyCharges` (Cargos mensuales).
3. **Contratos y Vinculación:** `Contract_One year` y `Contract_Two year`.
4. **Tecnología y Conectividad:** `InternetService_Fiber optic` y `InternetService_No`.
5. **Servicios de Valor Añadido:** `OnlineSecurity_Yes` y `TechSupport_Yes`.
6. **Facturación y Perfil:** `PaperlessBilling_Yes`, `PaymentMethod_Electronic check` y `Dependents_Yes`.

---

## 💡 Conclusiones Clave para el Negocio
1. **La Convergencia es Garantía:** Que los métodos *Forward* y *Backward* coincidan al 100% en las mismas 11 variables valida matemáticamente que este es el núcleo óptimo global para el negocio.
2. **El peligro de la tecnología y el precio:** Contratar Fibra Óptica y registrar altos cargos mensuales (`MonthlyCharges`) actúan como los principales catalizadores de riesgo de abandono.
3. **El Escudo Contractual:** Los contratos de 1 y 2 años, junto a los servicios de soporte técnico y seguridad online, reducen drásticamente los Odds (probabilidades) de fuga, siendo las palancas ideales para campañas de fidelización.
4. **Optimización con Ridge:** El GridSearchCV determinó que un valor de $C=10$ con regularización L2 equilibra perfectamente el modelo protegiéndolo contra el sobreajuste (*overfitting*).

---

## 🚀 Cómo ejecutar este proyecto
1. Descarga el dataset oficial desde [Kaggle - Telco Customer Churn](https://www.kaggle.com/datasets/blastchar/telco-customer-churn).
2. Clona este repositorio:
   ```bash
   git clone [https://github.com/nachofort/telco-customer-churn-prediction.git](https://github.com/nachofort/telco-customer-churn-prediction.git)
