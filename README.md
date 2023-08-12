# Real-Time Sentiment Analysis Pipeline with Kafka, PySpark, MySQL, and Tableau

This project demonstrates how to use Kafka, PySpark, and MySQL to process and store real-time streaming data. In this example, we will be working with Twitter data ie tweets related to chatgpt, and classify them into 3 categories namely Positive, Negative, and Neutral.

We will be using the following dataset: https://www.kaggle.com/datasets/khalidryder777/500k-chatgpt-tweets-jan-mar-2023. We will be preprocessing this dataset with the steps mentioned in the **data_cleaning.ipynb** and then using it later.

### Prerequisites
  1. Anaconda
  2. Apache Kafka
  3. Apache Spark
  4. MySQL Server

### Setup

**1. Create and activate an Anaconda environment named bigdata with Python 3.7 and the required packages:**

      conda create -n bigdata python=3.7
      conda activate bigdata
      pip install pyspark Kafka-python pandas textblob mysql-connector-python pymongo
      set PYSPARK_PYTHON=%CONDA_PREFIX%\python.exe

**2. Start Zookeeper:**

      zookeeper-server-start.bat ..\..\config\zookeeper.properties

**3. Start Kafka:**

      kafka-server-start.bat ..\..\config\server.properties

**4. Start the Kafka consumer:**

      kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic big_data_project --from-beginning
      
**5. Run the Kafka producer:**

      python kafka_producer.py

**6. Run the PySpark job:**

      spark-submit --packages mysql:mysql-connector-java:8.0.28,org.apache.spark:spark-sql-kafka-0-10_2.12:3.0.1 .\spark_streaming.py

**7. Create a MySQL database named big_data_project and a table named tweets with the following schema:**

      CREATE TABLE tweets (
    date VARCHAR(255),
    id VARCHAR(255),
    content TEXT,
    username VARCHAR(255),
    like_count VARCHAR(255),
    retweet_count VARCHAR(255),
    timestamp TIMESTAMP NULL,
    processed_text TEXT,
    subjectivity FLOAT,
    polarity FLOAT,
    sentiment VARCHAR(255));

After completing these steps, the data should be successfully processed and stored in the tweets table. You can verify this by running a SELECT * FROM tweets; query in MySQL.

**8. You can connect your tableau with MySQL and make visualization of positive, negative and neutral tweets**
