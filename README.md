# ... Project Overview... 🛰️
## EuroSAT-13Band  Multiclassification
"This repository provides code and documentation for a deep‐learning model that classifies 13-band Sentinel-2 satellite image patches (EuroSAT) into one of ten land‐cover classes (e.g., Annual Crop, Forest, Highway, etc.). By leveraging all 13 spectral bands, the model aims to achieve higher accuracy and richer feature representation. It is a high-school coding project, so it may lack lot of the finer details.”

#### Reasons for using 13Band
Combining visible, NIR, red-edge, and SWIR channels lets the model learn richer spectral signatures—yielding higher accuracy, better vegetation/water detection, and more reliable predictions in different lighting or atmospheric conditions.

#### Motivations behind this Project
My Extended Project Qualification was centered around the use of space technology in fighting climate change, and a part of the dissertation focused on Earth-monitoring satellites. This project is a start at replicating what those satellites are used for, and hopefully by the end the model can quickly identify wildfires and othe natural distaters, a simpler version of how it actually works. However, we will start with just multiclassification of the data to identify type of area.

## Dataset Details
EuroSAT-13 Band from 'https://zenodo.org/records/7711810#.ZAm3k-zMKEA'
- 10 land-cover classes: AnnualCrop, Forest, HerbaceousVegetation, Highway, Industrial, Pasture, Residential, River, SeaLake, PermanentCrop
- Each sample: 64×64 pixels × 13 spectral bands
- 27000 total images

The first real challenge was converting the TIFF image format into something usable. Due to my lack of real experience I had to do some fair bit of research into 'Rasterio', which I used to open the files. Since Rasterio needs a link to a singular TIFF image - whereas we have 27000 - I classed a Dataset that would go through the EuroSAT MS folder (main data folder) and then into each subfolder respective of the land-cover classes, and then open each TIFF file and put it into a singular dataset.

 - The data directory is the EuroSAT MS folder, where all the subfolders are located.
 - There are 3 empty arrays created at the beginning - to store paths to all .tif files, the numerical labels corresponding to the class (i.e 0 is Forest), and the names of the class folders / sub-folders inside the data directory, to map the labels back to the class names.
 - For loop loops inside all sub-folders in the EuroSAT MS, uses functions of 'os' module (used AI help for this).
 - 'glob.glob' and '*/*tif' is used to find all files inside the sub-folder that have the file attachment .tif.
 - Use Rasterio to open the files - as it can read geospatial raster data - and create an Numpy array of (height, width, 13), and later convert the array into a tensor.
 


