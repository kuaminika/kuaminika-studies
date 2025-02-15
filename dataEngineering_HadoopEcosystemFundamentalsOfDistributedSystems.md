# Hadoop Ecosystem: Fundamentals of Distributed Systems

## Challenges of Traditional Systems

- **Data Sizes**: Handling large volumes of data (e.g., managing heavy data content).
- **Unstructured Data**: Managing non-traditional data formats like videos and images.
- **Scalability**: Choosing between horizontal and vertical scaling.
  - **Horizontal Scaling** is implemented using **distributed systems**.
  - **Distributed Systems**: A model where components located on networked systems communicate and coordinate actions by passing messages.

---

## Challenges of Distributed Systems

- **System/Node Failure**: Ensuring the system remains functional even if a node fails.
- **Limited Bandwidth**: Minimizing latency to ensure seamless operation despite bandwidth constraints.
- **High Programming Complexity**: Managing the increased complexity of developing and maintaining distributed systems.

---

## Hadoop

Hadoop is a tool designed to address the challenges of distributed systems.

- **Hadoop** is a framework that enables distributed processing of large datasets across clusters of computers using simple processing models.

---

### Characteristics of Hadoop

- **Handling System Failures**: Data is distributed across multiple servers to ensure fault tolerance.
- **Scalability**: Supports both horizontal and vertical scaling.
- **Open Source**: Freely available and modifiable.

---

### More Facts on Hadoop

- The **master node** distributes executables to all **slave nodes**.
- Each node processes data using assigned jobs, known as **processing engines**.

---

### Core Components of Hadoop

Most systems rely on these major components:

- **RAM**
- **CPU**
- **Hard Disk**

Hadoop’s major components include:

- **HDFS**: Acts as the hard disk for distributed storage.
- **YARN**: Handles resource management.
- **Spark**: Used for MapReduce operations.

---

### More Facts on HDFS

- In HDFS, the default **replication factor** is **3**, and the default **block size** is **128 MB**.
- The **master node** (NameNode) stores file metadata and coordinates block distribution to **slave nodes** (DataNodes).
  - Note: The master node does **not** store actual data.
- If the replication factor is **3**, all three DataNodes will store all blocks of a file.
- If the number of replicas (DataNodes) exceeds the replication factor, some replicas may not store all blocks.
  - Deletion of excess block copies will occur.
- In HDFS 2.0, there's a second master node that is present as _standby_.
  - **Zookeeper** is responsible for managing multiple masters. It also informs slaves if the master has changed.
  - **Zookeeper** has the role of electing the leader in case of a failure.

- HDFS implements **Quorum-based storage**.
- In HDFS, metadata is shared across multiple masters. This is done with a component called **Journal Nodes**.
  - **Journal Nodes** keep the passive NameNode (aka standby master) in sync with the active NameNode.

- **NameNodes** are the core components of the HDFS cluster.
  - They store metadata for each file that is created.
  - Metadata consists of two data structures:
    - **FSImage** (File System Image):
      - It is essentially a snapshot of the file system. You can expect to see paths like `/var/...` or `/etc/...`.
    - **Edit Logs**: Sequential transaction logs that record every metadata change in HDFS.
  - In summary, NameNodes = File System (FSImage) + Edit Logs.