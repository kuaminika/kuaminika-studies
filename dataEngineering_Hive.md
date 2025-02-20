# Hive

Hive is an open-source **data warehouse** that can store a vast number of records and process them efficiently.

It is **distributed**, **fault-tolerant**, and enables **analytics at a massive scale**.

Its **UI and SQL-like query language (HiveQL)** make it feel similar to a traditional **DBMS**, simplifying the querying process for users.

## Components Inside Hive

### 1. Hadoop Core
- **HDFS** for storage.
- **MapReduce** for query execution, converting queries into executable tasks.

### 2. Metastore
- A **metadata repository** that can use databases like MySQL or Derby.
- Stores **table information, column names, and data types**.

### 3. Driver
- **Parses and executes queries** by interacting with the query execution engine (e.g., MapReduce, Tez, or Spark).
