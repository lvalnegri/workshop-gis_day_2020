## GIS DAY 2020: Mapping Covid-19 in England using *R* and *Shiny*

### *R* Packages

 - [data.table](https://rdatatable.gitlab.io/data.table/) (or the [*tidyverse*](https://www.tidyverse.org/) packages [readr](https://readr.tidyverse.org/) + [dplyr](https://dplyr.tidyverse.org/) + [tidyr](https://tidyr.tidyverse.org/)) for data collection, wrangling, and engineering

 - [openxlsx](https://ycphs.github.io/openxlsx/index.html) to easily read *Excel* files
 
 - [rgdal](https://cloud.r-project.org/web/packages/rgdal/) to read the boundaries in *shapefile* format from the [ONS Geography Portal](https://geoportal.statistics.gov.uk/)

 - [sp](https://cloud.r-project.org/web/packages/sp/) to store the spatial objects as a specific *R* class (you can also use the more modern [sf](https://github.com/r-spatial/sf/), that also ties neatly within the *tidyverse*)

 - [rgeos](https://cloud.r-project.org/web/packages/rgeos/), [rmapshaper](https://github.com/ateucher/rmapshaper), [maptools](https://cloud.r-project.org/web/packages/maptools/), [raster](https://cran.r-project.org/web/packages/raster/index.html), and [terra](https://github.com/rspatial/terra) are sets of various spatial tools. 

 - [leaflet](http://rstudio.github.io/leaflet/) is the *R* wrapper for the eponymous [Javascript library](https://leafletjs.com/) that allows to build interactive maps (you can also use the more complete [tmap](https://github.com/mtennekes/tmap) or [mapview](https://github.com/r-spatial/mapview) packeages, though they both rely on *leaflet* anyway for the interactive mapping). [leaflet.extras](https://github.com/bhaskarvk/leaflet.extras), [leaflet.extras2](https://github.com/trafficonese/leaflet.extras2), and [leafsync](https://github.com/r-spatial/leafsync) are add-ons packages that allows the *R* *leaflet* package to exploit more of the functionalities included in the original JS library.

A good introduction to *R* for Spatial Data Science can be found [here](https://rspatial.org/intr/). Lots of resources about GIS in general, and its applications, can be found on the dedicated section of the [GIS Day website](https://www.gisday.com/en-us/ebooks). 

Some of the spatial packages mentioned above can be difficult to install correctly, depending on your configuration. Have a look [here](https://github.com/lvalnegri/workshops-setup_-cloud_analytics_machine#install-linux-dependencies-for-r-packages) for a guide to the installation on a Ubuntu machine.

### Boundaries

 - [MSOA](https://geoportal.statistics.gov.uk/datasets/middle-layer-super-output-areas-december-2011-ew-bsc-v2) Middle Layer Super Output Areas
 
 - [LSOA](https://geoportal.statistics.gov.uk/datasets/lower-layer-super-output-area-december-2011-ew-bsc-v2) Lower Layer Super Output Areas
 
As we are not concerned here with geographical details, both the above boundaries are downloaded in the *super generalised* form, and can be actually *simplified* further. 

Other boundaries used in the session &mdash; *LTLA* Lower Tier Local Authorities, *UTLA* Upper Tier LA, *RGN* Regions, *CCG* NHS Clinical Commissioning Groups, *STP* NHS Sustainability and Transformation Partnerships &mdash; will be built by *dissolving* methods using the above boundaries and convenient lookup tables.

You can found [here](https://www.ons.gov.uk/methodology/geography/ukgeographies/censusgeography) a brief description of the UK Census Geography hierarchy, while [this](https://bit.ly/guide-uk-geographies) is a more comprehensive starting guide to the whole of UK Geographies.

### Covid Data

 - Covid Cases by LTLA [Total](https://coronavirus.data.gov.uk/details/about-data#legacy-csv-downloads) and [by Age Class](https://coronavirus.data.gov.uk/details/about-data#cases-by-age)
 
 - [Covid Cases by MSOA](https://coronavirus.data.gov.uk/details/about-data#cases-by-middle-super-output-area-msoa)
 
 - [Covid Deaths by NHS Trust](https://www.england.nhs.uk/statistics/statistical-work-areas/covid-19-daily-deaths/)
 
 - [Hospital Admissions and Bed Occupancy by NHS Trust](https://www.england.nhs.uk/statistics/statistical-work-areas/covid-19-hospital-activity/)
 
 - [Covid Symptoms (NHS Pathways Calls and Online) by CCG and Sex + Age](https://digital.nhs.uk/data-and-information/publications/statistical/mi-potential-covid-19-symptoms-reported-through-nhs-pathways-and-111-online/latest/)
 
 - *NEW* [Covid Vaccinations](https://www.england.nhs.uk/statistics/statistical-work-areas/covid-19-vaccinations/)
 

### Ancillary Data

 - [MSOA House of Commons *intelligible* Names](https://visual.parliament.uk/msoanames)

 - [MSOA => LTLA => UTLA => RGN APR-2020](https://coronavirus.data.gov.uk/details/about-data#cases-by-middle-super-output-area-msoa)

 - [OA => LSOA => MSOA 2011](https://geoportal.statistics.gov.uk/datasets/output-area-to-lower-layer-super-output-area-to-middle-layer-super-output-area-to-local-authority-district-december-2011-lookup-in-england-and-wales)

 - [LSOA => CCG => STP => CAL APR-2020](https://geoportal.statistics.gov.uk/datasets/lsoa-2011-to-clinical-commissioning-groups-to-sustainability-and-transformation-partnerships-april-2020-lookup-in-england)

 - [ONS Postcode Directory AUG-2020](https://geoportal.statistics.gov.uk/datasets/ons-postcode-directory-august-2020)


### GeoDemographics

 - [Population by LSOA + MSOA and Sex + Age 2019](https://www.ons.gov.uk/peoplepopulationandcommunity/populationandmigration/populationestimates/datasets/middlesuperoutputareamidyearpopulationestimates)

 - [Index of Multiple Deprivation 2019](https://www.gov.uk/government/statistics/english-indices-of-deprivation-2019)

 - [Food Shops Locations](https://ratings.food.gov.uk/open-data/en-GB) See [my other github repository] to learn how to collect data related to food shops

 - [Household Disposable Income FA-2018 by MSOA](https://www.ons.gov.uk/employmentandlabourmarket/peopleinwork/earningsandworkinghours/datasets/smallareaincomeestimatesformiddlelayersuperoutputareasenglandandwales)

 - [Median House Prices Mar-2020 by MSOA](https://www.ons.gov.uk/peoplepopulationandcommunity/housing/datasets/hpssadataset2medianhousepricebymsoaquarterlyrollingyear)

 - [Electricity and Gas Consumption 2018](https://www.gov.uk/government/statistics/lower-and-middle-super-output-areas-gas-consumption)


### Credits

 - [Gis Day website](https://www.gisday.com/en-us/overview)
 
 - Contains MSOA names © Open Parliament copyright and database right 2020
 
 - Contains Ordnance Survey data © Crown copyright and database right 2020
 
 - Contains Royal Mail data © Royal Mail copyright and database right 2020
 
 - Contains Public Health England data © Crown copyright and database right 2020
 
 - Office for National Statistics licensed under the Open Government Licence v.3.0
 
