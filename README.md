# st20357373_DAS7002PRAC1
Big Data Technologies (DAS-7002) - Practical Project – PRAC 1
---
# What this project does
1. Task 1 — ETL: Schema-enforced ingestion, data-quality cleaning, and a Year/District partitioning strategy over Parquet.
2. Task 2 — EDA: Rolling crime-rate averages (Spark Window functions), a broadcast join against socio-economic data, and a weather correlation analysis using daily NOAA station records.
3. Task 3 — Clustering: K-Means spatial-temporal clustering (latitude, longitude, cyclically-encoded time-of-day) with Elbow Method and Silhouette Coefficient model selection.
4. Task 4 — Prediction: A Random Forest classifier predicting arrest likelihood, with full evaluation (confusion matrix, precision/recall/F1, ROC-AUC) and a reflection on class-imbalance (data skew) effects.
---
# Prerequisites
* Windows 10/11	
* Anaconda (Python + Jupyter)	- Python 3.11+
* Java (JDK) - JDK 11 
* PySpark	- 4.2.0
---
# Datasets required (not included in this repo due to size)
- `Crimes_-_2001_to_Present.csv`	- https://www.kaggle.com/datasets/utkarshx27/crimes-2001-to-present 
- `socioeconomic_indicators.csv`	- https://data.cityofchicago.org/Health-Human-Services/Census-Data-Selected-socioeconomic-indicators-in-C/kn9c-c2s2/about_data
- `USW00014819.csv`	NOAA GHCN-Daily - https://www.ncei.noaa.gov/
 <br>
 <b/>Place all three files in `data/raw/` before running (see project structure below).</b>
 <br>
 
---
# Windows setup
Spark's file-system layer depends on a small Hadoop utility that isn't included
on Windows by default. Skip this section entirely on Mac/Linux.
1. Install Java 11+
Download from Oracle
and install with default options.
Verify: `java -version` in Command Prompt.
2. Install PySpark
```
   pip install pyspark
   ```
If Jupyter still can't find it afterwards, run this from inside a notebook cell instead:
```python
   import sys
   !{sys.executable} -m pip install pyspark
   ```
3. Download `winutils.exe` and `hadoop.dll`
From kontext-tech/winutils
(`hadoop-3.3.5/bin/` folder), download both files.
4. Place the files:
- Create `C:\hadoop\bin\` and put both files there.
- Also copy `hadoop.dll` into `C:\Windows\System32\` (requires admin permission).
5. Set environment variables inside your notebook (more reliable than
Windows system-level env vars, since they don't always persist across
restarts). Add this as the first cell of every notebook, before
creating the SparkSession:
```python
   import os
   os.environ["HADOOP_HOME"] = "C:\\hadoop"
   os.environ["PATH"] = "C:\\hadoop\\bin;" + os.environ["PATH"]
   ```
---
Project structure
```
chicago_crime_project/
├── data/
│   ├── raw/                          # place the 3 source CSVs here (see above)
│   └── processed/
│       └── crimes_partitioned/       # Spark writes this — Parquet, partitioned by Year/District
│       
├── notebooks/
│   └── 01_etl_pipeline.ipynb         # full pipeline: Tasks 1-4 in one notebook
├── outputs/

```

Author </br>
H M P M Herath </br>
Student ID: st20357373 — DAS7002 Big Data Technologies
