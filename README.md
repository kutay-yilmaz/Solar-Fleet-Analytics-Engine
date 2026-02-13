# Solar Fleet Performance Analytics Engine

## Abstract
This project presents an automated auditing tool developed to analyze the efficiency of large-scale Solar Photovoltaic (PV) power plants. The engine processes raw SCADA production data, integrates satellite-based meteorological data via Open-Meteo API, and generates actionable performance reports using the Performance Ratio (PR) metric. The system is designed to minimize human error in data processing and provide a standardized method for identifying underperforming assets.

## Key Features

### 1. Automated Data Mining
The system employs a keyword pattern matching algorithm to automatically detect "Production" or "Yield" columns within raw Excel files. This feature supports multi-language headers, ensuring compatibility with various SCADA export formats without manual intervention.

### 2. Satellite Irradiance Integration
The tool fetches real-time Global Horizontal Irradiance (GHI) data for specific geospatial coordinates using the Open-Meteo API. This allows for precise, location-based theoretical energy calculations.

### 3. Physics-Based Theoretical Modeling
Expected energy output is calculated using a physics engine that accounts for:
* Installed DC Capacity (kWp)
* Geometric Tilt Correction Factors (Seasonal adjustments for winter/summer incidence angles)
* System Loss Coefficients (Inverter efficiency, cabling, and soiling losses)

### 4. Data Sanitization and Quality Control
To ensure analytical accuracy, the system performs rigorous data cleaning:
* **De-duplication:** Removes duplicate daily logs using aggregation logic.
* **Unit Normalization:** Automatically detects and corrects unit mismatches (e.g., converting MWh to kWh).
* **Anomaly Rejection:** Filters out physically impossible data points (e.g., Performance Ratio > 100%) to prevent skewing of the final dataset.

### 5. Executive Reporting
The output includes a "Traffic-Light" classification system (Green/Yellow/Red) for rapid visual assessment and a detailed Excel audit report for in-depth analysis.

---

## Methodology

The core algorithm operates in five sequential stages:

1.  **Data Ingestion:** The script scans the directory for Excel files and identifies the target analysis period.
2.  **Sanitization:** The dataset is cleansed by aggregating daily sums and removing statistical outliers.
3.  **Irradiance Mapping:** The system queries satellite APIs for the exact latitude and longitude of each plant.
4.  **Performance Calculation:** The Performance Ratio (PR) is calculated using the following equation:

    PR = Actual Yield (kWh) / (Irradiance * Capacity * Tilt Factor * System Efficiency)

5.  **Audit Classification:** Plants are classified into performance tiers based on the calculated PR:
    * **Tier 1 (Excellent):** PR >= 85%
    * **Tier 2 (Standard):** 70% <= PR < 85%
    * **Tier 3 (Review Needed):** PR < 70%

---

## Installation and Usage

### Prerequisites
* Python 3.8 or higher
* Internet connection for API requests

### Installation

1. Clone the repository to your local machine.
2. Install the required Python dependencies:
   pip install pandas requests openpyxl matplotlib

### Configuration

Open the 'solar_analytics.py' script and locate the [MANUAL CONFIGURATION AREA]. You must populate the PLANTS list with your specific site data. The system requires the Plant ID, Excel filename, Capacity (kWp), and GPS coordinates.

### Execution

Run the analysis script via the terminal:
python solar_analytics.py

---

## Output Description

Upon successful execution, the tool generates two primary files in the root directory:

1.  **SOLAR_FLEET_AUDIT_REPORT.xlsx:** A comprehensive table containing daily production sums, theoretical expectations, and PR percentages for each plant.
2.  **Fleet_Performance_Chart.png:** A bar chart visualizing the comparative performance of the fleet, including threshold lines for KPI targets.

---

## Author
**İsmail Kutay Yılmaz**
