# Predicción de Costos Médicos de Seguro mediante Regresión

Proyecto Integrador de Dominio Autónomo (PIDA) — Certificación **Citizen Data Scientist**, Tec de Monterrey.

**Participante:** Jose Cristian Pérez Rubio

## Contexto

El proyecto se desarrolla como parte de la práctica del participante como agente de seguros, en el proceso de asesoría y cotización de pólizas de gastos médicos. Durante la suscripción se evalúan factores de riesgo del asegurado (tabaquismo, sedentarismo, etc.), generalmente mediante tarifas o categorías de riesgo fijas aplicadas de forma independiente para cada factor, sin capturar cómo interactúan entre sí.

## Objetivo

Desarrollar un modelo de regresión que prediga el costo médico anual de un cliente, e identificar y cuantificar los factores (predictores) con mayor influencia sobre dicho costo — incluyendo la interacción entre factores de riesgo (p. ej. tabaquismo + IMC elevado).

**Criterio de éxito:**
- R² ≥ 0.75
- MAE ≤ USD 4,000

## Dataset

[`insurance.csv`](insurance.csv) — [Medical Cost Personal Datasets](https://www.kaggle.com/datasets/mirichoi0218/insurance) (Kaggle). 1,338 registros, 7 variables: `age`, `sex`, `bmi`, `children`, `smoker`, `region`, `charges`.

## Contenido

- [`PIDA-Notebook-Completo.ipynb`](PIDA-Notebook-Completo.ipynb) — notebook con las 4 etapas del proyecto:
  1. Entendimiento del negocio (antecedentes, problema, objetivos, diccionario de datos)
  2. Entendimiento de los datos (EDA: estadísticas descriptivas, visualizaciones univariadas/bivariadas/multivariadas, hallazgos)
  3. Preparación de los datos (codificación, feature de interacción `smoker_bmi`, justificación de decisiones)
  4. Modelación y evaluación (comparación de 3 modelos, ajuste de hiperparámetros, búsqueda ampliada con AutoML, importancia de variables, selección del modelo final)

## Resultados

| Modelo | R² | MAE | MSE | Tiempo entrenamiento |
|---|---|---|---|---|
| Random Forest | 0.866 | USD 2,552 | 20,838,910 | 0.49 s |
| **Regresión Lineal (final)** | **0.865** | **USD 2,757** | 20,919,720 | 0.002 s |
| Árbol de Decisión | 0.848 | USD 2,872 | 23,580,839 | 0.002 s |

Random Forest y Regresión Lineal quedan prácticamente empatados (diferencia de ~0.0005 en R² y ~USD 205 en MAE, dentro del margen de variación esperable de una sola partición train/test). Se elige la **Regresión Lineal** como modelo final por su interpretabilidad: con la variable de interacción `smoker_bmi`, captura de forma explicable el efecto conjunto de fumar y el IMC, algo que el Random Forest no ofrece con la misma claridad.

**Ajuste de hiperparámetros** (Ridge, variables escaladas): alpha=0.1, R² ≈ 0.865, MAE ≈ USD 2,758 — prácticamente idéntico a la Regresión Lineal sin regularizar, esperable dado el tamaño y simplicidad del conjunto de datos.

**Búsqueda ampliada (AutoML, FLAML):** el mejor algoritmo encontrado (XGBoost) alcanzó R² ≈ 0.880 y MAE ≈ USD 2,433 — el mejor resultado numérico del proyecto, aunque sin representar una mejora determinante frente a los modelos manuales.

El modelo final (Regresión Lineal) **supera ambas metas** del criterio de éxito: R² ≈ 0.865 (meta ≥ 0.75) y MAE ≈ USD 2,757 (meta ≤ USD 4,000, ~31% mejor que el umbral).

## Cómo ejecutar

```bash
pip install -r requirements.txt
jupyter notebook PIDA-Notebook-Completo.ipynb
```
