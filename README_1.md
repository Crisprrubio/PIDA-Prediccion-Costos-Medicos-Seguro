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
  2. Entendimiento de los datos (EDA: estadísticas descriptivas, visualizaciones, hallazgos)
  3. Preparación de los datos (codificación, features de interacción, justificación de decisiones)
  4. Modelación y evaluación (comparación de 3 modelos, ajuste de hiperparámetros, selección del modelo final)

## Resultados

| Modelo | R² | MAE | MSE |
|---|---|---|---|
| **Regresión Lineal (final)** | **0.879** | **USD 2,378** | 18,752,018 |
| Random Forest | 0.864 | USD 2,554 | 21,167,834 |
| Árbol de Decisión | 0.848 | USD 2,872 | 23,580,839 |

El modelo final (Regresión Lineal, con variables de interacción fumador×IMC) **supera ambas metas** del criterio de éxito: R² ≈ 0.88 (meta ≥ 0.75) y MAE ≈ USD 2,378 (meta ≤ USD 4,000, ~41% mejor que el umbral).

## Cómo ejecutar

```bash
pip install -r requirements.txt
jupyter notebook PIDA-Notebook-Completo.ipynb
```
