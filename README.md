#  Australian Vehicle Price Prediction

Proyecto de Data Science que aplica **Random Forest** y **Extra-Trees Regressor** para predecir el precio de vehículos usados en el mercado australiano, comparando el rendimiento de ambos modelos mediante métricas estándar de regresión.

---

##  Pregunta de Negocio

> **¿Es posible predecir el precio de un vehículo en Australia a partir de sus características técnicas y de uso?**

Variables como el año, los kilómetros recorridos, el tipo de motor, la transmisión y el combustible contienen información suficiente para estimar el valor de mercado de un auto con buena precisión.

---

##  Estructura del Repositorio

```
australian-vehicle-price-prediction/
│
├── data/
│   └── Australian_Vehicle_Prices.csv   # Dataset original (~16.700 registros)
│
├── RandomForest_and_ExtraTrees.ipynb   # Notebook principal con análisis completo
├── requirements.txt                    # Dependencias del proyecto
└── README.md
```

---

##  Metodología

### 1. Limpieza y Preprocesamiento
- Eliminación de registros sin precio (variable objetivo)
- Conversión forzada a numérico con `pd.to_numeric(errors='coerce')` para manejar valores no estándar
- Imputación de kilómetros faltantes con la **mediana global**
- Extracción de variables desde texto con **regex**:
  - `FuelConsumption` → `FuelConsumption_per_km` (litros/100km)
  - `Engine` → `CylindersinEngine` y `LiterEngine`
- Imputación de variables extraídas con su mediana respectiva

### 2. Feature Engineering
- Selección de variables numéricas: `Year`, `Kilometres`, `FuelConsumption_per_km`, `CylindersinEngine`, `LiterEngine`
- Codificación de variables categóricas (`UsedOrNew`, `Transmission`, `FuelType`) con **One-Hot Encoding** y `drop_first=True`

### 3. Modelos Entrenados

####  Random Forest Regressor
- `n_estimators=100`, `random_state=42`
- División train/test: 80/20

####  Extra-Trees Regressor
- `n_estimators=100`, `max_depth=15`, `random_state=42`, `n_jobs=1`
- Mismo split para comparación directa

### 4. Evaluación y Comparación

| Métrica | Random Forest | Extra-Trees |
|---------|--------------|-------------|
| **MAE** (error promedio) | ~$7.723 AUD | — |
| **RMSE** (penaliza outliers) | ~$18.562 AUD | — |
| **R²** (varianza explicada) | **0.755** | — |

> El modelo explica el **75,5% de la variación** en los precios, cometiendo un error promedio de ~$7.700 AUD por vehículo. El RMSE mayor que el MAE indica que hay casos extremos (autos de lujo o colección) que el modelo predice con menor precisión.

### 5. Importancia de Variables
Se visualizó el **Top 10 de características más influyentes** en la predicción del precio mediante `feature_importances_` de Random Forest.

---

##  Cómo Ejecutar

### 1. Clonar el repositorio
```bash
git clone https://github.com/TU_USUARIO/australian-vehicle-price-prediction.git
cd australian-vehicle-price-prediction
```

### 2. Instalar dependencias
```bash
pip install -r requirements.txt
```

### 3. Abrir el notebook
```bash
jupyter notebook RandomForest_and_ExtraTrees.ipynb
```

---

##  Stack Tecnológico

| Herramienta | Uso |
|-------------|-----|
| `pandas` | Limpieza, imputación y transformación de datos |
| `numpy` | Operaciones matemáticas y manejo de arrays |
| `scikit-learn` | RandomForestRegressor, ExtraTreesRegressor, métricas |
| `matplotlib` | Visualizaciones |
| `seaborn` | Gráfico de importancia de variables |

---

##  Dataset

- **Fuente:** Australian Vehicle Prices (Kaggle)
- **Registros:** ~16.700 vehículos
- **Variables clave:** `Brand`, `Year`, `Model`, `Transmission`, `Engine`, `FuelType`, `FuelConsumption`, `Kilometres`, `Price`

---

## 📐 Métricas Explicadas

- **MAE:** Error promedio en dólares. Cuánto se equivoca el modelo en cada predicción.
- **RMSE:** Penaliza errores grandes. Si es mucho mayor que el MAE, hay outliers difíciles de predecir.
- **R²:** Proporción de la varianza del precio explicada por el modelo. 1.0 = perfecto, 0 = no mejor que predecir el promedio.

---

##  Autor

**Matías Mora Poblete**  
Estudiante de Ingeniería Civil Industrial — Universidad Diego Portales  
[LinkedIn](https://linkedin.com/in/MatiasMoraP)

---

## 📄 Licencia

Este proyecto es de uso educativo y libre para referencia.
