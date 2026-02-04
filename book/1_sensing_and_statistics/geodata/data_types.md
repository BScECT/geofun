# Variable and data types

## What is a variable?

Variable comes from the Latin *variabilis*, which means changeable. So a variable is a number, quantity, property, or characteristic that can change. Temperature for instance is a property that varies in space and time. Variables are opposed to constants, and physical constants in the context of the geosciences, which are assumed to always have the same value in a given system. The speed of light in vacuum and the gravitational constant are examples of physical constants.

This perspective is valid in geoscience and statistics, but variables also show up in another field: programming. There, a variable is a named container that stores a piece of information, called a value. In Python a variable can always be changed, so our initial definition remains valid, but in other programming languages such as C++ some variables can be defined as constant, so they cannot be changed after creation.

## How to differentiate variables?

### The standard approach

In this approach, variables are classified based on three criteria:

  * Whether they are countable &ndash; i.e., they are finite or countably infinite &ndash; or uncountable.
  * Whether they are ordered &ndash; i.e., their values can be ranked &ndash; or unordered.
  * Whether they are metric &ndash; i.e., they have valid distances between values &ndash; or non-metric.

Those criteria lead to four main types of variables, divided into two main classes:

  * Numerical variables:

    * *Continuous variables* are uncountable, ordered, and metric, e.g., the size of the grains in a sedimentary clastic rock. They are usually represented by floats.
    * *Discrete variables* are countable, ordered, and metric, e.g., the number of grains in a sedimentary clastic rock. They are usually represented by integers, although they can also be floats.

  * Categorical variables:

    * *Ordinal variables* are countable, ordered, and non-metric, e.g., the type of sedimentary material (silt, sand, gravel), which are based on grain size so can be ordered. They are usually represented by strings or integers.
    * *Nominal variables* are countable, unordered, and non-metric, e.g., the type of rock (igneous, metamorphic, or sedimentary). They are usually represented by strings.

### Other options

In statistics, another criterion is sometimes considered: whether variables have an absolute zero point, i.e., they have a true zero implying that there none of the variable. Based on that, categorical variables remain the same as before, but numerical variables become:

  * *Interval variables* are ordered and metric, but do not have an absolute zero, e.g., the elevation relative to sea level and the temperature in °C.
  * *Ratio variables* are ordered, metric, and have an absolute zero, e.g., the elevation relative to the center of the Earth temperature in °K.

As implied by their name, the ratio between two values only has a meaningful interpretation with ratio variables. Differences and ratios of differences have a meaningful interpretation with both interval and ratio variables. Note that interval and ratio variables are not incompatible with continuous and discrete variables, of which they can be considered sub-types.

It is also possible to define other sub-types because they can require special treatment when applying statistical methods, for instance:

  * *Directional variables*, e.g., angles, for which 0 is equal to 360°. Using standard formulas for summary statistics like the mean can lead to meaningless results.
  * *Bounded* or *truncated variables*, e.g., the porosity of a rock, which is bounded by 0 and 1. Predicting such variables properly requires to keep the predictions within those bounds.
  * *Compositional variables*, e.g., geochemical composition of a rock, often expressed as percentages that must sum to 100%. Predicting such variables properly requires to take this extra constraint into account.

## What are data?

A datum is a single piece of information, also called an observation. An observation can hold multiple values linked to multiple variables but associated to a common source, e.g., atmospheric temperature and pressure at a given time and location, or porosity and permeability of a given rock sample. The plural of datum, data, is a collection of observations. A dataset is an organized collection of data from one or multiple origins.

Earth System data are a specific type of data that connect to time-varying or static phenomena in the Earth system. As illustrated by the data-to-insight workflow (see {numref}`figure {number} <data-to-insight_workflow>` in the previous section), our goal is to extract insights from those data to support decision making.

## How to organize and store geodata?

### As tabular data

Tabular data are organized as tables, i.e., as ordered arrangements of columns and rows, for instance (data from [de Freitas et al., 2025](https://doi.org/10.1594/PANGAEA.986961)):

| Event | Depth sed | Age | SR | δ<sup>13</sup>C |
| :----: | :---: | :--: | :---: | :--------: |
| NPAL05 | 0.000 | 2019 |       |            |
| NPAL05 | 0.005 | 2018 | 0.270 | -23.342881 |
| NPAL05 | 0.015 |      |       | -23.258775 |
| NPAL05 | 0.025 | 2010 | 0.230 | -23.275825 |
| NPAL05 | 0.035 | 2004 | 0.180 | -23.697444 |
| NPAL05 | 0.045 | 1998 | 0.150 | -23.341460 |
| NPAL05 | 0.055 | 1991 | 0.140 | -23.463614 |
| NPAL05 | 0.065 | 1983 | 0.130 | -23.404730 |
| NPAL05 | 0.075 | 1975 | 0.110 | -23.402234 |

The columns represent different variables and the rows different observations that include the values of each variable. This is the simplest and most frequent type of data. They can be homogeneous or heterogeneous, i.e, made of variables of different types represented by different programming data types (i.e., a mix of integer, float, or string).

Tabular data are usually stored as comma-separated values (CSV) files (with extension `.csv`), which are simple text files. Each line represents an observation, and its values are separated by commas (same data from [de Freitas et al., 2025](https://doi.org/10.1594/PANGAEA.986961)):

```
Event, Depth sed, Age, SR, δ13C
NPAL05, 0.000, 2019, , ,
NPAL05, 0.005, 2018, 0.270, -23.342881
NPAL05, 0.015, , , -23.258775
NPAL05, 0.025, 2010, 0.230, -23.275825
NPAL05, 0.035, 2004, 0.180, -23.697444
NPAL05, 0.045, 1998, 0.150, -23.341460
NPAL05, 0.055, 1991, 0.140, -23.463614
NPAL05, 0.065, 1983, 0.130, -23.404730
NPAL05, 0.075, 1975, 0.110, -23.402234
```

The first line usually contains the variable names and is called the header. Unfortunately, this standard is infrequently respected. Sometimes the separator is a tab or a semicolon instead of a comma, and extra information is added above the header, which can require preprocessing to be read by programming languages.

### As vector data

Vector data represent geographic features as ({numref}`figure {number} <vector_example>`):

  * *Points*, which are single x, y (z) coordinates.
  * *Lines*, which are two points (also called vertices) or more that are connected.
  * *Polygons*, which are three points or more that are connected and closed.

````{figure} ../../figures/part-a_vector_example.jpg
---
name: vector_example
width: 100%
align: center
---
Example of vector data: rivers represented as lines and land masses as polygons (data from [HydroSHEDS](https://www.hydrosheds.org/products/hydrorivers)).
````

Each point, line, or polygon can store one or several variable values as attributes. They are best suited to map discrete objects such as rivers and surficial geological units, and when topology and connectivity are to be analyzed.

Multiple formats exist to store vector data, with the most common being:

 * *Shapefile*, which was developed by the company Esri and is now a mostly open specification. It is made of multiple files (with extensions `.shp`, `.shx`, `.dbf`, `.prj`) storing the geometry, variable values, and coordinate system of the data. All those files are required to open the dataset.
 * *GeoJSON*, which is an open format based on the JavaScript Object Notation (JSON). It is also text-based, so it can be read directly from a text editor. It is made of a single file (with extension `.json` or `.geojson`).
 * *GeoPackage*, which is an open format that can store vector but also raster data. It is made of a single file (with extension `.gpkg`).

### As raster data

Raster data are organized as matrices of pixels (in 2D, in 3D we call them voxels), each pixel containing one or several values ({numref}`figure {number} <raster_example>`). Pictures taken with a camera or a phone are a type of raster data.

````{figure} ../../figures/part-a_raster_example.jpg
---
name: raster_example
width: 100%
align: center
---
Example of raster data: topography and bathymetry of Earth (data from [NOAA](https://www.ncei.noaa.gov/products/etopo-global-relief-model)).
````

Those pictures contain a given number of rows, a given number of columns, and three channels (RGB channels, one for the color red, one for blue, and one for green). While nowadays the JPG and PNG file formats have become more popular, they were traditionally saved as TIFF files (with extension `.tiff` or `.tif`).

In a spatial context, this simple format is not enough. We need to also store some information about where the raster data were acquired. So on top of the number of rows and columns, we need:

  * The *origin*, i.e., the coordinate of the top-left corner of the image.
  * The *cell size*, i.e., the size of a pixel, which is identical for all the pixels of a raster and defines its resolution.
  * The *coordinate reference system*, i.e., the system used to project the raster from a spherical Earth to a planar map (you will learn more about that in the following chapters).

Those components are *metadata*, i.e., information that helps us understand the data, or "data about the data". They give us a georeferenced image, i.e., an image that can be located in the real world. Such image is often stored using an extension of the TIFF format called GeoTIFF (with the same extension `.tiff` or `.tif`). They are best suited to map continuous fields such as temperature and elevation, and when needing full spatial coverage over large areas.

Raster data can also be seen from a vector perspective as a set of connected polygons forming a grid. The advantage is that we can then build more flexible irregular grids; the inconvenient is that this is more difficult than building a standard, regular raster. This is something you will learn more about later in your studies.
