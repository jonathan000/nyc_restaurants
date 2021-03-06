# Exploratory Analysis of DOHMH New York City Restaurant Results

## Overview

This project explores the `DOHMH New York City Restaurant Inspection Results` dataset. Scripts are used to:
* Automate download of the `DOHMH New York City Restaurant Inspection Results` dataset and its subsequent upload to s3 (luigi pipeline tasks `nyc_inspection_to_csv` and `nyc_inspection_to_s3`)
* Automate download of complementary Yelp business data in incremental runs, and its upload to s3 (luigi pipeline task `yelp_business_data_to_s3`)
* Highlight certain trends in the NYC City Restaurant Inspection Results dataset, and enrich the analysis using Yelp business data (R script `nyc_restaurant_exploration`, see html report link below)

## Datasets

* DOHMH New York City Restaurant Inspection Results
https://catalog.data.gov/dataset/dohmh-new-york-city-restaurant-inspection-results

* Yelp Dataset
https://www.yelp.com/developers/documentation/v3/get_started

Note: For a Yelp API key, see: https://www.yelp.com/developers/

## Data Story

https://s3.amazonaws.com/nyc-restaurants-20180203/output/nyc_restaurant_exploration.html

## Setup Details

### Python Setup

* Install `virtualenv` https://virtualenv.pypa.io/en/stable/installation/
* Create a Python 3 virtual environment called `venv` in project root directory
* Run: `pip install -r requirements.txt` within the activated virtual environment
* If modifying a script and adding a new package, make sure to update the `requirements.txt` file: `pip freeze > requirements.txt`
* Environment variables can be accessed several ways, on way is to use a `.env` file, then `source .env`. Format:

```
export VARIABLE_ONE_NAME=VARIABLE_ONE_VALUE
export VARIABLE_TWO_NAME=VARIABLE_TWO_VALUE
```

### R Setup

This repo uses a combination of Packrat and Pacman R libraries for package management.
* Packrat: https://rstudio.github.io/packrat/
* Pacman: https://cran.r-project.org/web/packages/pacman/vignettes/Introduction_to_pacman.html

### AWS Setup

* Python package `boto3` documentation: https://boto3.readthedocs.io/en/latest/guide/quickstart.html
* R `aws.s3` documentation: https://cran.r-project.org/web/packages/aws.s3/index.html

### Pipeline

Tasks are managed using the command line and Luigi (https://luigi.readthedocs.io/en/stable/)
* In your virtual environment type `luigid`
* Then, in a separate command line window, run tasks found in `pipeline.py`, using `python3 -m luigi --module pipeline [TASK_NAME]`
* To run the Rscript, type `Rscript [FILEPATH]` (datasets in s3 required)
