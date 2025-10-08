# GBM Hydrological Discharge Processing Workflow (Harvard Dataverse)

***

## 🤝 Project Overview & Expertise

This repository showcases an advanced, end-to-end Python workflow designed for the **Ganges-Brahmaputra-Meghna (GBM) Basin**. The project demonstrates proficiency in seamlessly integrating large-scale geospatial data analysis with hydrological modeling techniques.

The primary objective is to process raw model outputs (e.g., global reanalysis) and observed discharge time-series data, harmonize them to a common time step (monthly), and perform a rigorous **Model Performance Evaluation** across **over 400 subbasins**.

### 🛠️ Key Expertise Showcased

| Domain | Skill Focus | Tools & Libraries |
| :--- | :--- | :--- |
| **Data Acquisition** | Automated, resilient file retrieval and parsing of public repository metadata. | `requests`, `urllib3`, `tqdm` |
| **High-Performance GIS** | **Parallel Processing** (multi-core) for efficient extraction of time-series data from large-volume **NetCDF** raster grids. | `xarray`, `netCDF4`, `multiprocessing` |
| **Hydrological Analysis** | Time-series aggregation, data quality control, and standard model performance calculation (NSE, PBIAS, R²). | `pandas`, `numpy`, Custom Metrics |
| **Reporting & Viz** | Generating publication-quality plots (Flow Duration Curves) and structured Excel evaluation reports. | `matplotlib`, `xlsxwriter` |

---

## ⚙️ Sequential Workflow and Data Flow

The project is structured as a clear, sequential pipeline. The notebooks must be executed in numeric order, with the output of one step serving as the input for the next.

| ID | Notebook Name | Input Data | Output Data |
| :--- | :--- | :--- | :--- |
| **1** | `1_Download_discharge_data.ipynb` | **Dataverse DOI** (Config) | **Raw NetCDF Files** (Yearly Discharge Grids) saved to local directory. |
| **2.0** | `2_Daily_data_extraction_from_NETCDF_singlecore_all_subbasins_outlets.ipynb` | *(Alternative: Single-Core Extraction)* | *(Included for completeness, **I used this one personally.**)* |
| **2.1** | `2_1_Daily_data_extraction_from_NETCDF_multicore_all_subbasins_outlets.ipynb` **(Recommended for Production)** | **Raw NetCDF Files** (from Step 1) & **`Outlets_subbasin.csv`** (415+ coordinates) | **Merged Daily Discharge Time-Series** (CSV/TSV file containing daily flow for all 415 subbasins). |
| **3** | `3_Observed_discharge_daily_to_monthly_all_subbasins.ipynb` | Multiple **Observed Daily Discharge CSV files** (one per subbasin). | Multiple **Observed Monthly Discharge CSV files** (aggregated using a chosen method like `mean`). |
| **4** | `4_Simulated_monthly_discharge_all_subbasins_SWAT.ipynb` | Single **Simulated Monthly Discharge Excel/CSV file** (from SWAT or similar model). | **Cleaned & Standardized Simulated Monthly Discharge CSV/Excel** (ready for comparison). |
| **5** | `5_Model_performance_evaluation_all_subbasins.ipynb` | **Observed Monthly Files** (from Step 3) & **Simulated Monthly File** (from Step 4). | **Comprehensive Excel Report** (`.xlsx`) detailing model metrics (NSE, PBIAS, R²) for all subbasins across multiple evaluation periods. |
| **6** | `6_Plots_flow_duration_curves_pdfs_all_subbasins.ipynb` | **Merged Observation/Simulation Time-Series** (the data source for Step 5's metrics). | **Individual PDF Reports** (one per subbasin) containing Flow Duration Curves and Seasonal Hydrographs, saved to an output folder. |

---

## ⚠️ Development Philosophy & AI Acknowledgment

**I am the primary maintainer and integrator of this project.** This workflow is a testament to my advanced capability in fine-tuning complex **Python workflows for geospatial and hydrological analysis**.

The foundational logic and many specific code snippets were developed transparently using respected web resources and **Large Language Models (LLMs)**, including **Gemini, ChatGPT, Claude, and Copilot**. This approach demonstrates my skill in orchestrating open-source libraries and leveraging AI to build a robust, production-ready scientific pipeline.

---

## 💾 Setup and Dependencies

This project requires a standard Python environment (≥ 3.10).

### 1. Installation

```bash
# Clone the repository
git clone https://github.com/srijondatta1/GBM_Discharge_processing_from_Harvard_Dataverse.git
cd GBM_Discharge_processing_from_Harvard_Dataverse

# Install all necessary packages (recommended inside a virtual environment)
pip install -r requirements.txt
