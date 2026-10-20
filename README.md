# str-density-colombia
This repository contains the replication data and R code for a multilevel analysis of short-term rental (STR) density and long-term rents in 18 Colombian cities in 2025. Using dwelling-level and city-level characteristics, the study draws on 6.803 web-scraped rental listings nested within 18 cities to examine the association between STR activity and long-term rental prices.

The repository is organized as follows. Each box is a folder, and the arrows show how the scripts turn the raw data into the results of the paper.

```mermaid
flowchart TB
  subgraph raw["data/raw"]
    A["120226_*_<br/>scraper_data.RDS"]
    B["raw-2nd-lvl-<br/>variables.xlsx"]
  end

  subgraph prep["prep-data"]
    S1["01_scrape_<br/>listings.R"]
    S2["02_build_<br/>city_level.R"]
    S3["03_prepare_<br/>input.R"]
    S4["04_housing_<br/>density.R"]
  end

  subgraph clean["data/clean"]
    C["clean_2ndlevel_<br/>data.xlsx"]
    D["100226_multilevel_<br/>final_dataset.xlsx"]
  end

  subgraph spatial["spatial-data"]
    L["Spatial layers"]
    M["Municipality maps"]
  end

  subgraph models["multilevel-models"]
    S5["05_estimation_<br/>sample.R"]
    S6["06_null_<br/>model.R"]
    S7["07_random_<br/>intercept_slope.R"]
    S8["08_cross_<br/>level.R"]
    F["model_<br/>functions.R"]
  end

  S1 --> A
  B --> S2 --> C
  A --> S3
  C --> S3 --> D
  D --> S4
  L --> S4 --> M
  D --> S5 --> S6 & S7 & S8
  F -.-> S6 & S7 & S8
```
