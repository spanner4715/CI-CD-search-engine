# CI-CD-search-engine

## Overview  
Keep doing CI/CD when new data being added to the content database. Minimize the effect from customer's experience

## Pre-requisites  
1. Set up AWS EC2 
2. Install docker and docker-compose  
3. Search engine is running

## Project workflow
![image](https://user-images.githubusercontent.com/103509243/219421700-9623e34a-4c6a-4856-a2f9-790118ea8089.png)

* data
  
  * project_mappings.csv - Index mapping for every project

* output

  * search.index - FAISS object for inference

* src

  * dataset.py - python script to fetch datasets from MongoDB
  * embeddings.py - python script to create embeddings using SBERT
  * processing.py - python script to preprocess data 
  * query_search.py - python inference script to generate search results
  * utils.py - python script for generating overall dataset

* app.py - streamlit app python script

* engine.py - creates embeddings for the overall projects text data and generates and saves index (FAISS object) for inference.


### Execution Steps:

* Install requirements with the command "pip3 install -r requirements.txt"

* Run engine.py to create embeddings and save the FAISS object with the command "python3 engine.py"

* Run app.py with the command "streamlit run app.py"
