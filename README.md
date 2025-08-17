# Proyecto Telecom X Parte 2 - Predicción de Churn de Clientes

## 🎯 Objetivo del Proyecto

El propósito principal de este análisis es desarrollar un modelo predictivo capaz de identificar clientes con alta probabilidad de cancelar sus servicios (churn) en Telecom X. Este modelo permitirá a la empresa anticiparse al problema de la cancelación y diseñar estrategias proactivas de retención.

## 📁 Estructura del Proyecto

```
Alura-Challenge-Telecom-X-Parte-2/
│
├── datos_tratados.csv                          # Datos limpios y preparados para modelado
│
├── Alura-Challenge-Telecom-X-Parte-2.ipynb     # Parte 2: Modelado predictivo
│
└── README.md                                   # Este archivo
```

## 📊 Preparación de Datos

### Clasificación de Variables

**Variables Numéricas:**
- `cuenta_total`: Gasto total del cliente
- `antiguedad`: Meses como cliente
- `cuentas_mensuales`: Facturación mensual
- `cuentas_diarias`: Facturación diaria (derivada)

**Variables Categóricas:**
- `contrato`: Tipo de contrato (Month-to-month, One year, Two year)
- `servicio_internet`: Tipo de servicio de internet
- `metodo_pago`: Método de pago del cliente
- `lineas_multiples`: Servicio de líneas múltiples

### Etapas de Preprocesamiento

1. **Codificación**: Variables categóricas transformadas mediante one-hot encoding
2. **Imputación**: Valores faltantes en `cuenta_total` imputados con la media
3. **Normalización**: Aplicada a datos para modelos sensibles a la escala (Regresión Logística, SVM, KNN)
4. **Balanceo**: Aplicado SMOTE para manejar el desbalanceo de clases (2.77:1)

### Separación de Datos

- **División**: 70% entrenamiento / 30% prueba
- **Estratificación**: Mantenimiento de proporciones de clases
- **Conjuntos múltiples**: Diferentes versiones para distintos tipos de modelos

## 🧠 Modelización y Justificación de Decisiones

### Modelos Evaluados

1. **Random Forest**: Modelo basado en árboles, no requiere normalización
2. **Regresión Logística**: Modelo lineal, requiere datos normalizados
3. **K-Nearest Neighbors**: Modelo basado en distancia, requiere normalización
4. **SVM**: Modelo basado en vectores de soporte, requiere normalización

### Decisión del Modelo Final

**Regresión Logística** seleccionada como mejor modelo:
- **F1-Score**: 0.5888 (mejor balance entre precisión y recall)
- **Tiempo de entrenamiento**: 0.05 segundos (muy rápido)
- **Interpretabilidad**: Coeficientes explican claramente la influencia de variables

## 📈 Insights Clave del Análisis Exploratorio

### Variables Más Influyentes en el Churn

1. **contrato_month-to-month**: Correlación 0.405 (muy fuerte)
   - Clientes con contratos mensuales tienen 40% más riesgo de churn

2. **antiguedad**: Correlación -0.352 (fuerte negativa)
   - Clientes nuevos muestran mayor tendencia a cancelar

3. **cuenta_total**: Correlación -0.199 (moderada negativa)
   - Clientes con mayor gasto histórico tienden a permanecer

4. **cuentas_mensuales**: Correlación 0.193 (moderada)
   - Facturas mensuales altas correlacionan con mayor churn

### Hallazgos Principales

- **Contratos largos** son protectores contra el churn
- **Clientes nuevos** (menos de 6 meses) son de alto riesgo
- **Facturación alta** puede ser un factor de estrés que lleva al churn
- **Servicios adicionales** (internet fibra óptica) influyen en la retención

## 🚀 Instrucciones de Ejecución

### Requisitos Previos

En Google Colab, las principales bibliotecas ya están instaladas

### Carga de Datos en Google Colab

1. **Subir el archivo `datos_tratados.csv`**:
   - Haz clic en el ícono de carpetas en el panel izquierdo de Colab
   - Haz clic en "Upload" y selecciona tu archivo `datos_tratados.csv`

2. **Cargar los datos en el notebook**:

```python
import pandas as pd
df = pd.read_csv("datos_tratados.csv")
```

### Ejecución del Proyecto

Abre el notebook `Alura-Challenge-Telecom-X-Parte-2.ipynb` en Google Colab y ejecuta las celdas en orden secuencial.

## 📌 Recomendaciones Estratégicas

1. **Promoción de Contratos Largos**: Incentivar contratos de 1-2 años con descuentos
2. **Programa de Fidelización**: Beneficios especiales para clientes nuevos (< 6 meses)
3. **Gestión de Facturación**: Analizar y optimizar planes con facturas altas
4. **Segmentación de Clientes**: Sistema de alertas para perfiles de alto riesgo

## 📈 Resultados del Modelo

- **F1-Score**: 0.5888 (efectividad moderada)
- **Recall**: 0.5437 (detecta 54% del churn real)
- **Precisión**: 0.6421 (64% de predicciones positivas son correctas)
- **Impacto esperado**: Reducción del 15-20% en tasa de cancelación
