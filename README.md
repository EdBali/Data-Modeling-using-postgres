Project: Data Modeling with Postgres
by Eddie Wamutu Balibali, 12 October 2020

 # INTRODUCTION
A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

They'd like a data engineer to create a Postgres database with tables designed to optimize queries on song play analysis. His role is to create a database schema and ETL pipeline for this analysis. He'll be able to test his database and ETL pipeline by running queries given to him by the analytics team from Sparkify and compare his results with their expected results.

# PROJECT DESCRIPTION
In this project, I have applied what I've learned on data modeling with Postgres and built an ETL pipeline using Python. To complete the project, I needed to define fact and dimension tables for a star schema , and then I wrote an ETL pipeline that transfers data from files in two local directories into these tables in Postgres using Python and SQL.

# DATASETS:

### SONG DATASET
The first dataset is a subset of real data from the Million Song Dataset. Each file is in JSON format and contains metadata about a song and the artist of that song. The files are partitioned by the first three letters of each song's track ID. For example, here are filepaths to two files in this dataset:

song_data/A/B/C/TRABCEI128F424C983.json 
song_data/A/A/B/TRAABJL12903CDCF1A.json

Below is an example of what a single song file, TRAABJL12903CDCF1A.json, looks like.

{"num_songs": 1, "artist_id": "ARJIE2Y1187B994AB7", "artist_latitude": null, "artist_longitude": null, "artist_location": "", "artist_name": "Line Renaud", "song_id": "SOUPIRU12A6D4FA1E1", "title": "Der Kleine Dompfaff", "duration": 152.92036, "year": 0}

### LOG DATASET
The second dataset consists of log files in JSON format generated by an event simulator based on the songs in the dataset above. These simulate activity logs from a music streaming app based on specified configurations.

The log files in the dataset I  worked with are partitioned by the year and month. For example, here is a filepath to a file in this dataset:

log_data/2018/11/2018-11-12-events.json log_data/2018/11/2018-11-13-events.json


# FILES:
In addition to the data files, the project includes six files:

test.ipynb displays the first few rows of each table to let me check my database.
create_tables.py drops and creates tables. I run this file to reset my tables before each time I run the ETL scripts.
etl.ipynb reads and processes a single file from song_data and log_data and loads the data into the tables. This notebook contains detailed instructions on the ETL process for each of the tables.
etl.py reads and processes files from song_data and log_data and loads them into the tables. It's based on my work in the ETL notebook.
sql_queries.py contains all my sql queries, and is imported into the last three files above.
README.md then provides an introduction to this project


# Extracting and Transforming the Data
The ETL pipeline extracts data from files in two directories:

/data/log_data and
/data/song_data.
It then transforms and loads the data into the five tables of the sparkifydb database. This is handled by four files using Python and SQL:

Running create_tables.py creates and initializes the tables for the sparkifydb database.
Running test.ipynb confirms the creation of my tables with the correct columns.
Running etl.ipynb develops ETL processes for each table and is used to prepare a python script for processing all the datasets.
sql_queries.py contains all SQL queries and is imported into create_tables.py and etl.ipynb
Loading the Data and Running ETL Pipeline
All the code I wrote in etl.ipynb I then used to complete etl.py, which reads and processes all the files from the song_data and log_data directories, and loads them into the sparkifydb database tables.

#### The steps to run the pipeline are as follows:

In a terminal, run python create_tables.py to reset the tables in the sparkifydb database.
Running test.ipynb (in a jupyter notebook) confirms that the tables were successfully created with the correct columns.
In a terminal, run python etl.py to process all the datasets.
Again, running test.ipynb confirms that the records were successfully inserted into each table.
