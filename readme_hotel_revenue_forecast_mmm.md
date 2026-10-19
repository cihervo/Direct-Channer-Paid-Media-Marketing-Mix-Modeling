# 🏨 Hotel Revenue Forecasting & Marketing Mix Modeling (MMM)
*Optimización de Presupuestos de Paid Media y Proyección de Revenue Hotelero*

[![Python Version](https://img.shields.io/badge/Python-3.9%2B-blue.svg)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Framework](https://img.shields.io/badge/Framework-DMAIC-orange.svg)](#metodología-dmaic)
[![Status](https://img.shields.io/badge/Project%20Status-Complete-success.svg)]()

> **Languages / Idiomas:** [English](#english-version) | [Español](#versión-en-español)

---

<a name="english-version"></a>
## 🌐 English Version

### Executive Summary
This project develops an end-to-end econometric **Marketing Mix Model (MMM)** in Python to quantify the incremental revenue impact of multi-channel advertising (Google Ads, Meta Ads, and TikTok Ads) for hotel direct web bookings. By leveraging non-linear transformations—specifically geometric **Adstock** and the **Hill Saturation Function**—alongside multiple linear regression, this project isolates baseline organic bookings, accurately captures diminishing returns, and outputs granular monthly budget allocation scenarios.

### Business Problem
A persistent challenge in hotel digital marketing is the reliance on linear budget scaling (assuming that doubling media spend will double revenue at a static CPA). In reality, audience saturation and competitive bidding lead to escalating marginal CPAs and margin erosion. This project solves that problem by answering:
1. What is the diminishing return curve for each advertising channel?
2. How does advertising memory (adstock decay) influence booking cycles?
3. What is the optimal budget allocation to maximize net revenue while keeping blended CPA within strict profitability boundaries?

### Mathematical Foundations

#### 1. Geometric Adstock (Advertising Memory Effect)
Advertising exposure generates lingering consumer recall that decays over time. The carryover effect is defined recursively:
$$Adstock_t = Spend_t + \lambda \cdot Adstock_{t-1}$$
where $\lambda \in [0, 1]$ represents the retention/decay parameter for each specific channel (e.g., lower $\lambda$ for high-intent Google Search, higher $\lambda$ for upper-funnel TikTok discovery).

#### 2. Hill Saturation Function (Diminishing Marginal Returns)
To prevent infinite returns and model capacity constraints, spend is passed through a sigmoidal Hill function:
$$Saturation(x) = \frac{x^\alpha}{x^\alpha + \gamma^\alpha}$$
* $\alpha$ (shape parameter): Dictates curve curvature (diminishing vs. S-curve behavior).
* $\gamma$ (half-saturation point): Represents the inflection point where spending yields diminishing marginal returns.

### DMAIC Methodology Framework

* **Define:** Formulate the objective to replace static yearly budgets with a dynamic elasticity-driven forecasting engine for hotel web revenue.
* **Measure:** Aggregate over 100,000 anonymized booking records into a 114-week time series, capturing seasonality, length of stay, and Average Daily Rate (ADR).
* **Analyze:** Train a multi-variable regression engine on transformed adspend variables ($X_{transf}$) against total booking revenue ($Y$).
  * **$R^2$ (Coefficient of Determination):** **89.92%** (Explaining nearly 90% of revenue variance).
  * **MAPE (Mean Absolute Percentage Error):** **19.92%** (Executive forecast accuracy of 80.08%).
* **Improve:** Model 3 forward-looking budget scenarios (Conservative, Optimal, Aggressive) simulating monthly YoY growth in spend, revenue, and blended CPA.
* **Control:** Export structured forecast datasets ready for automated ingestion into BI dashboards (Looker Studio) with built-in CPA circuit-breakers.

### Strategic Scenarios Comparison

| Scenario | Strategic Focus | Budget Allocation Strategy | Business Impact |
| :--- | :--- | :--- | :--- |
| **Conservative** | Margin Protection | Flat spend focused purely on high-intent Google Search. | Maximizes ROAS and cash flow; leaves potential revenue on the table. |
| **Optimal (Recommended)** | Net Revenue Maximization | Spend calibrated to the inflection point where marginal CPA equals marginal booking margin. | **Recommended plan:** Balances volume growth with efficiency, preventing saturation penalties. |
| **Aggressive** | Market Share Capture | Aggressive scaling across Meta and TikTok during seasonal peaks. | Maximizes gross room-night volume and occupancy, with controlled margin compression. |

### Visualizations

#### 1. Investment & CPA Forecast (Optimal Scenario)
`images/grafico_inversion_cpa_optimo.png`
*Displays monthly requested capital alongside target CPA% benchmarks.*

#### 2. Paid Media Mix Distribution
`images/grafico_mix_canales_optimo.png`
*Stacked allocation showing dynamic channel weighting across seasonality peaks.*

---

<a name="versión-en-español"></a>
## 🇪🇸 Versión en Español

### Resumen Ejecutivo
Este proyecto desarrolla un modelo econométrico de **Marketing Mix Modeling (MMM)** en Python para cuantificar el impacto incremental de la inversión publicitaria omnicanal (Google Ads, Meta Ads y TikTok Ads) en las reservas directas de cadenas hoteleras. Mediante transformaciones no lineales de **Adstock** geométrico y curvas de **Saturación de Hill**, el modelo aísla el tráfico orgánico base, mapea los rendimientos decrecientes y genera proyecciones presupuestarias mensuales bajo tres escenarios ejecutivos.

### Planteamiento del Problema
Un error recurrente en el marketing hotelero es asumir una relación lineal en la pauta (creer que duplicar el gasto duplicará las reservas al mismo CPA). En la práctica, la saturación de audiencias y la estacionalidad disparan el CPA marginal y comprimen el margen neto. Este proyecto responde analíticamente:
1. ¿Cuál es el punto de saturación y rendimiento decreciente de cada canal?
2. ¿Cómo influye el efecto residual de la publicidad en las decisiones de reserva diferidas?
3. ¿Cuál es la asignación óptima de inversión para maximizar el Revenue neto protegiendo el CPA objetivo del hotel?

### Fundamentos Matemáticos

#### 1. Transformación Adstock (Efecto Memoria)
Modela el impacto residual de la publicidad en el tiempo de forma recursiva:
$$Adstock_t = Spend_t + \lambda \cdot Adstock_{t-1}$$
donde $\lambda \in [0, 1]$ es el coeficiente de retención del canal (Google Ads con decaimiento rápido por intención directa; TikTok y Meta con mayor retención por descubrimiento).

#### 2. Función de Saturación de Hill (Rendimientos Decrecientes)
Mapea la compresión de eficiencia al incrementar la inversión:
$$Saturacion(x) = \frac{x^\alpha}{x^\alpha + \gamma^\alpha}$$
donde $\alpha$ determina la concavidad de la respuesta y $\gamma$ el punto de inflexión a partir del cual el costo por adquisición (CPA) marginal comienza a dispararse.

### Metodología de Resolución (Ciclo DMAIC)

* **Definir (Define):** Establecer el modelo econométrico para sustituir presupuestos planos por un pronóstico dinámico basado en elasticidad publicitaria.
* **Medir (Measure):** Procesar más de 100,000 registros transaccionales agregados en 114 semanas, consolidando ADR, estacionalidad e ingresos efectivos.
* **Analizar (Analyze):** Entrenamiento de regresión lineal múltiple sobre variables publicitarias transformadas:
  * **$R^2$ (Coeficiente de Determinación):** **89.92%** (Explica el 89.92% de la variación del Revenue).
  * **MAPE (Margen de Error Promedio):** **19.92%** (Precisión global del 80.08%).
* **Mejorar (Improve):** Proyección mes a mes de 3 escenarios comparativos interanuales (YoY) para Revenue, Pauta y CPA porcentual.
* **Controlar (Control):** Exportación en formato tabular para integración con tableros de BI (Google Looker Studio), estandarizando auditorías de rentabilidad publicitaria.

### Comparativa de Escenarios de Negocio

| Escenario | Enfoque Estratégico | Estrategia de Asignación | Impacto en Negocio |
| :--- | :--- | :--- | :--- |
| **Conservador** | Protección de Margen | Mantenimiento de inversión base enfocado en búsqueda de alta intención. | Maximiza el ROAS protegiendo flujo de caja; sacrifica volumen de reservas. |
| **Óptimo (Recomendado)** | Maximización de Revenue Neto | Presupuesto calibrado al punto de inflexión donde el beneficio marginal iguala al costo marginal. | **Plan recomendado:** Maximiza ingresos netos manteniendo el CPA bajo control. |
| **Agresivo** | Cuota de Mercado | Escala intensiva en Meta y TikTok en picos estacionales de alta demanda. | Maximiza ocupación y volumen bruto, aceptando una compresión controlada de margen. |

---

## 📂 Repository Structure / Estructura del Repositorio

```text
hotel-mmm-forecast/
│
├── data/
│   ├── hotel_bookings.csv                <- Raw dataset (Kaggle public benchmark)
│   ├── weekly_hotel_data.csv             <- Cleaned & aggregated weekly series
│   └── forecast_mensual_escenarios.csv   <- Model scenario outputs for BI ingestion
│
├── notebooks/
│   └── mmm_hotel_forecast.ipynb          <- Complete pipeline: EDA, Adstock, Hill & Scenarios
│
├── images/
│   ├── grafico_inversion_cpa_optimo.png  <- Requested spend & projected CPA%
│   ├── grafico_mix_canales_optimo.png    <- Stacked channel media mix
│   └── grafico_forecast_lineas.png       <- Revenue vs. Spend scenario curves
│
├── requirements.txt                      <- Environment dependencies
└── README.md                             <- Project documentation
```

## 🛠️ Tech Stack & Dependencies
* **Core Language:** Python 3.9+
* **Data Processing & Analytics:** `pandas`, `numpy`
* **Machine Learning & Modeling:** `scikit-learn`
* **Visualization & Reporting:** `matplotlib`, `seaborn`
* **BI Ingestion:** Compatible with Google Looker Studio / Power BI

## 🚀 How to Run / Instrucciones de Ejecución
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/hotel-mmm-forecast.git
   cd hotel-mmm-forecast
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Open and run the Jupyter Notebook:
   ```bash
   jupyter notebook notebooks/mmm_hotel_forecast.ipynb
   ```

---
*Author / Autor:* **[Tu Nombre / Your Name]**  
*Specialization:* Marketing Analytics | Paid Media Strategy | Revenue Econometrics  
*Connect on LinkedIn / Conecta en LinkedIn:* [LinkedIn Profile URL]