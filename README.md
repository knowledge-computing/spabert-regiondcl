# Bridging Spatial Language Models and Urban Foundation Models to Capture Diverse Urban Contexts

This repository contains essential scripts for integrating RegionDCL with SpaBERT, as described in our paper: Bridging Spatial Language Models and Urban Foundation Models to Capture Diverse Urban Contexts.

## Usage
This repository only contains the updated components. To run the whole pipeline, please first clone the original repositories of RegionDCL and SpaBERT:

```
git clone https://github.com/LightChaser666/RegionDCL.git
git clone https://github.com/knowledge-computing/spabert.git
```

To fine-tune **SpaBERT** with POI data, please convert your POI shapefile (`.shp`) into the required format. We provide a Jupyter notebook for this process: 
```
poi_datageneration.ipynb
```
This notebook performs:
- Loading and preprocessing POI shapefile data
- Extracting relevant attributes and coordinates
- Converting the data into JSON format compatible with SpaBERT fine-tuning

Next, replace the **RegionDCL** ```data_util/preprocess.py``` with the updated version:
```
cp preprocess.py ./data_util/preprocess.py 
```
In this updated `preprocess.py`:
- The original one-hot encoding of POIs is replaced with **SpaBERT embeddings**
- When multiple POIs belong to the same building, their features are **averaged by the number of POIs**

This ensures that RegionDCL utilizes contextualized semantic representations from SpaBERT rather than sparse one-hot features.
