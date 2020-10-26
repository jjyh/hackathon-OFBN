---
title: 'Climate Change: Too hot for our forests to handle?'
author: 'MECP hackathon team 3: M.Williamson, M.Khaddaj, D. Nguyen, J.Ho '
date: "October 2020"
output: 
  html_document:
    keep_md: true
    df_print: paged
bibliography: citation.bib
always_allow_html: yes
---
  
Shortcut to Data Sources and References: [References]  


# Background: Climate Change and Forests
Climate change is occurring - palpably and audibly so in its many manifestations.  But the trees are silent.  If one falls, is no one around to hear it?

The Ontario Ministry of Environment, Conservation and Parks (MECP)'s Terrestrial Assessment and Field Services Unit has been listening. The MECP has kept careful watch of our forests in the Ontario Forest Biomonitoring Network (OFBN), comprising of 111 mature stand plots over 30 years since 1986. [@OFBNppt] The OFBN has developed the Decline Index (DI) as a cumulative representation of observed tree stresses.

To understand future changes we need to know what has happened before. Future projections are long-term but our climate has already been changing. Understanding how much change has happened in recent years can help in creating models to predict the effects of climate change on forest ecosystems.  An exploratory dashboard for this purpose has been created for the MECP hackathon 2020, accessible at this location: http://15.223.127.188/#/site/EnvironmentalDataHackathon/projects/74

This documentation explains in detail the data sources, approach rationale, data processing and references used in the dashboard.  

# Objective
Much research has demonstrated that climate conditions over the long-term and annual differences affect forest health. Temperature and moisture are the most important climate factors influencing forest health. Extreme events will have substantial impact on forest health because of: 
1.Increases in Intensity, Duration and Frequency  
2.Irregular Timing  
3.Less Periodicity (more variable and less predictable)  

The dashboard seeks to provide visual insights on:  
1.How have climate conditions changed over in the OFBN sites?  
2.Do climate conditions differ among the OFBN sites?  
3.Do climate condition changes over the years differ among the OFBN sites?   
4.Are the annual plot Decline Index (DI) means influenced by the climate conditions found in the plot?  

# Scope - Spatial, Temporal and Climate Factors
Due to resource limitation, the data analysis and dashboard are constrained and may be considered a proof-of-concept or pilot for further expansion.  The current iteration is constrained to:  
1. Study Time Period of 1986-2018, for which DI data have been made available for public use   
2. Fourteen OFBN plots, as a sample selection across the province  
3. Usage of Environment Canada (ECCC) climate stations  
  
To simplify the influence of climate on the forest DI, we focus on the following climate metrics that have been shown to influence hardwood forest canopy health in Vermont [@OSarticle]:    
1.April minimum temperatures  
2.Preceding August minimum temperature  
3.Preceding October minimum temperature  

# Data Sources
All data used are from open data sources available to the public.  The subsequent retrieval section will detail the processes developed to make the data more reproducibly and consistently retrievable, for potential application to expanded time periods and location sets in the future.

## Global & Ontario Climate, Introductory 
Temperature records from NOAA, NASA and University of East Anglia as compiled by NOAA [@NOAA] were used to provide overall summary of global temperature change in the dashboard introductory header.  Ontario climate trends were based on analysis of York University's Ontario Climate Data Portal, accessible at  http://lamps.math.yorku.ca/OntarioClimate/index_v18.htm [@zhu_ontario_2020]  

## OFBN forest monitoring stations
The Ontario Open Data Portal contains the OFBN Decline Index data [@OFBNdata]: 
https://geohub.lio.gov.on.ca/datasets/3649ef49222e4f6890b38c1a867da887
Of the 111 OFBN plots, fourteen plots were further short-listed for climate data exploration.  These fourteen plots are where MECP has been monitoring forest understory climate and precipitation in nearby open area (this meteorological data is expected to be open source in the future), being:

<!--html_preserve--><div id="htmlwidget-6ee8859f67b63d221307" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-6ee8859f67b63d221307">{"x":{"filter":"none","data":[["1","2","3","4","5","6","7","8","9","10","11"],[3,27,40,44,46,60,85,86,98,110,111],[46.5398600511252,46.0483373701572,46.9800847303122,43.4557647630572,42.6837761420756,44.0590203087776,44.6430496126413,44.775553504005,45.5901560559868,48.0632665939629,47.285180054605],[-79.4315628055483,-81.3081758748739,-84.5165054686367,-79.9525605328381,-80.6102842837572,-78.6081655416637,-80.7278759311884,-76.1759904585778,-78.3014222513884,-89.5621722098439,-79.7236864641308]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>OFBN Plots<\/th>\n      <th>OFBN Latitude (Decimal Degrees)<\/th>\n      <th>OFBN Longitude (Decimal Degrees)<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[1,2,3]},{"orderable":false,"targets":0}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->

The Decline Index is a weighted measure of four stress parameters for every mature hardwood stem (> 10 cm of Diameter at Breast Height) inside the plot or initial 100 trees outside the plot.  The Decline Index is calculated to the nearest whole number and ranges from zero (0) for a tree stem with no symptoms to one hundred (100) for a stem with maximum decline that does not have any live foliage.  The Decline Index is divided into five classes of decline incidence to indicate the severity of decline for plot averages [@MOE]:  

Very Low (< 11), 
Low (11-15), 
Moderate (16-20), 
High (21 - 25) and 
Severe (> 25).  

These decline incidence classes were determined by forest experts to provide a measure of tree or forest stand health.  

The calculation formula is as follows:  
DI = CD + (A \* UL) + (A \* ST) + (A \* SL/2)  

Where  
DI = Decline Index  
CD = % Crown Dieback (percent cover of branches with no live foliage in crown)  
A = ([100-CD]/400  
UL = % Undersized leaves of remnant live foliage  
ST = % leaves with strong chlorosis i.e., dark yellow throughout leaves of remnant live foliage  
SL = % leaves with slight chlorosis of light yellow-pale green throughout leaves or leaf edges of remnant live foliage  

## ECCC Climate stations
ECCC's climate station data is publicly available at [@ECdata]: https://climate.weather.gc.ca/index_e.html

The following criteria were used to select suitable ECCC climate stations:  
1. Station contains records within Study Time Period 
2. Stations must have Climate Normals data available to calculate climate anomalies. Normals are from ECCC or the Canadian Forest Service Ecoclimatic regional metrics.   
3.Stations should have similar elevation, topography and land cover to the OFBN plot. Elevation point locations were used to compare. Topography and land cover were compared using satellite imagery. None of the ECCC stations will be truly representative of local forest (influenced by soil moisture, terrain, etc.) but will provide uniform conditions and regional representation at a synoptic scale.  
4. With the above conditions met, the closest suitable station(s) were selected. More than one station can provide insight into the variation among stations at different distances. Climate metrics vary in how much they are sensitive to distance differences (e.g.anomalies robust over large distances vs. precipitation being localized).  

<!--html_preserve--><div id="htmlwidget-61559e7f059a76671acf" style="width:100%;height:auto;" class="datatables html-widget"></div>
<script type="application/json" data-for="htmlwidget-61559e7f059a76671acf">{"x":{"filter":"none","data":[["1","2","3","4","5","6","7","8","9","10","11","12","13","14","15","16","17","18","19","20","21","22","23","24","25","26","27","28","29","30","31","32","33","34","35","36","37","38","39","40","41","42","43","44","45","46","47","48","49","50","51","52","53","54"],["6085695","6085680","6085701","6085700","6085682","6065006","6068153","6068150","6068145","6057590","6057591","6057592","6153301","6153300","6137361","6137362","6166415","616I002","6166418","6166420","6166455","6166456","6119500","6119494","6119498","6119499","6102J13","6104725","6105762","6100971","6103367","6106000","6105976","6151309","6106001","7030170","6080192","6084770","6082178","6163171","6048864","6042MJ7","6048261","6048268","6048264","6048262","6048260","6048270","6048266","604HBFA","6072230","6072223","6072224","6072225"],["NORTH BAY AIRPORT","NORTH BAY A","NORTH BAY A","NORTH BAY A","NORTH BAY","MASSEY","SUDBURY A","SUDBURY A","SUDBURY CLIMATE","SAULT STE MARIE 2","SAULT STE MARIE A","SAULT STE MARIE A","HAMILTON RBG CS","HAMILTON RBG","ST THOMAS","ST THOMAS WPCP","PETERBOROUGH A","PETERBOROUGH","PETERBOROUGH A","PETERBOROUGH AWOS","PETERBOROUGH TRENT U","PETERBOROUGH TRENT U","WIARTON A","WIARTON","WIARTON A","WIARTON A","DRUMMOND CENTRE","LYNDHURST SHAWMERE","OMPAH-SEITZ","BROCKVILLE PCC","HARTINGTON IHD","OTTAWA MACDONALD-CARTIER INT'L A","OTTAWA CDA","CENTREVILLE","OTTAWA INTL A","ANGERS","ALGONQUIN PARK EAST GATE","MADAWASKA","DWIGHT","HALIBURTON 3","TRANQUILLO RIDGE","FLINT","THUNDER BAY A","THUNDER BAY CS","THUNDER BAY AWOS","THUNDER BAY A","THUNDER BAY","THUNDER BAY AIRPORT MAINTAIR","THUNDER BAY BURWOOD","THUNDER BAY WPCP","EARLTON CLIMATE","EARLTON A","EARLTON AWOS","EARLTON A"],[18.47,19.58,19.58,19.61,24.97,57.52,75.2,75.2,75.9,51.6,55.06,55.24,18.59,19.97,46.77,49.48,27.26,27.33,27.33,27.33,42.12,40.63,32.09,32.09,32.13,32.13,29.17,29.71,56.99,44.75,56.3,72.7,76.61,71.21,72.26,99.12,6.88,26.72,52.03,64.59,19.21,33.12,38.23,38.24,38.33,38.67,38.67,38.78,40.3,44.67,46.54,46.54,46.54,47.1],[46.38,46.36,46.36,46.364,46.32,46.193,46.63,46.63,46.63,46.533,46.49,46.483,43.29,43.283,42.78,42.768,44.23,44.23,44.233,44.23,44.367,44.35,44.746,44.75,44.74,44.74,45.032,44.517,45.054,44.6,44.428,45.323,45.383,44.403,45.32,45.55,45.53,45.5,45.383,45.032,48.233,48.35,48.369,48.37,48.37,48.37,48.37,48.37,48.41,48.4,47.7,47.7,47.7,47.7],[-79.4,-79.42,-79.42,-79.423,-79.47,-82.025,-80.8,-80.8,-80.8,-84.333,-84.51,-84.509,-79.91,-79.883,-81.17,-81.205,-78.36,-78.37,-78.367,-78.37,-78.3,-78.3,-81.107,-81.11,-81.11,-81.11,-76.253,-76.083,-76.784,-75.667,-76.69,-75.669,-75.717,-76.908,-75.67,-75.55,-78.27,-77.983,-78.9,-78.531,-89.517,-89.683,-89.327,-89.33,-89.32,-89.32,-89.32,-89.32,-89.28,-89.23,-79.85,-79.85,-79.85,-79.85],[370.3,370.3,370.3,370.3,201.2,200,348.4,348.39,348,211.8,192,192,102,102.1,236.2,209.1,191.4,191,191.4,191.4,198.1,216,222.2,222.5,221.9,221.9,145,86.9,276,96,160,114,79.2,150,114.9,91,397,316.4,404,330,317,274,199,199.4,199.3,199.3,199.3,194.1,200,184.4,243.4,243.8,243.4,243.2],[2017,2014,2013,1939,1887,1983,2013,1954,2011,1957,2012,1945,1997,1950,1882,1980,2010,1995,1969,2004,1968,2005,1947,1994,2016,2014,1984,1976,1994,1965,1967,1938,1889,1985,2011,1962,2004,1915,1973,1987,1991,1979,1941,2000,1994,2012,2012,2003,2005,1960,2008,2011,2000,1938],[2020,2020,2020,2013,1982,2018,2020,2013,2018,2002,2020,2012,2018,1997,1980,2020,2020,1996,2007,2010,2012,2020,2014,1995,2020,2020,2020,2020,2020,2020,2020,2011,2020,2020,2020,2020,2020,2000,2005,2020,2007,2014,2012,2020,2012,2020,2020,2005,2020,1989,2020,2020,2011,2005],[null,null,null,"Yes",null,"Yes",null,"Yes","Almanac","Yes",null,"Yes","Almanac","Yes",null,"Yes",null,null,"Yes",null,"Yes",null,"Yes",null,null,null,"Yes","Yes",null,"Yes","Yes","Yes","Yes","Yes",null,null,null,"Yes","Yes","Yes","Yes","Yes",null,null,null,null,null,null,null,null,null,null,null,"Yes"]],"container":"<table class=\"display\">\n  <thead>\n    <tr>\n      <th> <\/th>\n      <th>EC Climate ID<\/th>\n      <th>EC Station Name 100 km Website<\/th>\n      <th>Distance EC Station 100 km Website<\/th>\n      <th>EC Latitude (Decimal Degrees)<\/th>\n      <th>EC Longitude (Decimal Degrees)<\/th>\n      <th>Elevation (m)...17<\/th>\n      <th>First Year<\/th>\n      <th>Last Year<\/th>\n      <th>Normal Data<\/th>\n    <\/tr>\n  <\/thead>\n<\/table>","options":{"columnDefs":[{"className":"dt-right","targets":[3,4,5,6,7,8]},{"orderable":false,"targets":0}],"order":[],"autoWidth":false,"orderClasses":false}},"evals":[],"jsHooks":[]}</script><!--/html_preserve-->






## National Ecological Framework Ecoregions
An ecoregion is characterized by ecological factors distinctive to the region, including climate, physiography, vegetation, soil, water, and fauna.  The National Ecological Framework (NEF) Ecoregions classification and extent data are publicly available at [@ERdata]:
https://open.canada.ca/data/en/dataset/ade80d26-61f5-439e-8966-73b352811fe6 

By viewing the OFBN Decline Index within this spatial context, Eco-regional associations with decline pattern may become discernable.

# Data Retrieval and Processing
## OFBN & NEF Processing
The OFBN decline index and plot locations were used without any pre-processing.  
The NEF Ecoregion map shapefile contained multiple polygons (e.g. detailed sub-district breakdown) within each Ecoregion.  Through GIS software,these were dissolved into one polygon per Ecoregion to prevent data densification issues when overlain with OFBN plots to join in DI data.  Ecoregions without any OFBN plots were removed from processing.   
Ecoregions were manually identified as Canadian Shield regions (or not) using a calculated field by text-case within Tableau.    

## ECCC Retrieval
Data records were combined as needed from multiple stations from the same location or within close proximity, with similar elevations and land cover. Note: Different stations could be the same station with changes in station caretaker, instrumentation and slight relocations.  

ECCC provides Linux-based instruction for bulk download at the following location: https://drive.google.com/drive/folders/1WJCDEU34c60IfOnG4rv5EPZ4IhhW9vZH
To facilitate working with Tableau and Windows-based system, the team has compiled an alternate retrieval script that can be run in Windows command prompt (PowerShell) instead:  
To run a PowerShell command:  
1.	Click Start on your Desktop, type PowerShell, and then click Windows PowerShell.  
2.	Copy/paste the script to the text editor  
3.	Hit Enter  
 
The script pulls all the station data into one text file. The only limitation is that the output file contains http response headers, that need to be manually deleted. 
The variables followed by #comments can be changed:
 

```bash
$stations = 52318, 54604, 4201 , 50839 #add or remove station id separated by “,”
Foreach ($station in $stations)
{
      For ($year =1990; $year -lt 2021; $year++) #change start and end years of the required data range
      {
            for ($month =1; $month -lt 2; $month++) 
            { 
            $R = Invoke-WebRequest "https://climate.weather.gc.ca/climate_data/bulk_data_e.html?format=csv&stationID=$station&Year=$year&Month=$month&Day=14&timeframe=2&submit= Download+Data";
            $R.RawContent | Out-File C:\Users\Documents\R\HackathonMECP\data\north_bay.txt -Append #file path and file name can be changed.
           }
      }
}
```

The order of year-month-day and the data general quality was checked prior to import into Tableau

## ECCC Processing 

From the ECCC climate dataset, the following parameters were chose to explore the effect of changing climate on the forest plots:   
- Extreme minimum daily temperature, termed within the dataset as "Extr Min Daily Temp C"  
- Extreme maximum daily temperature, termed within the dataset as "Extr Max Daily Temp C"  
- Total precipitation, termed within the dataset as "Total Precip mm"  
To facilitate processing, the originally wide-format data were pivotted into long format with only the selected parameters.  
These values were further aggregated into averages relative to the ECCC station's related OFBN plot e.g. the average of the  April daily minima of several stations in proximity of an OFBN plot.  

April minimum, prior year's August mininum and prior year's Oct mininmum temperatures were factors noted by Oswald et al. (2018) to most influence forest health in their Vermont U.S. study.  These values were parsed within Tableau using filters by month.


# References


