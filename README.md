# str-density-colombia
This repository contains the replication data and R code for a multilevel analysis of short-term rental (STR) density and long-term rents in 18 Colombian cities in 2025. Using dwelling-level and city-level characteristics, the study draws on 6.803 web-scraped rental listings nested within 18 cities to examine the association between STR activity and long-term rental prices.

The repository is organized as follows. Each box is a folder, and the arrows show how the scripts turn the raw data into the results of the paper.

```mermaid
flowchart TB
  subgraph raw["data/raw"]
    A["120226_*_scraper_data.RDS"]
    B["raw-2nd-lvl-variables.xlsx"]
  end

  subgraph prep["prep-data"]
    S1["01_scrape_listings.R"]
    S2["02_build_city_level.R"]
    S3["03_prepare_input.R"]
    S4["04_housing_density.R"]
  end

  subgraph clean["data/clean"]
    C["clean_2ndlevel_data.xlsx"]
    D["100226_multilevel_final_dataset.xlsx"]
  end

  subgraph spatial["spatial-data"]
    L["Spatial layers"]
    M["Municipality maps (Figure 1)"]
  end

  subgraph models["multilevel-models"]
    S5["05_estimation_sample.R"]
    S6["06_null_model.R"]
    S7["07_random_intercept_slope.R"]
    S8["08_cross_level.R"]
    F["model_functions.R"]
  end

  subgraph out["output"]
    E["estimation_sample.rds"]
    T3["Table 3"]
    T4["Table 4"]
    T5["Table 5"]
  end

  S1 --> A
  B --> S2 --> C
  A --> S3
  C --> S3 --> D
  D --> S4
  L --> S4 --> M
  D --> S5 --> E
  E --> S6 & S7 & S8
  F -.-> S6 & S7 & S8
  S6 --> T3
  S7 --> T4
  S8 --> T5
```
