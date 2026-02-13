# ☀️ Solar Fleet Analytics Engine (v1.0)

![Python](https://img.shields.io/badge/Python-3.9%2B-blue?style=for-the-badge&logo=python)
![Status](https://img.shields.io/badge/Status-Production%20Ready-success?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

A robust, automated auditing tool designed to analyze the efficiency of large-scale Solar Photovoltaic (PV) power plants. This engine processes raw SCADA production data, integrates satellite-based meteorological data, and generates actionable performance reports using the **Performance Ratio (PR)** metric.

---

## 🚀 Key Features

* **🔍 Smart Data Mining:** Automatically detects "Production/Yield" columns in raw Excel files using keyword pattern matching (supports multi-language headers).
* **🛰️ Satellite Intelligence:** Fetches real-time Global Horizontal Irradiance (GHI) data for specific coordinates via the **Open-Meteo API**.
* **📐 Physics Engine:** Calculates *Expected Energy* based on installed capacity (kWp), geometric tilt correction (Winter/Summer factors), and system loss coefficients.
* **🧹 Auto-Sanitization:**
    * Removes duplicate daily logs using `groupby()` logic.
    * Auto-corrects unit mismatches (MWh vs kWh).
    * Filters out physical anomalies (e.g., PR > 100%).
* **📊 Executive Reporting:** Generates a "Traffic-Light" visualization (Green/Yellow/Red) and a professional Excel audit report.

---

## 🧠 Methodology & Logic

The core algorithm operates in 5 stages:

1.  **Data Ingestion:** Scans the directory for `.xlsx` files and identifies the target period (e.g., `2026-01`).
2.  **Sanitization:** Cleanses the dataset by aggregating daily sums and removing outliers.
3.  **Irradiance Mapping:** Queries satellite APIs for the exact latitude/longitude of the plant.
4.  **Performance Calculation:**
    $$PR = \frac{Actual~Yield~(kWh)}{Irradiance \times Capacity \times TiltFactor \times \eta_{sys}}$$
5.  **Audit & Visualization:** Classifies plants into performance tiers:
    * 🟢 **Excellent:** PR ≥ 85%
    * 🟡 **Standard:** 70% ≤ PR < 85%
    * 🔴 **Review Needed:** PR < 70%

---

## 🛠️ Installation & Usage

1.  **Clone the Repository:**
    ```bash
    git clone [https://github.com/YourUsername/Solar-Fleet-Analytics-Engine.git](https://github.com/YourUsername/Solar-Fleet-Analytics-Engine.git)
    ```

2.  **Install Dependencies:**
    ```bash
    pip install pandas requests openpyxl matplotlib
    ```

3.  **Configure Your Plants:**
    Open the script and edit the `[MANUAL CONFIGURATION AREA]` to add your plant details:
    ```python
    PLANTS = [
        {"id": "Plant_A", "file": "scada_data.xlsx", "kwp": 1200, "lat": 41.00, "lon": 28.97},
        # Add more plants here...
    ]
    ```

4.  **Run the Analysis:**
    ```bash
    python solar_analytics.py
    ```

---

## 📈 Sample Output

The tool generates a **Professional Audit Report (`.xlsx`)** and a **Performance Chart (`.png`)**:

*(You can upload your 'Fleet_Performance_Chart.png' here)*

---

### 👨‍💻 Author
Developed as an advanced engineering project for renewable energy data analytics.
