# DA321 — Datasets (`data/` folder)

This folder contains every dataset used in the course notebooks. All notebooks read
these files with **local relative paths** (e.g. `pd.read_csv("data/penguins.csv")`),
so once you have this folder no downloads or uploads are needed — everything runs
offline.

> All notebook data loads from this folder — no `files.upload()`, no Kaggle, no live URLs.

---

## Files in this folder

| File | Dataset | What it is | Key columns | Used for |
|---|---|---|---|---|
| `penguins.csv` | Palmer Penguins | 344 penguins across 3 species on 3 islands | id, species, island, bill_length_mm, bill_depth_mm, flipper_length_mm, body_mass_g, sex, year | Descriptive stats, distributions, box/violin/QQ plots, contingency & chi-square, correlation, PCA, factor analysis, ANOVA, MANOVA |
| `life_expectancy.csv` | WHO Life Expectancy | Country-year health & economic indicators | Country, Year, Status, Life expectancy, GDP, Schooling, … | Multiple-regression modeling |
| `mushrooms.csv` | UCI Mushroom | ~8,100 mushrooms, all categorical | class (edible/poisonous), cap-shape, odor, … | Classification (label-encoded) |
| `amazon_sales.csv` | Amazon Sales 2025 | Retail orders (250 rows) | Order ID, Date, Product, Category, Total Sales, Customer Name, Status | Weekly retail KPI dashboards |
| `healthcare_noshows.csv` | Medical appointment no-shows | ~110k appointments | ScheduledDay, AppointmentDay, Age, Showed_up, SMS_received, … | Binary classification (no-show prediction) |
| `synthetic_healthcare.csv` | Synthetic clinic operations | Appointment-level service records | Department, Service_Time(mins), Delay_Reason, Patient_Group, Satisfaction | One-way ANOVA, Kruskal–Wallis, Dunn post-hoc |
| `flights.csv` | Airline passengers | Monthly passenger totals 1949–1960 (144 rows) | year, month, passengers | Time-series descriptive statistics |
| `nightingale.csv` | Nightingale mortality | Crimean War monthly deaths, 1854–1856 (24 rows) | Month, Deaths from Diseases, Deaths from Wounds, Deaths from Other Causes | Polar / rose-diagram (coxcomb) visualization |
| `netflix_titles.csv` | Netflix catalog | ~7,800 Netflix titles | type, title, country, date_added, release_year, rating, listed_in | Categorical data handling, text/word cloud |
| `nyc_taxi_sample.parquet` | NYC Yellow Taxi (sample) | 100k sampled trips (full source is multi-GB) | tpep_pickup_datetime, trip_distance, fare_amount, total_amount, payment_type | Large-scale scatter/bubble/parallel-coordinates plots |
| `us-states.json` | US state boundaries | GeoJSON polygons of US states (52 features) | geometry, `properties.name` | Choropleth map |
| `dem/N22E113.hgt`, `dem/N22E114.hgt` | SRTM elevation (Hong Kong) | SRTMGL1 1-arc-second tiles (3601×3601) | (raster grid) | 3D terrain / raster visualization |

All datasets are now present in `data/` — the notebook runs fully offline after cloning.

---

## Sources & licenses
- **Palmer Penguins** — Horst, Hill & Gorman (2020), CC0. https://allisonhorst.github.io/palmerpenguins/
- **WHO Life Expectancy** — WHO / Kaggle, open data.
- **UCI Mushroom** — UCI Machine Learning Repository, open.
- **Amazon Sales 2025** — Kaggle retail sample, educational use.
- **Medical appointment no-shows** — Kaggle `JoniHoppen/...` (KaggleV2), open data.
- **Synthetic clinic dataset** — course-authored synthetic data (no privacy concerns).
- **flights** — classic AirPassengers series, public domain.
- **Nightingale** — Florence Nightingale (1858), public domain historical data.
- **Netflix titles** — Kaggle `shivamb/netflix-shows`, CC0.
- **NYC Yellow Taxi** — NYC TLC open data (public domain); redistributed as a small sample.
- **SRTM DEM** — NASA/USGS, public domain.
- **US states GeoJSON** — PublicaMundi MappingAPI, open.

Data is included here **for coursework use only**. Refer to each source for full terms.
