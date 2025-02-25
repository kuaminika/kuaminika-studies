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

[//]: <> (TODO: put architecture diagram.)

# File Formats

1. Text  
2. Sequential  
3. Avro  
4. Parquet  
5. ORC  

**Note:** Text and Sequential are considered legacy formats.

---

## AVRO File Format

AVRO is a **serialization format** used for data storage and exchange.

### Data Types in AVRO  

(*These data types are used when defining schemas.*)

- **Record**: Analogous to a table.  
- **Enum**: Represents a specific set of values.  
- **Array**: All elements must be of the same type.  
- **Map**: Key-value pairs.  
  - Keys must be **strings**, while values can be of any type.  
- **Fixed**: A fixed number of 8-bit unsigned bytes.  

### Other Facts  

- In an AVRO file, the first row contains the **schema**, represented in JSON.  
- Apache AVRO provides **JAR tools** to create and process AVRO files.  
- **Fun fact:** AVRO files can hold **billions** of records.  
- When creating a table in Hive, you must configure the **SERDE** (Serialization & Deserialization) settings.  

---

## Managed Table vs External Table in Hive  

### **Managed Table**  

- No additional keywords are needed when creating a table.  
- Both **metadata** and **HDFS storage** are managed by Hive.  

### **External Table**  

- Must use the `EXTERNAL` keyword when creating the table.  
- Only the **metadata** belongs to Hive; the data remains external.  

**Note:**  

- Deleting a **managed table** removes both **metadata** and **data**.  
- Deleting an **external table** removes only **metadata**, while the actual data remains intact. 