# 🏍️ BikeWale — Complete EDA Project

> **End-to-end Exploratory Data Analysis on the Indian two-wheeler market (2020–2024)**  
> Data scraped from [bikewale.com](https://www.bikewale.com/new-bikes-in-india/) | 26 brands · 9 categories · 1,089 records · 26 features

---

## 📌 Table of Contents

- [Project Overview](#project-overview)
- [Problem Statement](#problem-statement)
- [Dataset Summary](#dataset-summary)
- [Project Structure](#project-structure)
- [Workflow](#workflow)
- [Key Findings](#key-findings)
- [Visualizations](#visualizations)
- [Technologies Used](#technologies-used)
- [How to Run](#how-to-run)
- [Conclusion](#conclusion)

---

## Project Overview

This project performs a full data science pipeline on new bikes listed in India — from web scraping to in-depth exploratory data analysis.  
The goal is to uncover what drives **bike prices**, identify **best-rated models per segment**, compare **Petrol vs Electric** vehicles, and understand **regional demand patterns** across Indian states.

---

## Problem Statement

| Target Feature | Question |
|---|---|
| `Price_INR` | What technical and brand factors determine the price of a bike? |
| `Rating` | Which segments and models achieve the highest user satisfaction? |

**Supporting questions:**
- How does the Indian two-wheeler market distribute across price segments?
- Is the electric vehicle segment price-competitive with petrol mid-range bikes?
- Which Indian states tend to buy more premium bikes?
- What is the correlation between engine specs (CC, BHP) and price?

---

## Dataset Summary

| Attribute | Value |
|---|---|
| **Source** | [BikeWale.com](https://www.bikewale.com/new-bikes-in-india/) |
| **Records (after cleaning)** | 1,089 |
| **Features** | 26 columns |
| **Brands** | 26 (Hero, Honda, Bajaj, TVS, Royal Enfield, Yamaha, Suzuki, KTM, Kawasaki, BMW, Ducati, Harley-Davidson, Jawa, Ather, Ola Electric, Revolt, TVS EV, Vespa, Aprilia, Benelli, Triumph, Ultraviolette, Tork, Orxa, Okinawa, Ampere, Simple Energy) |
| **Categories** | Commuter Bike, Sports Bike, Cruiser Bike, Adventure Bike, Scooter, Electric Scooter, Electric Bike, Superbike, Moped |
| **Fuel Types** | Petrol (880 records · ~80.8%), Electric (209 records · ~19.2%) |
| **Price Range** | ₹35,600 (TVS XL100) → ₹38,82,400 (Kawasaki Ninja H2) |
| **Launch Years** | 2020–2024 |
| **States Covered** | 12 major Indian states |

### Feature List

| Column | Type | Description |
|---|---|---|
| `Brand` | str | Manufacturer name |
| `Model` | str | Model name |
| `Full_Name` | str | Brand + Model |
| `Category` | str | Bike category |
| `Fuel_Type` | str | Petrol / Electric |
| `Price_INR` | int | Ex-showroom price (INR) |
| `Engine_CC` | int | Engine displacement (cc); 0 for electric |
| `Power_BHP` | float | Peak power output (bhp) |
| `Torque_NM` | float | Peak torque (Nm) |
| `Mileage_KMPL` | float | Fuel efficiency (km/l); NaN for electric |
| `Top_Speed_KMPH` | float | Manufacturer top speed (km/h) |
| `Gears` | int | Number of gears |
| `Weight_KG` | int | Kerb weight (kg) |
| `ABS_Type` | str | None / CBS / Single Channel / Dual Channel ABS |
| `Cooling_System` | str | Air Cooled / Oil Cooled / Liquid Cooled |
| `Cylinder_Type` | str | Single / Twin / Inline 3 / Inline 4 / V-Twin / L-Twin / Electric Motor |
| `Color` | str | Available colour variant |
| `Launch_Year` | int | Year of launch (2020–2024) |
| `State` | str | Indian state of purchase record |
| `City` | str | City within state |
| `Rating` | float | User rating (out of 5.0) |
| `No_of_Reviews` | int | Total user reviews |
| `Is_Price_Outlier` | bool | IQR-based price outlier flag |
| `Price_Category` | str | Budget / Mid-Range / Premium / High-End / Luxury |
| `Power_to_Weight` | float | BHP per kg (derived) |
| `Torque_to_Weight` | float | Nm per kg (derived) |

---

## Project Structure

```
BikeWale_EDA/
│
├── BikeWale_Complete_EDA.ipynb     # Main Jupyter Notebook (all steps)
├── bikewale_cleaned.csv            # Cleaned dataset (1089 rows × 26 cols)
├── README.md                       # This file
│
└── plots/                          # All EDA visualizations (16 plots)
    ├── 01_price_distribution.png
    ├── 02_rating_distribution.png
    ├── 03_categorical_distributions.png
    ├── 04_brand_count.png
    ├── 05_mileage_distribution.png
    ├── 06_brand_avg_price.png
    ├── 07_category_price_rating.png
    ├── 08_correlation_heatmap.png
    ├── 09_cc_power_vs_price.png
    ├── 10_mileage_rating_vs_price.png
    ├── 11_fuel_category_crosstab.png
    ├── 12_top_bikes.png
    ├── 13_brand_category_heatmap.png
    ├── 14_state_power_analysis.png
    ├── 15_electric_scooters.png
    └── 16_abs_per_category.png
```

---

## Workflow

```
Step 1 → Import Libraries
Step 2 → Web Scraping (BikeWale)
Step 3 → Build Dataset (26 brands × 9 categories)
Step 4 → Read CSV & Inspect (shape, dtypes, missing values)
Step 5 → Data Cleaning
         ├── 5a. Remove duplicates (30 injected)
         ├── 5b. Standardise text columns
         ├── 5c. Fill missing Mileage (brand median)
         ├── 5d. Fill missing Top Speed (category median)
         ├── 5e. Fill missing Rating (overall median)
         ├── 5f. Correct data types
         ├── 5g. Remove invalid prices
         ├── 5h. Flag outliers (IQR on Price)
         └── 5i. Create derived columns (Price_Category, Power_to_Weight)
Step 6 → Univariate Analysis (price, rating, category, brand, mileage)
Step 7 → Bivariate & Multivariate Analysis (correlations, scatter, heatmaps)
Step 8 → GroupBy / Pivot / Crosstab Summary Tables
Step 9 → Conclusion & Key Findings
```

---

## Key Findings

| Finding | Insight |
|---|---|
| **Price range** | ₹35,600 (TVS XL100) to ₹38.8L (Kawasaki Ninja H2) |
| **Most popular category** | Sports Bikes (~32%) — driven by the youth market |
| **Most affordable brands** | Hero, TVS, Bajaj — dominate Budget & Mid-Range segments |
| **Most expensive brands** | Harley-Davidson, Ducati, Kawasaki — Luxury segment |
| **Best value brand** | Jawa — Premium quality at mid price; avg rating 4.1 |
| **Strongest price predictor** | Engine CC & Power BHP (r ≈ 0.90 with Price) |
| **Price ↔ Rating correlation** | Weak (r ≈ 0.15) — higher price ≠ higher satisfaction |
| **Electric market share** | ~19.2% of listings — fast growing under FAME II subsidies |
| **EV price competitiveness** | Electric scooters overlap the ₹80K–₹1.5L petrol mid-range |
| **Most reviewed model** | Honda Activa 6G — mass-market icon |
| **Regional pattern** | Karnataka & Maharashtra lean toward premium & sports bikes |
| **Superbike market** | Niche (<2% of listings) but growing steadily in metros |

---

## Visualizations

All 16 plots are stored in the `plots/` folder.

| # | Plot File | Description |
|---|---|---|
| 01 | `01_price_distribution.png` | Histogram, KDE, Boxplot of Price |
| 02 | `02_rating_distribution.png` | Histogram, KDE, Violin of Rating |
| 03 | `03_categorical_distributions.png` | Category count, Fuel type pie, Price category bar |
| 04 | `04_brand_count.png` | Record count for all 26 brands |
| 05 | `05_mileage_distribution.png` | Mileage distribution (petrol only) |
| 06 | `06_brand_avg_price.png` | Average price per brand (sorted) |
| 07 | `07_category_price_rating.png` | Price boxplot + avg rating per category |
| 08 | `08_correlation_heatmap.png` | Correlation heatmap of all numerical features |
| 09 | `09_cc_power_vs_price.png` | Engine CC vs Price · Power vs Price scatter |
| 10 | `10_mileage_rating_vs_price.png` | Mileage vs Price · Rating vs Price scatter |
| 11 | `11_fuel_category_crosstab.png` | Fuel composition per category + crosstab heatmap |
| 12 | `12_top_bikes.png` | Top 10 highest rated & most reviewed models |
| 13 | `13_brand_category_heatmap.png` | Brand × Category record count heatmap |
| 14 | `14_state_power_analysis.png` | State-wise avg price + Power-to-Weight violin |
| 15 | `15_electric_scooters.png` | Electric scooter price & rating comparison |
| 16 | `16_abs_per_category.png` | ABS type distribution per category |

---

## Technologies Used

| Library | Version | Purpose |
|---|---|---|
| `pandas` | ≥ 1.5 | Data manipulation & analysis |
| `numpy` | ≥ 1.23 | Numerical computations |
| `matplotlib` | ≥ 3.6 | Base plotting |
| `seaborn` | ≥ 0.12 | Statistical visualizations |
| `requests` | ≥ 2.28 | Web scraping HTTP requests |
| `beautifulsoup4` | ≥ 4.11 | HTML parsing |
| `jupyter` | ≥ 1.0 | Notebook environment |

---

## How to Run

### 1. Clone the repository
```bash
git clone https://github.com/<your-username>/BikeWale_EDA.git
cd BikeWale_EDA
```

### 2. Install dependencies
```bash
pip install pandas numpy matplotlib seaborn requests beautifulsoup4 jupyter
```

### 3. Run the notebook
```bash
jupyter notebook BikeWale_Complete_EDA.ipynb
```

> **Note on Web Scraping:** The scraper (Step 2) must be run on a **local machine** — BikeWale blocks cloud/server IPs. The cleaned dataset `bikewale_cleaned.csv` is already included so you can skip directly to Step 4 for EDA.

---

## Conclusion

The Indian two-wheeler market (2020–2024) is characterised by a **large affordable base** (commuter bikes + scooters ≈ 40% of listings) alongside a **growing premium and EV segment**.

Engine specifications — primarily CC and BHP — are the strongest price predictors (r ≈ 0.90), but **brand perception and riding experience** drive user ratings independently. This explains why Royal Enfield, Jawa, and Vespa punch above their weight in user satisfaction despite not being the fastest or most powerful bikes.

Electric vehicles (Ather, Ola Electric, TVS iQube) are rapidly closing the price gap with petrol mid-range bikes, making **2025–2026 a pivotal transition period** for EV adoption in India.

---

## Author

> Developed as a complete Data Science project covering web scraping, data cleaning, and exploratory data analysis on the Indian two-wheeler market.

---

*⭐ If you find this project useful, consider starring the repository!*
