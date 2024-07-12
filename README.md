# A novel use of Stereo Baited Remote Underwater Video and Drop Down Video for biodiversity and marine landscape mapping and prediction
[![DOI](https://zenodo.org/badge/772036364.svg)](https://zenodo.org/doi/10.5281/zenodo.10986427)

This dataset comprises data gathered using Stereo Baited Remote Underwater Video (SBRUV) and Drop Down Video (DDV) by the University of Glasgow and NatureScot respectively.
All data was taken from surveys conducted between 2013 - 2019, in the Firth of Clyde, Scotland. This resulted in 554 SBRUV and 333 DDV deployments.
The maximum number of individuals present on the screen at any one time (MaxN) was recorded for each species present and a still image captured from each station for substratum analysis.
Examination of the substratum was carried out for each deployment, the substratum within each grid square was recorded to create a proportional coverage of each substratum type at each station minus those which were classified as unknown due to poor image clarity or being obscured. Substrata were classed as algae, gravel, mud, sand, and pebble and based on two divisions of the Wentworth scale.

## Project analysis summary
In order to calculate biodiversity for each site, Simpson’s diversity was calculated for each SBRUV deployment using the rdiversity package in R From the recorded proportional cover.
Diversity and substratum coverage for each site was predicted using ordinary kriging in the R package automap.
to estimate proportional substratum coverage throughout the area of the MPA. Variograms were produced and 5-fold cross validation undertaken to examine Mean Error (ME), Mean Predicted Standard Error (MPSE), Mean Square Normalised Error (MSNE), Correlation Observed and Predicted (COP), and Correlation and Predicted Observed (CPR).

## Data structure
This script uses spatial data subset from UK boundaries shapefiles masked to the study to the study area, and marine Protected Area (MPA) boundary outline contained in (Shapefiles/South_arran_measures.shp) - created from data available from the South Arran Marine Conservation Order 2015 (Scottish Government, 2015). 
All raw SBRUV landscape data is contained in .csv file format, including fields for location (latitude/longitude), station, depth, proportional coverage of each substratum type, and the main substratum found at each station.
All raw species data contains all species and the number of occurrences recorded at each station.

## Predictions
For prediction of each category of substrata coverage and biodiversity across the study area ordinary kriging was employed. Kriging was carried out using the [automap](https://github.com/cran/automap) package in R, including variograms and 5 - fold cross validation.

## Gridded analysis
In order to analysis how coverage of predicted substrata within each set of fishing limitations within the MPA, the study area was gridded using 500x500m grid area and data extracted from each using the [raster](https://github.com/rspatial/raster) package.

## Substrata patch analysis
Analysis of each patch of predicted substrata began with first aggregating each substratum using [SDMTools](https://github.com/cran/SDMTools) raster with a cut off of minimum 20% coverage, this was then "clumped" using the [raster](https://github.com/rspatial/raster) package.
From these further analysis could be carried out such as calculating distance to edge of substrata patches, patch area, and patch perimeter to area ratio. Results from this were also used to compare differences in patch biodiversity statistics between different fishing limitation zones and substratum classifications were compared using a pairwise comparison, as the data did not meet the normality and homogeneity of variance assumptions for an ANOVA test non-parametric tests were conducted including Kruskal-Wallis, Wilcox and post-hoc Dunns tests.
