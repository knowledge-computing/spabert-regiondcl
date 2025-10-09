# Bridging Spatial Language Models and Urban Foundation Models to Capture Diverse Urban Contexts

This repository contains scripts for integrating a spatial language model, SpaBERT, with an urban foundation model, RegionDCL, to improve urban characterization in cities with heterogeneous environments.

We gratefully acknowledge the authors of **SpaBERT** and **RegionDCL** for making their code publicly available.  


## Usage
This repository includes only the updated integration components. To run the complete pipeline, please first clone the original repositories:

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

## Acknowledgements
This work builds upon and extends the following repositories:
- SpaBERT: https://github.com/knowledge-computing/spabert
- RegionDCL: https://github.com/LightChaser666/RegionDCL

We thank the original authors for their open-source contributions, which made this research possible.

## Citation
If you use this work, please cite both our paper and the foundational repositories:
```
@inproceedings{li-etal-2022-spabert,
    title = "{S}pa{BERT}: A Pretrained Language Model from Geographic Data for Geo-Entity Representation",
    author = "Li, Zekun  and Kim, Jina  and Chiang, Yao-Yi  and Chen, Muhao",
    booktitle = "Findings of the Association for Computational Linguistics: EMNLP 2022",
    month = dec,
    year = "2022",
    address = "Abu Dhabi, United Arab Emirates",
    publisher = "Association for Computational Linguistics",
    url = "https://aclanthology.org/2022.findings-emnlp.200/",
    doi = "10.18653/v1/2022.findings-emnlp.200",
    pages = "2757--2769"
}

@inproceedings{li2023urban,
    author = {Li, Yi and Huang, Weiming and Cong, Gao and Wang, Hao and Wang, Zheng},
    title = {Urban Region Representation Learning with OpenStreetMap Building Footprints},
    year = {2023},
    isbn = {9798400701030},
    publisher = {Association for Computing Machinery},
    address = {New York, NY, USA},
    url = {https://doi.org/10.1145/3580305.3599538},
    doi = {10.1145/3580305.3599538},
    booktitle = {Proceedings of the 29th ACM SIGKDD Conference on Knowledge Discovery and Data Mining},
    pages = {1363–1373},
    numpages = {11},
    keywords = {urban regions, representation learning, openstreetmap, geospatial data mining},
    location = {Long Beach, CA, USA},
    series = {KDD '23}
}
```
