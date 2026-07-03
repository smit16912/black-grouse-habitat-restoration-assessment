# Black Grouse 2030: Ecological Restoration and Multi-Objective Land-Use Assessment

## Project overview

This Python/Jupyter project evaluates historical land-use change and alternative 2030 habitat-restoration strategies for Black Grouse habitat in and around Sallandse Heuvelrug National Park, the Netherlands.

The project combines:

- historical land-use change;
- habitat amount, fragmentation, and connectivity;
- spatially explicit restoration allocation;
- agricultural opportunity costs;
- population accessibility and recreation;
- recreation–conservation disturbance exposure;
- multi-objective scenario ranking under alternative policy priorities.

The ecological study area consists of the national park and a 5 km surrounding buffer, covering **762.88 km²**. A larger social-analysis extent was created by adding a further 10 km buffer around the ecological study area.

## Central analytical message

Core-habitat area increased substantially between 1990 and 2024, but patch number and edge density also increased.

> An increase in habitat amount does not necessarily represent an improvement in habitat-network integrity.

The four equal-area restoration scenarios further demonstrate that spatial configuration strongly affects ecological outcomes. When agricultural opportunity costs, social accessibility, and disturbance exposure are included, the ecologically strongest strategy is not automatically the strongest under every policy objective.

## Research questions

1. How did land-use composition change between 1990, 2012, and 2024?
2. How did core-habitat amount, patch configuration, and fragmentation change during this period?
3. How do equal-area 2030 restoration strategies differ in habitat configuration and connectivity?
4. How much registered agricultural land and annual agricultural Standard Output would each strategy displace?
5. How do the scenarios differ in potential population access, proximity to recreation infrastructure, and disturbance exposure?
6. Which scenarios perform best under nature-priority, multifunctional, and production-oriented policy contexts?
7. How robust are the scenario rankings when policy weights change?

## Study area

The ecological analysis covers Sallandse Heuvelrug National Park and a 5 km buffer.

- National park area: **252.99 km²**
- Total ecological study area: **762.88 km²**
- Coordinate reference system: **EPSG:28992**
- Ecological analysis resolution: **25 m**
- Social analysis: additional **10 km extension** around the ecological study area

## Input datasets

### Land use and habitat

- **1990:** HGN1990
- **2012:** LGN7
- **2024:** LGN2024

### Agricultural opportunity costs

- **BRP Gewaspercelen 2024 Definitief**
- Crop-specific and proxy **Standard Output 2020** coefficients

### Social accessibility and recreation

- **CBS Vierkantstatistieken 100 m, 2024**
- **TOP10NL Wegdeel lijn**
- **TOP10NL Wegdeel vlak**

All datasets were transformed to or analysed in **EPSG:28992**.

## Harmonised land-use classification

The original HGN and LGN classes were harmonised into five common categories:

| Value | Harmonised class |
|---:|---|
| 1 | Agricultural matrix |
| 2 | Core habitat |
| 3 | Forest |
| 4 | Urban and infrastructure |
| 5 | Water |

All three land-use datasets were aligned to the same 25 m raster grid and masked to an identical ecological-analysis extent.

## Workflow

| Notebook | Purpose |
|---|---|
| `01_setup_and_inspect_data.ipynb` | Inspect inputs and create the 5 km ecological study-area buffer |
| `02_harmonise_landuse.ipynb` | Clip, align, reclassify, mask, and validate land-use rasters |
| `03_observed_landuse_change.ipynb` | Analyse land-use transitions and core-habitat persistence, gains, and losses |
| `04_landscape_metrics.ipynb` | Calculate habitat amount and fragmentation metrics |
| `05_restoration_suitability.ipynb` | Calculate restoration-suitability variables |
| `06_simulate_2030_scenarios.ipynb` | Simulate four equal-area restoration scenarios |
| `07_connectivity_analysis.ipynb` | Compare habitat-network connectivity across gap distances |
| `08_compare_scenarios.ipynb` | Combine landscape, connectivity, and suitability indicators |
| `09_create_figures.ipynb` | Produce ecological portfolio figures |
| `10_economic_opportunity_costs.ipynb` | Estimate affected crop areas and agricultural Standard Output displaced |
| `11_social_access_and_recreation.ipynb` | Evaluate population access, recreation-network proximity, and disturbance exposure |
| `12_multiobjective_assessment.ipynb` | Integrate ecological, economic, social, and disturbance indicators |

---

## Part I: Historical landscape change and ecological restoration

## Observed land-use change

Core-habitat area increased throughout the study period:

| Year | Core-habitat area | Percentage of study area |
|---:|---:|---:|
| 1990 | 21.51 km² | 2.82% |
| 2012 | 42.75 km² | 5.60% |
| 2024 | 54.41 km² | 7.13% |

Between 1990 and 2024:

- Core-habitat area increased by **32.90 km²**
- Agricultural matrix decreased by **78.24 km²**
- Urban and infrastructure increased by **52.40 km²**
- Forest decreased by **13.67 km²**

Of the 1990 core habitat:

- **17.44 km²** persisted until 2024
- **4.07 km²** was lost
- **36.97 km²** of new core habitat was identified in 2024

## Observed fragmentation

Although core-habitat area increased, habitat configuration became more fragmented.

| Metric | 1990 | 2012 | 2024 |
|---|---:|---:|---:|
| Core-habitat area | 21.512 km² | 42.752 km² | 54.408 km² |
| Number of patches | 701 | 1,351 | 2,570 |
| Mean patch area | 0.0307 km² | 0.0316 km² | 0.0212 km² |
| Largest patch area | 6.597 km² | 11.136 km² | 13.093 km² |
| Edge density | 5.747 m/ha | 12.829 m/ha | 19.632 m/ha |

From 1990 to 2024:

- Core-habitat area increased by **152.92%**
- Patch number increased by **266.62%**
- Mean patch area decreased by **30.94%**
- Edge density increased by **241.60%**

The results indicate that habitat expansion occurred together with increasing subdivision and edge exposure.

## Restoration suitability

Restoration candidates were restricted to agricultural-matrix pixels in the 2024 land-use raster.

The suitability analysis included:

- proximity to existing core habitat;
- distance from urban and infrastructure;
- surrounding core-habitat proportion within 1 km;
- surrounding urban proportion within 1 km.

The four components were standardised from 0 to 1 and combined using equal weights.

## 2030 restoration scenarios

Each scenario restored exactly:

- **18,649 pixels**
- **11.656 km²**

All four scenarios therefore contain the same total 2030 core-habitat area:

- **66.063 km²**

### Dispersed restoration

Restoration pixels were selected randomly across the eligible agricultural matrix. This represents spatially uncoordinated restoration.

### Patch enlargement

Pixels close to existing core habitat were prioritised. This represents restoration around existing habitat boundaries.

### Connectivity-focused restoration

Candidate pixels within potential gaps between existing habitat patches were prioritised. This represents restoration intended to strengthen habitat-network links.

### Integrated low-matrix-pressure restoration

Pixels were prioritised using the combined restoration-suitability score. This strategy balances proximity to core habitat, surrounding habitat amount, distance from urban areas, and low surrounding urban pressure.

## Ecological scenario comparison

| Scenario | Patches | Mean patch area | Largest patch | Edge density |
|---|---:|---:|---:|---:|
| Baseline 2024 | 2,570 | 0.0212 km² | 13.093 km² | 19.632 m/ha |
| Dispersed | 19,058 | 0.0035 km² | 13.101 km² | 43.210 m/ha |
| Patch enlargement | 2,290 | 0.0288 km² | 13.418 km² | 23.461 m/ha |
| Connectivity focused | 2,546 | 0.0259 km² | 14.749 km² | 21.411 m/ha |
| Integrated | 2,574 | 0.0257 km² | 13.878 km² | 21.820 m/ha |

- **Dispersed restoration** produces the greatest fragmentation and edge exposure.
- **Patch enlargement** produces the fewest patches and largest mean patch area.
- **Connectivity-focused restoration** produces the largest individual habitat patch and strongest intermediate-distance network structure among the structured strategies.
- **Integrated restoration** produces the highest mean suitability and greatest mean distance from urban and infrastructure.

Connectivity was assessed using maximum gap distances of **0, 100, 250, 500, and 1,000 m**.

---

## Part II: Socio-economic and multi-objective assessment

## Agricultural opportunity costs

The four restoration masks were intersected with BRP 2024 agricultural parcels. The analysis calculated affected area by crop type and estimated annual agricultural Standard Output displaced.

| Rank: lowest cost | Scenario | BRP coverage | Annual output displaced | Output displaced per restored ha |
|---:|---|---:|---:|---:|
| 1 | Patch enlargement | 77.75% | €1,569,796.56 | €1,346.81/ha |
| 2 | Dispersed | 87.68% | €1,847,400.57 | €1,584.99/ha |
| 3 | Integrated | 92.32% | €2,246,921.42 | €1,927.76/ha |
| 4 | Connectivity focused | 84.87% | €2,252,302.79 | €1,932.37/ha |

**Patch enlargement** has the lowest estimated agricultural opportunity cost. **Connectivity-focused restoration** has the highest, although the integrated strategy is almost equally costly.

![Agricultural opportunity costs](outputs/figures/scenario_agricultural_opportunity_costs.png)

## Population accessibility and recreation

CBS 100 m population cells were used to estimate the number of residents living within 2, 5, and 10 km of restored pixels. TOP10NL walking and cycling infrastructure was used to calculate restoration proximity to recreation networks.

| Scenario | Population within 5 km | Restoration within 500 m of recreation network | Restoration within 250 m of recreation network |
|---|---:|---:|---:|
| Dispersed | 328,588 | 65.94% | 35.66% |
| Patch enlargement | 310,671 | 77.90% | 48.20% |
| Connectivity focused | 178,859 | 79.04% | 44.59% |
| Integrated | 232,153 | 76.52% | 41.87% |

Interpretation:

- **Dispersed restoration** reaches the largest nearby population and has the lowest close-range recreation exposure.
- **Patch enlargement** combines high population access with strong recreation-network proximity, but also has the highest potential disturbance exposure.
- **Connectivity-focused restoration** has the greatest share of restored land within 500 m of recreation infrastructure, but reaches the smallest population.
- **Integrated restoration** occupies an intermediate position.

These indicators represent **potential accessibility and disturbance exposure**, not confirmed public access or observed visitor pressure.

![Social access and disturbance trade-off](outputs/figures/scenario_social_access_disturbance_tradeoff.png)

## Dimension scores

Indicators were standardised from 0 to 1 so that higher scores consistently represent better performance.

| Scenario | Ecological | Economic | Social access | Low disturbance |
|---|---:|---:|---:|---:|
| Dispersed | 0.2500 | 0.5933 | 0.5000 | 1.0000 |
| Patch enlargement | 0.6163 | 1.0000 | 0.8967 | 0.0000 |
| Connectivity focused | 0.7258 | 0.0000 | 0.5000 | 0.2879 |
| Integrated | 0.7456 | 0.0079 | 0.5818 | 0.5048 |

## Policy-context rankings

| Scenario | Nature priority | Multifunctional | Production oriented |
|---|---:|---:|---:|
| Connectivity focused | 3 | 4 | 4 |
| Dispersed | 4 | 2 | 2 |
| Integrated | 1 | 3 | 3 |
| Patch enlargement | 2 | 1 | 1 |

- **Integrated restoration** ranks first under a nature-priority context.
- **Patch enlargement** ranks first under multifunctional and production-oriented priorities.
- **Dispersed restoration** ranks second under multifunctional and production-oriented priorities.
- **Connectivity-focused restoration** performs strongly ecologically but is constrained by high agricultural opportunity cost.

![Policy-context comparison](outputs/figures/scenario_policy_context_comparison.png)

## Weight-sensitivity analysis

Scenario robustness was evaluated using **10,000 random policy-weight combinations**.

| Scenario | First-place frequency | Mean simulated rank | Top-two frequency |
|---|---:|---:|---:|
| Patch enlargement | 57.20% | 1.78 | 76.09% |
| Dispersed | 34.44% | 2.08 | 74.47% |
| Integrated | 8.36% | 2.46 | 46.06% |
| Connectivity focused | 0.00% | 3.68 | 3.38% |

**Patch enlargement** is the most robust overall strategy across changing policy weights. **Integrated restoration** becomes preferred when ecological performance receives dominant weight. **Connectivity-focused restoration** does not rank first because its ecological gains are offset by its economic and social-access performance in the selected multi-objective framework.

![Weight-sensitivity analysis](outputs/figures/scenario_weight_sensitivity.png)

## Main conclusion

The project demonstrates that habitat-restoration planning cannot be evaluated using habitat area alone.

Historical habitat expansion occurred together with increasing fragmentation. The equal-area 2030 scenarios also produced substantially different habitat configurations, agricultural opportunity costs, accessibility benefits, and disturbance exposure.

The preferred strategy depends on policy priorities:

- **Integrated restoration** performs best under nature-priority weighting.
- **Patch enlargement** is the strongest multifunctional and production-oriented strategy and is the most robust across random weight combinations.
- **Dispersed restoration** provides high population accessibility and low close-range recreation exposure but produces poor habitat configuration.
- **Connectivity-focused restoration** provides strong ecological connectivity outcomes but has the highest estimated agricultural opportunity cost.

The results support spatially explicit, multi-objective restoration planning that evaluates ecological condition, economic trade-offs, social accessibility, and conservation disturbance together.

## Repository structure

```text
BlackGrouse_2030/
│
├── data/
│   ├── raw/
│   ├── external/
│   └── processed/
│
├── outputs/
│   ├── figures/
│   ├── maps/
│   └── tables/
│
├── 01_setup_and_inspect_data.ipynb
├── 02_harmonise_landuse.ipynb
├── 03_observed_landuse_change.ipynb
├── 04_landscape_metrics.ipynb
├── 05_restoration_suitability.ipynb
├── 06_simulate_2030_scenarios.ipynb
├── 07_connectivity_analysis.ipynb
├── 08_compare_scenarios.ipynb
├── 09_create_figures.ipynb
├── 10_economic_opportunity_costs.ipynb
├── 11_social_access_and_recreation.ipynb
├── 12_multiobjective_assessment.ipynb
└── README.md
```

## Python packages

The workflow uses:

- `pathlib`
- `numpy`
- `pandas`
- `rasterio`
- `geopandas`
- `shapely`
- `matplotlib`
- `scipy`
- `requests`

## Reproducibility

Run notebooks sequentially from `01` to `12`.

- Notebooks `01–09` generate the ecological baseline, restoration scenarios, and ecological indicators.
- Notebook `10` calculates agricultural opportunity costs.
- Notebook `11` calculates population accessibility, recreation-network proximity, and disturbance exposure.
- Notebook `12` integrates all indicators and performs policy-weight and sensitivity analyses.

The dispersed scenario uses a fixed random seed of `42`. The weight-sensitivity analysis also uses a fixed random seed of `42`.

Large national datasets are not intended to be stored in the repository. The README or a separate data guide should document their providers, required filenames, coordinate reference system, and preparation steps.

## Limitations

- The scenarios are spatial restoration alternatives, not predictions of future land-use change.
- The harmonised core-habitat category is a landscape-scale habitat proxy.
- Restoration suitability does not include field-measured vegetation structure, habitat quality, management intensity, or demographic Black Grouse data.
- Connectivity results depend on the selected gap-distance thresholds.
- Small habitat pixels may not represent functional habitat patches.
- BRP does not cover every restored pixel; uncovered areas are reported separately.
- Standard Output estimates include direct crop matches, transparent related-crop proxies, category-median proxies, and zero-output assumptions.
- Standard Output represents standardised agricultural output, not land price, compensation cost, farm profit, or complete welfare loss.
- CBS confidentiality codes were represented using lower, midpoint, and upper population estimates.
- Population access was calculated using Euclidean distance to restoration, not travel time through a routable network.
- TOP10NL represents mapped recreation infrastructure but does not fully capture local restrictions, seasonal closures, visitor intensity, or actual public access.
- The multi-objective results depend on indicator selection, standardisation, and policy weights.