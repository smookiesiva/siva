# STEDI Human Balance Analytics: AWS Data Lakehouse
**📌 Project Overview**
The STEDI Team is developing a hardware/software solution to help users train their balance. This project implements a Data Lakehouse on AWS to process and curate data from two primary sources:

STEDI Step Trainer: A motion sensor that records distance.

STEDI Mobile App: An accelerometer that tracks motion in X, Y, and Z axes.

The goal is to produce a privacy-compliant, aggregated dataset that Data Scientists can use to train a Machine Learning model for real-time step detection.

## 🛠️ Technical Stack
Storage: Amazon S3

Processing: AWS Glue (PySpark), Glue Studio

Analysis: Amazon Athena (Presto-based SQL)

Schema Management: AWS Glue Data Catalog

Infrastucture: Python, Spark SQL

## 🏗️ Data Architecture
The pipeline follows a three-tier architecture to ensure data quality and strictly enforce privacy requirements.

1. Landing Zone (Raw Data)
Raw JSON data is ingested from the STEDI website and IoT sensors into S3.

Customer Records: Fulfillment data containing serialNumber and shareWithResearchAsOfDate.

Step Trainer Records: Time-series IoT data (sensorReadingTime, distanceFromObject).

Accelerometer Records: Mobile app logs (timeStamp, user, x, y, z).

2. Trusted Zone (Sanitized Data)
In this layer, we filter data to comply with user privacy settings.

Privacy Filter: Only records from customers who agreed to share data for research purposes (shareWithResearchAsOfDate != 0) are propagated.

Validation: Use AWS Athena to verify that no PII or non-consented data exists in this layer.

3. Curated Zone (ML-Ready Data)
The final layer where data is joined and aggregated for the ML model.

Join Logic: We align Step Trainer readings with Accelerometer readings based on matching timestamps.

Constraint: Only users who have both valid accelerometer data and research consent are included.
