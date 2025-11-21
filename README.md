Hackathon Part A – Pipeline Design
Objectives

In this exercise, you will:

    Design and implement a modular Python data pipeline to process multiple related datasets.
    Use Pandas and other tools to ingest, clean, transform, and merge real-world data.
    Generate a minute-by-minute temperature estimate for 2012 using a model based on daily weather summaries.
    Document your pipeline logic, assumptions, and outputs clearly for reuse by other developers.

Overview

You have been provided with two zipped files in the folder PartA_Data.
The first contains data about the time of sunrise, sunset and the length of the day in Edinburgh.
The second contains weather data from a weather station in Scotland.

Your goal is to build a Python data pipeline that merges these sources, models temperature changes over time, and outputs a synthetic dataset estimating temperature every minute for 2012.
This data will later be used to analyse electronic equipment performance under environmental stress.
Pipeline Structure

Your repository should contain the following:

/data-pipeline-hackathon/
│
├── data/
│ ├── Edinburgh-daytime.xlsx
│ └── Strathspey-weather.xlsx
│
├── pipeline/
│ ├── ingest.py
│ ├── clean.py
│ ├── transform.py
│ ├── merge.py
│ └── resample.py
│
├── output/
│ └── merged_summary.csv
│
├── main.py
└── requirements.txt

Each module should perform a clear function:

    ingest.py – reads Excel data, handling multiple worksheets dynamically.
    clean.py – removes empty rows, fixes headers, and standardises column names.
    transform.py – converts date fields and derives useful numerical values.
    merge.py – joins astronomical and weather data on date.
    resample.py – interpolates daily data to one-minute intervals using a sinusoidal temperature model.

Temperature Estimation Model

To estimate temperatures between the daily minimum and maximum, use a sinusoidal model:

[ T(t) = T_{avg} + A \cdot \sin\left(\frac{\pi (t - t_{peak})}{12}\right) ]

Where:

    ( T_{avg} ) is the average of daily min and max temperature.
    ( A ) is half the difference between max and min.
    ( t_{peak} ) is the hour of peak temperature, typically around 15:00.

This generates a smooth temperature curve that peaks mid-afternoon and reaches its minimum near dawn.
Output

Your final dataset should:

    Contain 527,040 rows (one per minute from midnight 31 December 2011 to 23:59 on 31 December 2012).
    Include columns for datetime, estimated_temp, and optionally metadata such as Location.

Deliverables

    Working pipeline – all stages functional and reproducible.
    Test process – confirm row counts and data consistency.
    Code quality – meaningful variable names and clear comments.
