# Cloud Data Warehouse – Sparkify ETL Pipeline
**This project builds a scalable AWS Redshift Data Warehouse and ETL pipeline for Sparkify, a music streaming startup. The goal is to transform raw JSON song metadata and user activity logs stored in Amazon S3 into a structured analytics-ready star schema hosted in Redshift.**

##Project Overview
**Sparkify’s data—song metadata and user activity logs—is stored in Amazon S3. To support business analytics, this project creates:**

##Staging tables (copying raw data from S3 → Redshift)
**A star schema (fact + dimension tables)
A Python-based ETL pipeline

The final warehouse allows for insights such as user listening patterns, most played songs, popular artists, and session trends.

DatasetS3 LocationSong Datas3://udacity-dend/song_dataLog Datas3://udacity-dend/log_dataJSON Path Files3://udacity-dend/log_json_path.json
Song Dataset

JSON files containing metadata about songs and artists
Partitioned by the first 3 letters of the song’s track ID

Log Dataset

App activity logs (JSON format)
Partitioned by year and month
Includes user actions; only NextSong events are used for analytics


Data Model (Star Schema)
Fact Table: songplays
Records of song play events.

Dimension Table

users – App users
user_id, first_name, last_name, gender, level

songs – Song information
song_id, title, artist_id, year, duration

artists – Artist details
artist_id, name, location, latitude, longitude

time – Timestamp breakdown
start_time, hour, day, week, month, year, weekday


Project Structure
.
├── create_tables.py      # Creates and resets tables on Redshift
├── etl.py                # Loads data from S3 → staging → final tables
├── sql_queries.py        # SQL commands for DDL, staging, inserts
├── dwh.cfg               # Configuration (Redshift & IAM role info)
└── README.md             # Project documentation


Environment Requirements

Python 3.11.0
AWS Redshift Cluster
IAM Role with S3 read access and Redshift permissions

How to Run the Project
Create a Redshift Cluster
You will need:

HOST
DB_NAME
DB_USER
DB_PASSWORD
DB_PORT
IAM Role ARN with S3 read permissions


 Configure the dwh.cfg File
Fill the file as follows:
[CLUSTER]
HOST=
DB_NAME=
DB_USER=
DB_PASSWORD=
DB_PORT=

[IAM_ROLE]
ARN=


Create Database Tables
Run the script to drop existing tables and recreate fresh ones:
Shellpython create_tables.py``Show more lines

Run the ETL Pipeline
Execute the ETL process:
Shellpython etl.pyShow more lines
This will:

Copy raw JSON data from S3 → Redshift staging tables
Transform and insert data into analytics tables


 Project Output
Once complete, your Redshift cluster will contain:
Staging Tables

staging_events
staging_songs

Fact Table

songplays

Dimension Tables

users
songs
artists
time**