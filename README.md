# Predicción de abandono de clientes en telecomunicaciones

Proyecto de la Guía de Prácticas #01 de **Minería de Datos**, Universidad Estatal Amazónica.
Autor: Leonardo Andrés Valarezo Veintimilla · ORCID [0009-0001-9655-8468](https://orcid.org/0009-0001-9655-8468)

El objetivo es predecir si un cliente de una empresa de telecomunicaciones va a cancelar su servicio (*churn*), usando el proceso CRISP-DM: exploración, preprocesamiento, modelado y evaluación.

**Cuaderno en Colab:** https://colab.research.google.com/drive/1q54BdxVubXb9SyEsM21t706MuKhVHgB5?usp=sharing

## Datos

- **Dataset:** Telco Customer Churn, IBM (2019). 7043 clientes y 21 variables.
- **Fuente:** https://github.com/IBM/telco-customer-churn-on-icp4d (también en [Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)).
- Una copia está en `data/Telco-Customer-Churn.csv`.

## Estructura

```
├── notebook/Churn_Telco_Mineria_de_Datos.ipynb   Cuaderno completo (se puede abrir en Google Colab)
├── data/                                          Dataset original
├── figuras/                                       Gráficos generados por el cuaderno
└── modelo/                                        Modelo entrenado (.joblib) y tablas de métricas
```

## Qué se hizo

1. **Exploración:** estadística descriptiva (media, mediana, desviación, asimetría, curtosis), nulos por variable, duplicados, atípicos con IQR y 7 visualizaciones.
2. **Traducción:** nombres de variables y categorías pasados al español (por ejemplo `tenure` → `MesesCliente`, `Churn` → `Abandono`).
3. **Preprocesamiento:** 11 nulos de `CargoTotal` completados con 0 (clientes sin facturar), 22 duplicados eliminados, unificación de categorías, One-Hot Encoding y StandardScaler.
4. **Variables nuevas:** `NumServicios`, `CargoPromedioMensual` y `GrupoAntiguedad`.
5. **Análisis descriptivo:** PCA y segmentación con K-Means (k = 3).
6. **Modelos:** Regresión Logística, Árbol de Decisión y Random Forest (80 % entrenamiento / 20 % prueba, estratificado).
7. **Evaluación:** Accuracy, Precision, Recall, F1, AUC-ROC, matrices de confusión y validación cruzada estratificada de 5 particiones.

## Resultados

| Modelo | Accuracy | Precision | Recall | F1 | AUC-ROC |
|---|---|---|---|---|---|
| Regresión Logística | 0,737 | 0,503 | 0,774 | 0,610 | 0,840 |
| Árbol de Decisión | 0,745 | 0,513 | 0,761 | 0,613 | 0,831 |
| **Random Forest** | **0,760** | **0,533** | **0,766** | **0,628** | **0,843** |

Validación cruzada (5 folds, F1): Regresión Logística 0,628 ± 0,022 · Árbol 0,625 ± 0,023 · Random Forest 0,639 ± 0,017.
El mejor modelo fue el **Random Forest**.

## Cómo ejecutar

### Cuaderno
Abrir el cuaderno en Google Colab: https://colab.research.google.com/drive/1q54BdxVubXb9SyEsM21t706MuKhVHgB5?usp=sharing

También está en `notebook/Churn_Telco_Mineria_de_Datos.ipynb`. Hay que ejecutar todas las celdas en orden. Los datos se descargan solos desde GitHub.
