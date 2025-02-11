# Introduction to Data Engineering

## What is it?

- It is the process of designing and building systems to collect, store, and analyze large amounts of data.
- Data engineers are heavily needed in systems that generate large amounts of data.

## Data Engineers vs. Data Scientists

| **Data Engineer** | **Data Scientist** |
|--|--|
| They build pipelines that perform ETL for data scientists. | They take transformed data and perform analysis and machine learning. |
| **Skills needed:** | **Skills needed:** |
| Infrastructure, Databases (DB), Data Warehouses (DWH), design pipelines, ETL tools, Java, Python, Big Data processing tools (Spark, Hadoop, Databricks, Snowflake) | Java, Math (Linear Algebra, Calculus, Matrices), Machine Learning & AI libraries (TensorFlow, PyTorch), Big Data technologies, Databases |

## Challenges that Data Engineers Face

### 6 Vs

The 6 Vs are:

1. **Volume**
2. **Variety**
3. **Value**
4. **Veracity**
5. **Velocity**
6. **Variability**

#### 1. Volume

It's about how much data is going to be stored.

#### 2. Variety

It's about the type of data. For example, it could come from a database, JSON, or video.

There are three types of data variety:

- **Structured data** consists of organized data like relational databases.
- **Semi-structured data** consists of loosely organized data like JSON, CSV, or XML.
  - Note: CSV is considered semi-structured because, although it has a tabular format, its schema is flexible and can change.
- **Unstructured data** consists of data that does not follow a defined framework.
  - Examples: Videos, images, audio, PDFs.

The new trend in data engineering is dealing with unstructured data.

#### 3. Value

It's about the usefulness of data in decision-making.

#### 4. Velocity

It's about the speed at which data is generated.

There are two categories of data velocity:

- **Batch processing**: When we know the size of the data before processing it.
- **Streaming**: When data flows continuously (24/7) to feed analytics. This can be critical.

#### 5. Veracity

It's about how accurate and trustworthy the data is.

#### 6. Variability

It's about the changing nature and inconsistency of data.

## ETL

ETL stands for **Extract, Transform, Load**.

- **Extract**: Retrieve data from source systems.
- **Transform**: Cleanse and modify data to meet operational needs.
- **Load**: Store the transformed data in a target system.

## Cluster, Node, Instance

- **Instance**: A physical or virtual machine (e.g., a VM in the cloud).
- **Node**: An instance that runs a specific software for processing or storage.
- **Cluster**: A group of interconnected nodes working together.
