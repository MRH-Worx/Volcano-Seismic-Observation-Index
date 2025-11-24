# 🌋 Volcano Seismic Observation Index (VSOI)

### *A daily metric for quantifying and visualizing volcanic seismic unrest*

The **Volcano Seismic Observation Index (VSOI)** is an open-science tool for monitoring volcanic seismicity using publicly available earthquake data from the USGS.  
It computes a standardized **daily unrest score (0–100)** based on:

- 📈 **Earthquake frequency**
- 💥 **Magnitude distribution (90th percentile)**
- 🕳 **Depth characteristics (shallow % < 5 km)**

This score highlights changes in seismic behavior that may reflect magmatic unrest.  
The framework is designed to be transparent, reproducible, and extendable to any volcano with basic seismic data.

---

## 🔍 Project Goals

- Provide a **quantitative indicator** of daily volcanic seismic unrest.
- Use **only open data and open-source tools** (R + USGS).
- Enable scientists, students, and citizen-researchers to explore volcanic activity.
- Support **future modules** such as clustering, forecasting, and AI interpretation.

---

## 📦 Features

### **Current (v0.x)**
- ✔ Automated USGS data retrieval  
- ✔ Daily seismic metric extraction  
- ✔ Standardized unrest score (0–100)  
- ✔ Fixed & rolling baselines (3 / 5 / 7 / 10 years + full historical)  
- ✔ Visualization with 7-day smoothing  
- ✔ Interactive hover tooltips (Plotly)  

### **Coming Soon**
- 🔄 Seismic swarm boundary detection (DBSCAN / OPTICS)  
- 📈 Forecasting module (ARIMA / machine learning)  
- 🧠 AI-generated scientific interpretations  
- 🌎 Multi-volcano dashboard (Shiny)  

---

## 🚀 Getting Started

### 🔧 Requirements

- **R ≥ 4.0**
- Recommended packages:

```r
tidyverse
httr
jsonlite
plotly
zoo
lubridate
```

### 📥 Install Required Packages

```r
install.packages(c("tidyverse", "httr", "jsonlite", "plotly", "zoo", "lubridate"))
```

---

## 🧠 Concept: How VSOI Works

The VSOI score compares current seismic activity against a statistical baseline:

| Metric        | Description |
|---------------|-------------|
| `n_events`    | Daily earthquake count |
| `p90_mag`     | 90th percentile magnitude (captures larger events without outlier bias) |
| `shallow_pct` | Fraction of earthquakes occurring at depths < 5 km |

Each metric is standardized using a z-score relative to a baseline window.  
Values are then scaled, clipped (0–1), and averaged into a **0–100 unrest score**:

```r
unrest_score = 100 * (I_n + I_p90 + I_shp) / 3
```

---

## 📊 Example Output (Trident Volcano, Alaska)

| Date       | Score | Status |
|------------|-------|--------|
| 2021-06-12 | 4.2   | 🟢 Green |
| 2022-10-01 | 46.7  | 🟠 Orange |
| 2023-01-20 | 71.3  | 🔴 Red |

---

## 🧪 Data Integrity Checks

VSOI includes optional diagnostics to prevent silent data errors:

- 📌 Raw event count = sum of daily counts  
- 📌 Shallow % must fall between 0 and 1  
- 📌 All events must fall within the selected volcano boundary  
  *(unless clustering boundary mode is enabled)*  

These tests can run silently within R Markdown to safeguard results.

---

## 🧑‍💻 Recommended Project Structure

```text
VSOI/
├── R/                # Functions (scoring, baselines, clustering, forecasting)
├── data/             # Cached USGS JSON pulls (optional)
├── scripts/          # Tests, diagnostics, spot checks
├── docs/             # Rendered markdown, reports
├── dashboard/        # Future Shiny app
└── README.md         # You are here
```

---

## 🤝 Contributing

This project welcomes contributions from:

- 🌋 Volcanologists  
- 🌎 Seismologists  
- 👩‍💻 Developers & data scientists  
- 🧪 Students & citizen scientists  

> **Knowledge contributions are as valuable as code.**  
> Issues, suggestions, and pull requests are encouraged!

---

## 📜 License

**MIT License** — open for research, modification, and commercial use with attribution.

---

## 🌟 Acknowledgments

- **USGS Earthquake Hazards Program**
- **Open-source R community**
- Inspiration from global volcano observatories and monitoring networks

---
