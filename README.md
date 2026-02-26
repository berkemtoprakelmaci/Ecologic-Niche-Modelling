# 🌴 Present and Future Distribution Projections of *Phoenix theophrasti* Greuter (Cretan Date Palm)

**Author:** Berkem Toprak Elmacı

## Overview

This project models the **current and future distribution** of *Phoenix theophrasti* Greuter (Cretan date palm / Datça palmiyesi) using Ecological Niche Modeling (ENM) with the `biomod2` package in R. The species is an endemic palm native to the eastern Mediterranean — found in Greece (Crete) and Turkey (Datça peninsula).

Future projections are generated for two **SSP scenarios** (SSP126 and SSP585) and two **time periods** (2021–2040 and 2041–2060).

---

## 📁 Repository Structure

```
├── Cretan_date_palm_Berkem_Toprak_Elmaci.Rmd   # Main R Markdown analysis file
├── Cretan_date_palm_Berkem_Toprak_Elmaci.html  # Rendered HTML report
├── occurence_data.csv                           # GBIF occurrence data (tab-separated)
├── wc2.1_2.5m_bio_1.tif                        # WorldClim BIO1 - Annual Mean Temperature
├── wc2.1_2.5m_bio_2.tif                        # WorldClim BIO2 - Mean Diurnal Range
├── wc2.1_2.5m_bio_3.tif                        # WorldClim BIO3 - Isothermality
├── wc2.1_2.5m_bio_12.tif                       # WorldClim BIO12 - Annual Precipitation
├── wc2.1_2.5m_bio_14.tif                       # WorldClim BIO14 - Precipitation of Driest Month
└── README.md
```

> **Note:** Raster files (`.tif`) and occurrence CSV are not tracked by Git due to file size. Download instructions are provided below.

---

## 🔧 Requirements

### R Packages

```r
install.packages(c("biomod2", "raster", "dismo", "sp", "dplyr", "maxnet"))
```

| Package  | Purpose |
|----------|---------|
| `biomod2` | Ensemble species distribution modeling |
| `raster`  | Raster data handling |
| `dismo`   | Species distribution modeling tools |
| `sp`      | Spatial data classes |
| `dplyr`   | Data manipulation |
| `maxnet`  | MaxEnt implementation |

---

## 📦 Data Sources

### Occurrence Data
- Downloaded from [GBIF](https://www.gbif.org/) — 129 occurrence records for *Phoenix theophrasti* Greuter
- 19 records in Turkey, remainder in Greece (Crete)

### Bioclimatic Variables
- **Present:** [WorldClim v2.1](https://www.worldclim.org/data/worldclim21.html) — 2.5 min resolution
- **Future:** [WorldClim CMIP6](https://www.worldclim.org/data/cmip6/cmip6_clim5m.html) — 2.5 min resolution
  - Model: **ACCESS-CM2**
  - Scenarios: **SSP126** (sustainable) and **SSP585** (high emission)
  - Periods: **2021–2040** and **2041–2060**

Selected bioclimatic variables: BIO1, BIO2, BIO3, BIO12, BIO14

---

## 🧪 Methods

1. **Data Acquisition** — Occurrence records from GBIF; bioclimatic rasters from WorldClim
2. **Data Formatting** — `BIOMOD_FormatingData()` with 3,000 pseudo-absences (random strategy, 3 replicates)
3. **Modeling** — Three algorithms: **MaxNet**, **GAM**, **CTA**
4. **Projection** — Current + 4 future scenarios (2 SSPs × 2 time periods), cropped to Turkey/Aegean region
5. **Ensemble Modeling** — `BIOMOD_EnsembleModeling()` + `BIOMOD_EnsembleForecasting()`

---

## 📊 Key Results

- Current distribution is concentrated along **Aegean and Mediterranean coasts**
- Under **SSP126**, the species shows potential range expansion into Mesopotamia
- Under **SSP585**, distribution remains restricted to core coastal habitats
- Ensemble models consistently identify Aegean coast as a critical habitat

---

## ▶️ How to Run

1. Clone this repository
2. Download the required raster `.tif` files from WorldClim (links above) and place them in the project root
3. Download occurrence data from GBIF and save as `occurence_data.csv` (tab-separated)
4. Update working directory paths in the `.Rmd` file if needed, or use RStudio's **Knit** button

```r
rmarkdown::render("Cretan_date_palm_Berkem_Toprak_Elmaci.Rmd")
```

---

## 📚 References

- García-Granero et al. (2020). *Journal of Ethnobiology*, 40(1): 101–114.
- Örücü, Ö. K. (2019). *Turkish Journal of Forestry*, 20(3), 274–283.
- Phillips, S. J. et al. (2006). *Ecological Modelling*, 190(3-4), 231–259.
- O'Neill, B. C. et al. (2014). *Climatic Change*, 122, 387–400.
- Meinshausen, M. et al. (2020). *Geoscientific Model Development*, 13(8), 3571–3605.

---

## 📄 License

This project is for academic purposes. Please cite the original data sources (GBIF, WorldClim) if you reuse any data.
