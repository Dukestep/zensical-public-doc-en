---
tags:
  - Regional
  - Deterministic
  - Arctic
---

![ECCC logo](../../img_eccc-logo.png)

# Data and Products of the experimental Canadian Arctic Prediction System (CAPS)

The Canadian Arctic Prediction System (CAPS) is an experimental coupled atmosphere-ocean-ice prediction system based on a limited-area configuration (LAM) of the Global Environmental Multiscale (GEM) model, coupled with the Nucleus of European Modeling of the Ocean (NEMO) and the Community ICe Code (CICE). It covers the entire Arctic basin with a horizontal grid resolution of approximately 3 km. The system CAPS is driven by ECCC's [Global Deterministic Prediction System (GDPS)](../nwp_gdps/readme_gdps.md), which provides initial and lateral boundary conditions for atmospheric fields. Initial hydrometeorological fields are recycled from the 12-hour forecast of the previous CAPS integration. In addition, the GDPS is used to force the ocean-ice model outside the coupled regions. Initial conditions for ocean-ice fields are taken from the [Regional Ocean-Ice Prediction System (RIOPS)](../nwp_riops/readme_riops.md). Ocean boundary conditions in the North Atlantic and North Pacific come from the GDPS. The system CAPS runs twice a day and is initialized at 00 and 12 UTC, respectively, with a 48-hour integration.

## Access

### How to access the data

This experimental data is available from the [MSC GeoMet](../../msc-geomet/index.md) API / web services and on the [MSC Datamart](../../msc-datamart/index.md) data server respectively:

* [Data available via the GeoMet-Weather geospatial web services](https://eccc-msc.github.io/open-data/msc-geomet/readme_en/)
* [GRIB2 and NetCDF data available on the MSC Datamart](readme_caps-datamart.md)
* [GRIB2 weather elements on the grid data available on the MSC testing data repository DD-Alpha](readme_caps-weong-datamart.md)

An [overview and examples to access and use the Meteorological Service of Canada's open data](../../usage/index.md) is available.

### Licence

The [end-user licence for Environment and Climate Change Canada's data servers](../../licence/index.md) specifies the conditions of use of this data.

### MSC Open Data Service Usage Policy

The [MSC Open Data Service Usage Policy](../../usage-policy/index.md) determines what constitutes an acceptable use of MSC Open Data services and provides users best practices for optimal use.

### Discovery metadata

Upcoming.

## Technical documentation

* [Current version of the Canadian Arctic Prediction System](https://collaboration.cmc.ec.gc.ca/cmc/cmoi/product_guide/docs/tech_specifications/tech_specifications_CAPS_e.pdf)
* [Diagram of dependencies](https://collaboration.cmc.ec.gc.ca/cmc/cmos/public_doc/msc-data/nwep-dependency-diagrams/system_CAPS_en.svg)
* [Technical Note](https://collaboration.cmc.ec.gc.ca/cmc/cmoi/product_guide/docs/tech_notes/technote_caps_e.pdf)
* [Weather elements on the grid (WEonG) technical Note](https://collaboration.cmc.ec.gc.ca/cmc/cmoi/product_guide/docs/tech_notes/technote_weong-hrdps_e.pdf)

## Changelog

The chronology of changes to the Regional Canadian Arctic Prediction System (CAPS) is available [here](changelog_caps.md).
