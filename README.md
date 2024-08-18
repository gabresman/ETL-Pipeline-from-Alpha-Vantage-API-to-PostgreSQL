# ETL-Pipeline-from-Alpha-Vantage-API-to-PostgreSQL

This project implements a complete end-to-end ETL (Extract, Transform, Load) pipeline that retrieves real-time stock price data from the Alpha Vantage API, processes it using Kafka and PySpark, and stores it in a PostgreSQL database. The pipeline aims to simulate a near real-time data processing flow, suitable for analyzing stock prices for future data-driven applications such as analytics dashboards, algorithmic trading models, or financial monitoring systems.

### Project Objective
The primary objective of this project is to build a scalable and automated data pipeline for real-time stock price processing. By integrating multiple technologies—Kafka, PySpark, and PostgreSQL—this project demonstrates how to efficiently collect, process, and store stock price data in a structured and consistent manner, supporting both historical and real-time data analysis.

### General Overview
#### 1. Data Extraction (API Integration):
The stock price data is periodically fetched from the Alpha Vantage API in JSON format. The stock symbol used for this demo is AAPL (Apple Inc.), but the API can support multiple stock symbols. The Python script downloads the data and publishes it to a Kafka topic (stock_prices) for downstream consumption.

#### 2. Message Streaming (Kafka):
Kafka is used as the data streaming platform, with the broker running locally on port 9092. The project initializes a Kafka topic named stock_prices to which the stock price data is published periodically. The project is designed to handle real-time data streaming and can be extended to a distributed Kafka environment for higher scalability.

#### 3. Data Processing (PySpark):
PySpark is responsible for consuming the streaming data from Kafka, parsing the JSON structure, and transforming it into a more structured format suitable for storage. The pipeline processes the data in micro-batches and converts it into a Spark DataFrame with meaningful columns such as timestamp, symbol, open, high, low, close, and volume. This allows for efficient batch processing while maintaining a real-time data flow.

#### 4. Data Storage (PostgreSQL):
After transforming the data, it is inserted into a PostgreSQL table called ohlcv. The project ensures that the data is upserted (inserted or updated if it already exists) using PostgreSQL's ON CONFLICT clause. This guarantees that the data remains accurate, consistent, and up-to-date.

#### 5. Automation and Scalability:
The project employs Spark's foreachBatch function to process each micro-batch of stock data from Kafka and handle it with the process_batch function. This combination allows for seamless and efficient integration between Kafka, PySpark, and PostgreSQL. The pipeline continuously runs, awaiting new data until terminated manually.

### Summary
This project showcases a powerful data pipeline that automates the collection, transformation, and storage of stock price data in a real-time environment. It leverages cutting-edge tools such as Kafka for distributed streaming, PySpark for big data processing, and PostgreSQL for structured data storage. The project pipeline will enable users to analyze large volumes of stock data in real-time.
