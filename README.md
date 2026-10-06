# Every Hour Matters: An Hourly Spatio-Temporal Assessment of Air Quality, Dominant Pollutants, and Potential Population Burden in Belgrade, Serbia (2024–2025)

This repository presents an interactive web application and the analytical framework of a research study on the hourly spatio-temporal structure of air quality in Belgrade, Serbia.

The study uses validated hourly measurements from 27 automatic monitoring stations (AMS) of the local air quality monitoring network of the Belgrade City Institute of Public Health (GZJZ), classified according to the revised European Air Quality Index (EAQI), and links them with the spatial distribution of population.

The framework shows what information a dense ground-based hourly network provides, and what is lost when air quality data are reduced to an annual mean or to the overall share of adverse hours.

**Interactive application:** [Serbian](https://jelena383.github.io/belgrade-hourly-air-quality/) | [English](https://jelena383.github.io/belgrade-hourly-air-quality/index_en.html)

The application is retrospective (2024–2025) and does not show current conditions. For current air quality in Serbia, see the portal of the Serbian Environmental Protection Agency: https://vazduh.sepa.gov.rs/

## Project Objective

The central research question was what information on the timing, duration and spatial differences of adverse air quality conditions is provided by hourly measurements of a densely distributed local monitoring network, and what remains hidden when the data are reduced to summary indicators.

The analysis aimed to:

- examine whether the mean PM2.5 concentration differentiates monitoring sites according to the frequency of adverse hours,
- identify when adverse conditions occur and how long they last,
- determine which pollutant drives the adverse classification by season, hour of day and station type,
- link the temporal burden with the spatial distribution of population,
- and assess the spatial coverage of the existing monitoring network.

## Study Area and Monitoring Network

The analysis covers the territory of the City of Belgrade (17 city municipalities, approximately 1.7 million inhabitants) for the period 1 January 2024 – 31 December 2025.

The dataset comprises validated hourly measurements from 27 automatic monitoring stations of the GZJZ local network, the only measuring points of that network that provide the hourly data required for the EAQI. The stations are officially classified as urban, suburban, industrial, traffic and combined types, and the distance between nearest neighboring sites ranges from 1.42 km to 28.11 km.

After quality and completeness control, the final dataset contained 473,634 hourly records, of which 471,642 hours received a valid EAQI category.

## Methodological Framework

### EAQI classification

Each hour at each monitoring site was classified according to the revised European Air Quality Index of the European Environment Agency (González Ortiz et al., 2025), based on hourly concentrations of five pollutants:

- PM2.5,
- PM10,
- NO2,
- O3,
- and SO2.

The overall category of each hour is determined by the pollutant with the least favorable category, which is recorded as the dominant pollutant.

### Poor+ hours

Hours classified as Poor, Very poor or Extremely poor were grouped into an operational category **Poor+**. Poor+ is an analytical group defined for the study, not an official index category, and not a boundary between safe and harmful air.

### Analytical dimensions

The framework links four complementary analytical dimensions:

1. **Spatial distribution:** Poor+ share by monitoring site and its relationship with the mean PM2.5 concentration.
2. **Temporal patterns:** seasonal and diurnal patterns, an hourly burden calendar (month × hour), a winter–summer paired test, cluster analysis of seasonal profiles, and the duration of continuous Poor+ episodes.
3. **Dominant pollutant:** the pollutant that determines the Poor+ classification, by season, hour of day and station type.
4. **Person-hours indicator:** the number of inhabitants assigned to the Voronoi zone of each monitoring site (15 km maximum radius, WorldPop 2024 population raster), multiplied by the number of Poor+ hours at that site.

### Person-hours indicator

The person-hours indicator is a measure of spatio-temporal population burden at area level. It is not a measure of individual exposure or health effect.

Interpretation logic:

- more Poor+ hours and more inhabitants in a site's zone → higher person-hours value,
- a high Poor+ share in a sparsely populated zone → lower person-hours value.

The ranking of sites by person-hours was tested at radii of 5, 15 and 20 km and remained highly consistent (Spearman's ρ = 0.929–0.993).

## Key Findings

- **A single number does not tell the whole story.** The mean PM2.5 concentration explains 27.9% of the variation in the Poor+ share between monitoring sites.
- **Three different rankings.** The site with the highest Poor+ share (Franše Deperea, 27.27%) is neither the site with the longest single episode (Leštane, 132 consecutive hours) nor the site with the highest person-hours value (Pošta Srbije, 510.4 million person-hours).
- **Seasonal and diurnal structure.** The Poor+ share was 26.51% in winter and 14.32% in summer (Cohen's d_z = 1.16), with peaks on winter evenings and summer afternoons. Monitoring sites form three seasonal groups that do not follow the official station type.
- **The dominant pollutant changes.** PM2.5 predominates in winter and evening Poor+ hours, O3 in summer Poor+ hours and around midday, and NO2 is the most frequent dominant pollutant at three traffic sites.
- **High but uneven coverage.** 98.0% of the population lives within 15 km of an analyzed station, while the uncovered population is concentrated mainly in the municipality of Obrenovac (86.6%).

## Interactive Application

The web application presents the results of the study through:

- a map of the 27 monitoring sites with the Poor+ share, dominant pollutant and person-hours indicator,
- the 15 km coverage layer and areas outside monitoring network coverage,
- the hourly burden calendar and seasonal patterns by monitoring site,
- an hour-by-hour view of EAQI categories for 2024–2025,
- the dominant pollutant by season and hour of day,
- and tables of Poor+ episodes with playback of the longest episodes.

All values in the application are identical to the tables of the study.

## Software and Methods

**Data processing and statistics**

- Python 3.13 (pandas, NumPy, SciPy, scikit-learn)
- Pearson and Spearman correlation
- Paired t-test, Shapiro–Wilk and Wilcoxon signed-rank tests
- Hierarchical cluster analysis (Ward's method), k-means, silhouette coefficient and adjusted Rand index

**GIS and spatial analysis**

- QGIS
- GeoPandas, Shapely, Rasterio, pyproj
- Voronoi allocation
- Population raster analysis (WorldPop R2025A)
- Environmental cartography

**Web application**

- HTML, CSS and JavaScript
- Leaflet 1.9.4

## Repository Contents

| File | Description |
|---|---|
| `index.html` | Interactive application (Serbian) |
| `index_en.html` | Interactive application (English) |
| `lokacije.js` | Monitoring sites with Poor+ share, dominant pollutant and person-hours |
| `podaci.js` | Hourly burden calendar, monthly Poor+ shares and dominant pollutant results |
| `satni.js` | Hourly EAQI categories by monitoring site, 2024–2025 |
| `podloga.js` | Base map (municipal boundaries and rivers) |
| `leaflet.js`, `leaflet.css`, `images/` | Leaflet 1.9.4 (BSD-2-Clause, see `LICENSE-Leaflet.txt`) |

## Limitations

- The analysis covers only the 27 automatic stations of the GZJZ local network; semi-automatic and indicative measuring points and stations of the national network are not included.
- The EAQI is an air quality index, not a measure of health risk, and the study does not assess regulatory compliance.
- O3 is not measured at three monitoring sites, so their Poor+ share may be underestimated.
- Meteorological data were not used, so the patterns do not establish emission sources or causal mechanisms.

## Data

Hourly air quality data are the property of the Belgrade City Institute of Public Health and are presented with its consent. Population data: WorldPop R2025A (Bondarenko et al., 2025, https://doi.org/10.5258/SOTON/WP00839).

## Scientific and Practical Relevance

The study shows how hourly data that a monitoring network already routinely collects can, without new measurements, provide reproducible information on:

- when adverse air quality conditions are most likely and how long they last,
- which pollutant predominantly determines them,
- where they overlap with the largest number of inhabitants,
- and where the spatial coverage of the monitoring network is limited.

This information can support air quality reporting, more temporally targeted public communication and the planning of the monitoring network.

## Contact

For additional methodological details, collaboration opportunities, or air quality and GIS-related research inquiries, feel free to connect with me on LinkedIn.

[LinkedIn Profile](https://www.linkedin.com/)

## Author

**Jelena Lukić**
Environmental Monitoring Specialist | GIS & Spatial Analytics
Belgrade City Institute of Public Health
ORCID: [0009-0008-7883-6402](https://orcid.org/0009-0008-7883-6402)
