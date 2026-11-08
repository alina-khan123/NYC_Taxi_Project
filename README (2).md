This is the NYC Taxi Record project for CSCI316!

PROJECT STRUCTURE

app/
├── scripts/                        # Our jupyter notebooks
    ├── eda.ipynb                           # Exploratory Data Analysis using Pandas and Sklearn
    ├── preprocessing.ipynb                 # Data wrangling and feature engineering
    └── models.ipynb                        # OLS, Regression DT w/ Grid Search CV, Bagging Ensemble
├── data/                           # Our parquet files
    ├── yellow_tripdata_2025-01.parquet
    ├── yellow_tripdata_2025-02.parquet
    ├── yellow_tripdata_2025-03.parquet
    └── taxi_data_final.parquet             # Final output of preprocessing.ipynb
├── requirements.txt                # Packages required for this project
└── Dockerfile                      # The build instructions for Docker


HOW TO DOWNLOAD WITH DOCKER

Option A: Pull from DockerHub
1. Make sure you have Docker installed
2. In terminal, move from your current directory to the project directory
3. Run this line in your terminal to pull the image: docker pull mgkh/taxi-project-csci316
4. Run this line to containerize the image: docker run -it --rm -p 8888:8888 -p 4040:4040 -e SPARK_CORES=4 -m 8g --name taxi-test taxi-project-csci316

Option B: Build the image manually
1. Make sure you have Docker installed
2. In terminal, move from your current directory to the project directory
3. Run this line in your terminal to build the image (command prompt preferred on Windows): docker build -t taxi-project_csci316 .
4. Run this line to containerize the image: docker run -it --rm -p 8888:8888 -p 4040:4040 -e SPARK_CORES=4 -m 8g --name taxi-test taxi-project-csci316
5. Once the container is up and running, you can find at the terminal two browsers URLs to open the project in Jupyter

(!!!) IMPORTANT CONSIDERATIONS: 
"-e SPARK_CORES=" sets the amount of cores that will be used in Spark. I recommend to not go over 10: model metrics may start behaving oddly because of excessive partitioning. Default cores number is set to 8.
"-m 8g" sets the amount of memory given to a container. Our application uses 6gb memory, which is why we set the container memory to 8gb. So there is a memory constraint. 

Our docker image is built on python_3.11:slim version from Docker Hub. Spark version 3.5.1
Apart from the packages mentioned in requirements.txt, we also install JRE21 (Java Runtime Environment) to slim down on the image size.

Once the container is running, you can monitor Spark performance at:
JupyterLab: http://localhost:8888
Spark UI: http://localhost:4040

NOTES
- preprocessing.ipynb should be ran before models.ipynb. However, a combined and cleaned parquet file is already given in the data folder, so models.ipynb can be ran independently. 
- You can visit the link in the end to see the source of data. We downloaded three months from year 2025, but you can download whichever month and year you wish. Just place them in data and rerun the scripts (but they must start with "yellow_tripdata").

Our project used NYC TLC Trip Record Data. 
https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page
