# Toxic Schools: Interactive Map

Interactive map for the CGD working paper **"Toxic Schools: Proximity to Polluted Sites in 17 Low- and Middle-Income Countries"** by Lee Crawfurd (Center for Global Development, 2026).

**[→ Open the map](https://center-for-global-development.github.io/toxic-schools-map/)**  
**[→ CGD Working Paper](https://www.cgdev.org/publication/toxic-schools-proximity-polluted-sites-17-low-and-middle-income-countries)**  
**[→ Replication data (Zenodo)](https://doi.org/10.5281/zenodo.19359188)**

---

## Key findings

- **2,840** contaminated sites across 17 countries (TSIP)
- **2.7 million** geocoded schools analysed
- **171,348 schools (6.3%)** are within 5 km of a known polluted site — a lower bound
- **9.9%** of students (7 countries with enrolment data) attend schools within 5 km
- Private schools are more proximate to polluted sites than public schools in **all 8 countries** with available breakdowns — the opposite of the US pattern, driven by co-location of private schools and industry in wealthy urban cores

> **Note:** these figures measure *proximity* to documented sites, not confirmed exposure or health outcomes. The TSIP also includes inactive and legacy sites. Proximity is a necessary but not sufficient condition for exposure; estimates are best understood as indicators of potential risk identifying schools that warrant further environmental investigation.

---

## About the map

The map displays TSIP pollution sites alongside school locations for countries covered by the paper. Click any site to see its name, industry category, country, and nearby schools with distances.

**Layers:**
- **Polluted sites (TSIP)** — 3,180 sites in paper countries
- **Schools within 1 km** — ~20,000 schools (clustered); on by default
- **Schools 1–5 km** — ~158,000 additional schools; loaded on demand (~8 MB)
- **5 km buffer circles** — catchment rings around each site with at least one nearby school

**Map coverage note:** schools are shown for countries covered by Overture Maps / OpenStreetMap in our dataset. Five paper countries (Argentina, Bangladesh, Mexico, Pakistan, Uruguay) use national EMIS data included in the paper's headline figures but not yet in the map layer.

---

## Data sources

### Contaminated sites — Pure Earth TSIP

Polluted site locations come from the **Toxic Sites Identification Program (TSIP)** maintained by [Pure Earth](https://www.pureearth.org), downloaded in March 2026 via the [contaminatedsites.org](https://www.contaminatedsites.org) API. The TSIP is the most comprehensive global inventory of contaminated sites in lower-income settings, drawing on government requests, community reports, academic research, and media coverage.

> The TSIP substantially undercounts actual contaminated sites. Estimates suggest it captures one-seventh to one-ninth of real sites in Ghana (Dowling et al., 2016). All proximity figures are therefore lower bounds on true school–pollution co-location.

### School locations

The paper uses national school census (EMIS) data for 11 countries and Overture Maps data for 6 additional countries where public geocoded EMIS data are not available.

| Country | Source | Schools | Year | In map |
|---|---|---|---|---|
| India | UDISE+ (Ministry of Education) | 1,372,195 | 2022/23 | ✓ |
| Indonesia | Dapodik (Ministry of Education) | 396,280 | 2024 | ✓ |
| Brazil | INEP Censo Escolar | 150,131 | 2023 | ✓ |
| Mexico | SEP Catálogo de Centros de Trabajo | 270,228 | 2025 | — |
| Argentina | Mapa Educativo Nacional (MEN) | 64,638 | 2023 | — |
| Philippines | DepEd school master list | 16,022 | 2023 | ✓ |
| Peru | MINEDU Padrón de IE | 175,754 | 2024 | ✓ |
| Ghana | ESRAG EMIS (geocoded via GhanaPostGPS) | 22,581 | 2020/21 | ✓ |
| Kenya | NEMIS (Ministry of Education) | 26,197 | 2023 | ✓ |
| Colombia | SISE (DANE) | 56,650 | 2024 | ✓ |
| Bangladesh | LGED education facilities (HDX) | 78,129 | 2023 | — |
| Pakistan | Punjab EMIS | — | — | — |
| Uruguay | ANEP | — | — | — |
| Vietnam | Overture Maps (Feb 2026) | 67,087 | 2026 | ✓ |
| Cambodia | Overture Maps (Feb 2026) | 17,148 | 2026 | ✓ |
| Kazakhstan | Overture Maps (Feb 2026) | 6,365 | 2026 | ✓ |
| Kyrgyzstan | Overture Maps (Feb 2026) | 1,935 | 2026 | ✓ |
| Armenia | Overture Maps (Feb 2026) | 1,379 | 2026 | ✓ |
| Mongolia | Overture Maps (Feb 2026) | 795 | 2026 | ✓ |

[Overture Maps](https://overturemaps.org) data are available under the [CDLA Permissive 2.0](https://cdla.dev/permissive-2-0/) licence. National EMIS datasets are obtained from government open-data portals; access conditions for each country are documented in the replication package.

### Neighbourhood wealth — Meta Relative Wealth Index

The paper uses the **Meta Relative Wealth Index (RWI)** ([Chi et al., 2022](https://doi.org/10.1073/pnas.2113658119)), providing gridded estimates of relative household wealth at 2.4 km resolution for all LMICs, derived from machine learning on satellite imagery and connectivity data. RWI data are available from the [Humanitarian Data Exchange](https://data.humdata.org).

---

## Replication

All analysis code, school census data, TSIP data, government contaminated site registers, and generated tables and figures are archived at:

**<https://doi.org/10.5281/zenodo.19359188>**

---

## Citation

```
Crawfurd, Lee (2026). "Toxic Schools: Proximity to Polluted Sites in 17
Low- and Middle-Income Countries." Center for Global Development Working Paper.
https://doi.org/10.5281/zenodo.19359188
```

---

*Map data: [Pure Earth TSIP](https://www.contaminatedsites.org), [Overture Maps](https://overturemaps.org)*
