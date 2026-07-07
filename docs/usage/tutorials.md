![ECCC logo](../img_eccc-logo.png)

# Tutorials

!!! tip "Access tutorials"
    This page presents the available tutorials grouped by data-access standard: WMS, WCS, OGC API &ndash; Features, and raw data (including GRIB2), see links below:

## WMS

<div class="grid cards" markdown>

-   :material-animation: **[MSC AniMet](../msc-animet/index.md)**

    ---

    - [X] Display data on an interactive map
    - [X] Create and share custom animations
    - [X] Access third-party WMS services (ECMWF, NASA, NOAA, and more)

-   :material-layers: **[Tutorial: display, interact and animate WMS layers in QGIS](tutorial_WMS_QGIS/)**

    ---

    - [X] Add a WMS/WMTS connection and layer
    - [X] Browse and switch between available layer styles
    - [X] Pan, zoom, and query pixel values (GetFeatureInfo)
    - [X] Animate the layer's time dimension

-   :material-web: **[Tutorial: building interactive web maps with OpenLayers and Leaflet](tutorial_web-maps/)**

    ---

    - [X] Display a WMS layer on an interactive map
    - [X] Build interactive popups with feature queries
    - [X] Animate time-enabled WMS layers

-   :material-language-python: **[Use case: anticipated profits based on precipitations probability](use-case_arthur/use-case_arthur.md)**

    ---

    - [X] Query WMS services in Python with OWSLib
    - [X] Query layers for specific locations and time ranges
    - [X] Show results as plots and data tables

    [:lucide-download: Download the jupyter notebook ](use-case_arthur/use-case_arthur.ipynb){ .md-button .md-button--primary }

</div>

## WCS

<div class="grid cards" markdown>

-   :material-console: **[Use GDAL to extract data from GeoMet's Web Coverage Service (WCS) endpoint](tutorial_gdal/tutorial_gdal.md)**

    ---

    - [X] Extract raster data from a WCS endpoint
    - [X] Save output to disk in various formats
    - [X] Reproject a raster and convert it to NetCDF
    - [X] Get the value at a specific longitude/latitude point

    [:lucide-download: Download the jupyter notebook](tutorial_gdal/tutorial_gdal.ipynb){ .md-button .md-button--primary }

</div>

## OGC API &ndash; Features

<div class="grid cards" markdown>

-   :material-earth: **[Use OGC API - Features in QGIS](tutorial_OAFeat_QGIS/)**

    ---

    - [X] Add a WFS/OGC API - Features connection
    - [X] Build and filter data with a custom query
    - [X] Display the resulting vector layer

-   :material-chart-bar: **[Use OGC API - Features in Power BI](tutorial_OAFeat_Power-BI/)**

    ---

    - [X] Build a filtered Open Data Collections URL
    - [X] Load real-time hydrometric data as CSV into Power BI
    - [X] Display the data on a simple report map

-   :material-code-braces: **[Make OGC API - Features requests from Python with OWSLib](use-case_oafeat/use-case_oafeat-script.md)**

    ---

    - [X] Case study: monitoring water levels at hydrometric stations
    - [X] Create time series and interactive maps
    - [X] Display time series data in graphic and tabular format

    [:lucide-download: Download the jupyter notebook](use-case_oafeat/use-case_oafeat-script.ipynb){ .md-button .md-button--primary }

-   :material-table: **[Make OGC API - Features requests using VBA in Excel and R](tutorial_OAFeat_R-Excel/)**

    ---

    - [X] Query AQHI observations real-time data from the web
    - [X] [Plot data using R in RStudio](tutorial_OAFeat_R-Excel.md#r-example)
    - [X] [Generate tables and graphs using VBA in Excel](tutorial_OAFeat_R-Excel.md#excel-example)

</div>

## Raw data

<div class="grid cards" markdown>

-   :material-layers: **[Tutorial: adding raw geospatial file in QGIS](tutorial_raw-data_QGIS/)**

    ---

    - [X] Add downloaded vector/raster files (Shapefile, GeoJSON, GRIB2, GeoTIFF, NetCDF...)
    - [X] Drag and drop files directly from MSC Datamart
    - [X] Works with WCS and OGC API - Features outputs too

-   :material-file-document-outline: **[Use of GRIB2 data format](../msc-data/readme_grib.md)**

    ---

    - [X] Learn the structure of the GRIB2 format
    - [X] Decode GRIB2 files with GDAL or wgrib2
    - [X] Visualize GRIB2 data with GEMPAK or NCL

</div>
