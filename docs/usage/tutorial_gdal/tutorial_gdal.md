![ECCC logo](../../img_eccc-logo.png)  


# GDAL command line tutorial with weather data

## Introduction

[MSC GeoMet](../../msc-geomet/index.md) and [MSC Datamart](../../msc-datamart/index.md) data can be manipulated via the command line using [GDAL](https://gdal.org/), a widely-known software library used to read and write raster and vector geospatial data. In the following examples, you'll use a GeoTIFF file retrieved using via a Web Coverage Service (WCS) request to MSC GeoMet. This tutorial will show you how to:
* Display the GDAL version installed on your system
* Save a WCS request output to your computer
* List information/metadata related to the raster file
* Reproject a raster file
* Convert a GeoTIFF file to the NetCDF file format
* Get the value for a specific point based on a location in longitude/latitude

There are various ways to install GDAL, please refer to https://gdal.org/ for more information.

To run the following GDAL command line examples, you need to have a basic knowledge of using the terminal command line. These examples work within a bash terminal. 

The [interactive version of this Jupyter Notebook is available](https://mybinder.org/v2/gh/ECCC-MSC/open-data/master?filepath=docs%2Fusage%2Ftutorial_gdal%2ftutorial_gdal_en.ipynb).

[![badge](https://img.shields.io/badge/Interactive%20version-binder-F5A252.svg?logo=data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAFkAAABZCAMAAABi1XidAAAB8lBMVEX///9XmsrmZYH1olJXmsr1olJXmsrmZYH1olJXmsr1olJXmsrmZYH1olL1olJXmsr1olJXmsrmZYH1olL1olJXmsrmZYH1olJXmsr1olL1olJXmsrmZYH1olL1olJXmsrmZYH1olL1olL0nFf1olJXmsrmZYH1olJXmsq8dZb1olJXmsrmZYH1olJXmspXmspXmsr1olL1olJXmsrmZYH1olJXmsr1olL1olJXmsrmZYH1olL1olLeaIVXmsrmZYH1olL1olL1olJXmsrmZYH1olLna31Xmsr1olJXmsr1olJXmsrmZYH1olLqoVr1olJXmsr1olJXmsrmZYH1olL1olKkfaPobXvviGabgadXmsqThKuofKHmZ4Dobnr1olJXmsr1olJXmspXmsr1olJXmsrfZ4TuhWn1olL1olJXmsqBi7X1olJXmspZmslbmMhbmsdemsVfl8ZgmsNim8Jpk8F0m7R4m7F5nLB6jbh7jbiDirOEibOGnKaMhq+PnaCVg6qWg6qegKaff6WhnpKofKGtnomxeZy3noG6dZi+n3vCcpPDcpPGn3bLb4/Mb47UbIrVa4rYoGjdaIbeaIXhoWHmZYHobXvpcHjqdHXreHLroVrsfG/uhGnuh2bwj2Hxk17yl1vzmljzm1j0nlX1olL3AJXWAAAAbXRSTlMAEBAQHx8gICAuLjAwMDw9PUBAQEpQUFBXV1hgYGBkcHBwcXl8gICAgoiIkJCQlJicnJ2goKCmqK+wsLC4usDAwMjP0NDQ1NbW3Nzg4ODi5+3v8PDw8/T09PX29vb39/f5+fr7+/z8/Pz9/v7+zczCxgAABC5JREFUeAHN1ul3k0UUBvCb1CTVpmpaitAGSLSpSuKCLWpbTKNJFGlcSMAFF63iUmRccNG6gLbuxkXU66JAUef/9LSpmXnyLr3T5AO/rzl5zj137p136BISy44fKJXuGN/d19PUfYeO67Znqtf2KH33Id1psXoFdW30sPZ1sMvs2D060AHqws4FHeJojLZqnw53cmfvg+XR8mC0OEjuxrXEkX5ydeVJLVIlV0e10PXk5k7dYeHu7Cj1j+49uKg7uLU61tGLw1lq27ugQYlclHC4bgv7VQ+TAyj5Zc/UjsPvs1sd5cWryWObtvWT2EPa4rtnWW3JkpjggEpbOsPr7F7EyNewtpBIslA7p43HCsnwooXTEc3UmPmCNn5lrqTJxy6nRmcavGZVt/3Da2pD5NHvsOHJCrdc1G2r3DITpU7yic7w/7Rxnjc0kt5GC4djiv2Sz3Fb2iEZg41/ddsFDoyuYrIkmFehz0HR2thPgQqMyQYb2OtB0WxsZ3BeG3+wpRb1vzl2UYBog8FfGhttFKjtAclnZYrRo9ryG9uG/FZQU4AEg8ZE9LjGMzTmqKXPLnlWVnIlQQTvxJf8ip7VgjZjyVPrjw1te5otM7RmP7xm+sK2Gv9I8Gi++BRbEkR9EBw8zRUcKxwp73xkaLiqQb+kGduJTNHG72zcW9LoJgqQxpP3/Tj//c3yB0tqzaml05/+orHLksVO+95kX7/7qgJvnjlrfr2Ggsyx0eoy9uPzN5SPd86aXggOsEKW2Prz7du3VID3/tzs/sSRs2w7ovVHKtjrX2pd7ZMlTxAYfBAL9jiDwfLkq55Tm7ifhMlTGPyCAs7RFRhn47JnlcB9RM5T97ASuZXIcVNuUDIndpDbdsfrqsOppeXl5Y+XVKdjFCTh+zGaVuj0d9zy05PPK3QzBamxdwtTCrzyg/2Rvf2EstUjordGwa/kx9mSJLr8mLLtCW8HHGJc2R5hS219IiF6PnTusOqcMl57gm0Z8kanKMAQg0qSyuZfn7zItsbGyO9QlnxY0eCuD1XL2ys/MsrQhltE7Ug0uFOzufJFE2PxBo/YAx8XPPdDwWN0MrDRYIZF0mSMKCNHgaIVFoBbNoLJ7tEQDKxGF0kcLQimojCZopv0OkNOyWCCg9XMVAi7ARJzQdM2QUh0gmBozjc3Skg6dSBRqDGYSUOu66Zg+I2fNZs/M3/f/Grl/XnyF1Gw3VKCez0PN5IUfFLqvgUN4C0qNqYs5YhPL+aVZYDE4IpUk57oSFnJm4FyCqqOE0jhY2SMyLFoo56zyo6becOS5UVDdj7Vih0zp+tcMhwRpBeLyqtIjlJKAIZSbI8SGSF3k0pA3mR5tHuwPFoa7N7reoq2bqCsAk1HqCu5uvI1n6JuRXI+S1Mco54YmYTwcn6Aeic+kssXi8XpXC4V3t7/ADuTNKaQJdScAAAAAElFTkSuQmCC)](https://mybinder.org/v2/gh/ECCC-MSC/open-data/master?filepath=docs%2Fusage%2Ftutorial_gdal%2ftutorial_gdal_en.ipynb)

## Show GDAL version

GDAL is a suite of several command line tools. When you install GDAL you get all the different command line tools. The most basic tool is `gdalinfo` which can be used to retrieve information pertaining to your GDAL installation and display information about a raster file.


```bash
%%bash

gdalinfo --version
```

    GDAL 3.1.1, released 2020/06/22


## Save a WCS request output to disk

The OGC Web Coverage Service requests enable a client to retrieve coverage information from a raster file for a given area of interest. WCS requests are made over the internet (HTTPS) and give the user more flexibility when requesting information about the coverage of a layer compared with the more traditional way of downloading flat files. The Web Coverage Service allows for several different types of requests, each of which are described in further detail below. For more information on the WCS request parameters, please refer to the [MSC GeoMet WCS GetCoverage page](../../msc-geomet/wcs.md#wcs-getcoverage).

We are going to use a `curl` command to save the WCS request result on disk, the file will be named `CMC_glb_TMP.tif`. The result is a GeoTIFF file, showing temperature (°C) from a subset of MSC's Global Deterministic Prediction System (GDPS).


```bash
%%bash

curl "https://geo.weather.gc.ca/geomet?SERVICE=WCS&VERSION=2.0.1&REQUEST=GetCoverage&COVERAGEID=GDPS_15km_AirTemp_2m&SUBSETTINGCRS=EPSG:4326&SUBSET=x(-120,-85)&SUBSET=y(48,66)&RESOLUTION=x(0.24)&RESOLUTION=y(0.24)&FORMAT=image/tiff" > CMC_glb_TMP.tif 
```

      % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                     Dload  Upload   Total   Spent    Left  Speed
    
      0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
    100 44266  100 44266    0     0  78208      0 --:--:-- --:--:-- --:--:-- 78208


## Lists information about a raster file

The `gdalinfo` tool can be used to retrieve the downloaded raster file's metadata. The command's output will list some information on the file, such as:
* File format
* File size
* Coordinate system
* Metadata
* Band information


```bash
%%bash

gdalinfo CMC_glb_TMP.tif
```

    Driver: GTiff/GeoTIFF
    Files: CMC_glb_TMP.tif
    Size is 146, 75
    Coordinate System is:
    GEOGCRS["WGS 84",
        DATUM["World Geodetic System 1984",
            ELLIPSOID["WGS 84",6378137,298.257223563,
                LENGTHUNIT["metre",1]]],
        PRIMEM["Greenwich",0,
            ANGLEUNIT["degree",0.0174532925199433]],
        CS[ellipsoidal,2],
            AXIS["geodetic latitude (Lat)",north,
                ORDER[1],
                ANGLEUNIT["degree",0.0174532925199433]],
            AXIS["geodetic longitude (Lon)",east,
                ORDER[2],
                ANGLEUNIT["degree",0.0174532925199433]],
        ID["EPSG",4326]]
    Data axis to CRS axis mapping: 2,1
    Origin = (-119.999862068965513,66.000000000000000)
    Pixel Size = (0.239724137931034,-0.240000000000000)
    Metadata:
      AREA_OR_POINT=Area
      TIFFTAG_RESOLUTIONUNIT=2 (pixels/inch)
      TIFFTAG_XRESOLUTION=72
      TIFFTAG_YRESOLUTION=72
    Image Structure Metadata:
      INTERLEAVE=BAND
    Corner Coordinates:
    Upper Left  (-119.9998621,  66.0000000) (119d59'59.50"W, 66d 0' 0.00"N)
    Lower Left  (-119.9998621,  48.0000000) (119d59'59.50"W, 48d 0' 0.00"N)
    Upper Right ( -85.0001379,  66.0000000) ( 85d 0' 0.50"W, 66d 0' 0.00"N)
    Lower Right ( -85.0001379,  48.0000000) ( 85d 0' 0.50"W, 48d 0' 0.00"N)
    Center      (-102.5000000,  57.0000000) (102d30' 0.00"W, 57d 0' 0.00"N)
    Band 1 Block=146x14 Type=Float32, ColorInterp=Gray


It is also possible to use `gdalinfo` to retrieve some basic statistics on the raster file, such as minimum and maximum value by adding the `-mm` option. Note that the resulting values are in °C.


```bash
%%bash

gdalinfo -mm CMC_glb_TMP.tif | grep Min/Max
```

        Computed Min/Max=0.728,27.828


Adding the `-proj4` option to `gdalinfo` will output the projection definition as a proj4 string:


```bash
%%bash

gdalinfo -proj4 CMC_glb_TMP.tif | grep PROJ.4 -A 1
```

    PROJ.4 string is:
    '+proj=longlat +datum=WGS84 +no_defs'


## Reproject a raster file

Using the `gdalwarp` command, we can reproject a raster file. Using MSC GeoMet and MSC Datamart data, you only need to provide an output projection definition corresponding to a EPSG code, or you can use a proj4 string.

The following example reprojects the GeoTIFF file into an EPSG:3857 projection. The output file is named `CMC_glb_TMP_epsg3857.tif`


```bash
%%bash

gdalwarp -t_srs EPSG:3857 CMC_glb_TMP.tif CMC_glb_TMP_epsg3857.tif
```

    Creating output file that is 118P x 114L.
    Processing CMC_glb_TMP.tif [1/1] : 0...10...20...30...40...50...60...70...80...90...100 - done.


Then we can use `gdalinfo` to look at the coordinates and the proj4 string to ensure that the projection of `CMC_glb_TMP_epsg3857.tif` really is different from the original file.


```bash
%%bash

gdalinfo -proj4 epsg3857.tif | grep -E '(PROJ.4|Corner Coordinates:)' -A 5
```

    PROJ.4 string is:
    '+proj=merc +a=6378137 +b=6378137 +lat_ts=0 +lon_0=0 +x_0=0 +y_0=0 +k=1 +units=m +nadgrids=@null +wktext +no_defs'
    Origin = (-20037500.189506221562624,17439592.350557137280703)
    Pixel Size = (19796.259162699658191,-19796.259162699658191)
    Metadata:
      AREA_OR_POINT=Area
    --
    Corner Coordinates:
    Upper Left  (-20037500.190,17439592.351) (179d59'59.74"W, 82d34' 7.50"N)
    Lower Left  (-20037500.190,-17441416.294) (179d59'59.74"W, 82d34'15.13"S)
    Upper Right (20030128.356,17439592.351) (179d56' 1.34"E, 82d34' 7.50"N)
    Lower Right (20030128.356,-17441416.294) (179d56' 1.34"E, 82d34'15.13"S)
    Center      (   -3685.917,    -911.972) (  0d 1'59.20"W,  0d 0'29.49"S)


## Convert a GeoTIFF file to the NetCDF file format

Using `gdal_translate` command, we can convert a raster file from any supported format (`gdalinfo --formats`) into another raster file format.

In this example, we convert our GeoTIFF file to a NetCDF file. The `-of NetCDF` parameter tells gdal_translate in which format to do the projection. The output file will be named `CMC_glb_TMP.nc`


```bash
%%bash

gdal_translate -of NetCDF CMC_glb_TMP.tif CMC_glb_TMP.nc
```

    Input file size is 146, 75
    0...10...20...30...40...50...60...70...80...90...100 - done.


Then using `gdalinfo` we can make sure the output NetCDF file is a valid raster file.


```bash
%%bash

gdalinfo CMC_glb_TMP.nc
```

    Driver: netCDF/Network Common Data Format
    Files: CMC_glb_TMP.nc
    Size is 146, 75
    Coordinate System is:
    GEOGCRS["WGS 84",
        DATUM["World Geodetic System 1984",
            ELLIPSOID["WGS 84",6378137,298.257223563,
                LENGTHUNIT["metre",1]]],
        PRIMEM["Greenwich",0,
            ANGLEUNIT["degree",0.0174532925199433]],
        CS[ellipsoidal,2],
            AXIS["geodetic latitude (Lat)",north,
                ORDER[1],
                ANGLEUNIT["degree",0.0174532925199433]],
            AXIS["geodetic longitude (Lon)",east,
                ORDER[2],
                ANGLEUNIT["degree",0.0174532925199433]],
        ID["EPSG",4326]]
    Data axis to CRS axis mapping: 2,1
    Origin = (-119.999862068965513,66.000000000000000)
    Pixel Size = (0.239724137931034,-0.240000000000000)
    Metadata:
      Band1#grid_mapping=crs
      Band1#long_name=GDAL Band Number 1
      Band1#_FillValue=9.96921e+36
      crs#GeoTransform=-119.9998620689655 0.2397241379310344 0 66 0 -0.24 
      crs#grid_mapping_name=latitude_longitude
      crs#inverse_flattening=298.257223563
      crs#longitude_of_prime_meridian=0
      crs#long_name=CRS definition
      crs#semi_major_axis=6378137
      crs#spatial_ref=GEOGCS["WGS 84",DATUM["WGS_1984",SPHEROID["WGS 84",6378137,298.257223563,AUTHORITY["EPSG","7030"]],AUTHORITY["EPSG","6326"]],PRIMEM["Greenwich",0],UNIT["degree",0.0174532925199433,AUTHORITY["EPSG","9122"]],AXIS["Latitude",NORTH],AXIS["Longitude",EAST],AUTHORITY["EPSG","4326"]]
      lat#long_name=latitude
      lat#standard_name=latitude
      lat#units=degrees_north
      lon#long_name=longitude
      lon#standard_name=longitude
      lon#units=degrees_east
      NC_GLOBAL#Conventions=CF-1.5
      NC_GLOBAL#GDAL=GDAL 3.1.1, released 2020/06/22
      NC_GLOBAL#GDAL_AREA_OR_POINT=Area
      NC_GLOBAL#GDAL_TIFFTAG_RESOLUTIONUNIT=2 (pixels/inch)
      NC_GLOBAL#GDAL_TIFFTAG_XRESOLUTION=72
      NC_GLOBAL#GDAL_TIFFTAG_YRESOLUTION=72
      NC_GLOBAL#history=Tue Jul 21 18:51:21 2020: GDAL CreateCopy( CMC_glb_TMP.nc, ... )
    Corner Coordinates:
    Upper Left  (-119.9998621,  66.0000000) (119d59'59.50"W, 66d 0' 0.00"N)
    Lower Left  (-119.9998621,  48.0000000) (119d59'59.50"W, 48d 0' 0.00"N)
    Upper Right ( -85.0001379,  66.0000000) ( 85d 0' 0.50"W, 66d 0' 0.00"N)
    Lower Right ( -85.0001379,  48.0000000) ( 85d 0' 0.50"W, 48d 0' 0.00"N)
    Center      (-102.5000000,  57.0000000) (102d30' 0.00"W, 57d 0' 0.00"N)
    Band 1 Block=146x1 Type=Float32, ColorInterp=Undefined
      NoData Value=9.96920996838686905e+36
      Metadata:
        grid_mapping=crs
        long_name=GDAL Band Number 1
        NETCDF_VARNAME=Band1
        _FillValue=9.96921e+36


## Get the value for a specific point based on a location in longitude/latitude

Using `gdallocationinfo` command we can get the raw value of a pixel by specifying a location in either longitude/latitude or by specifying a pixel position. 

In the following example, we use longitude/latitude. The resulting value is in °C.


```bash
%%bash

gdallocationinfo -wgs84 CMC_glb_TMP.tif -100 50
```

    Report:
      Location: (83P,66L)
      Band 1:
        Value: 16.4780216217041

