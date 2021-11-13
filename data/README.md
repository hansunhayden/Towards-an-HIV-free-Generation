# Data description

## World map: ISO_A3 as country unique code

### World map: 

[ne_110m_admin_0_countries.geojson]

- `ISO_A3` : country code to associate with other data files
- `NAME_LONG`: country name in this shapefile dataset

### Sub-Saharan Africa countries: 

[ssa_country_code.csv]

- `Entity`: country name in our-world-in-data dataset
- `ISO_A3`: country code to associate with geojson file

## Regional Comparison

### Annual number of death by cause

[annual-number-of-deaths-by-cause.csv]

- Include three regions: SSA, US, CH
- 1990 - 2017
- `Entity`: region name

### Death rate: 

All data: [hiv-death-rate.csv] (including regions like World, Sub-Saharan,...)

World map: [hiv-death-rates.geojson]

SSA map: [hiv-death-rates-ssa.geojson]

- 1990-2017
- Death rate column name: `YYYY_death_rate`

- Country code: `ISO_A3`
- Country name: `NAME_LONG`

### Share of death:

All data: [share-deaths-aids.csv] (including regions like World, Sub-Saharan,...)

World map: [share-deaths-aids.geojson]

SSA map: [share-deaths-aids-ssa.geojson]

- 1990-2017
- Death rate column name: ``YYYY_death_share`

- Country code: `ISO_A3`
- Country name: `NAME_LONG`

### Women living with HIV:



### Children with HIV:

