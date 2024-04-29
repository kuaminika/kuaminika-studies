# various points about High level design

- a messaging System uses app servers as caches because it helps with concurrency by being able to write locks on user data to ensure sequential writes.

- to ensure high consistency, it's important ot write  to the recipient's databse first, then the sender's

- systems like SLACK or messenger are both read heavy and write heavy because they need to handle message storage, and retrieval and real time delivery.

- In the context of storing files in chunks, the challengs of dividing files into smaller chunks are:
  - collation of chunks _(i.e when you bring the chunks together to build the file)_
  - High metadata overhead
  - slow download speads

- variable sized grids are preferred for location based systems to optimize query performance in dense and parse areas

- a primary advantage of using a quadtree for spacial data is that it efficiently handles dynamic changes in data.

- in an e-commerce platform that frequently experiences high traffic during sales events and has a diverse product catalog,the product_id is a good option for sharding

- In a multimaster distributed database system, given that:
  - R _( i.e minimum reads)_
  - W _(i.e minimum number of writes)_
  - we know that R+W <= X because x is the maximum amount of transactions
  - In the end.
    - If R = X, then you best believe the system is highly available
    - If R+W is high then the system is highly consistent

- kafka ensures that messages with the same key ends up in the same partition by hashing the  key to determine the partition

- Zookeeper reduces the need for contiuous queries to find out who the master is in by setting watches on nodes.

- In HDFS, the namemode server primarily stores information about file meta data and dta role locations.

- HDFS uses the rack awareness algorithm to  improve fault tolerance hen data is stored in different machines

- Uber uses client side handling of location changes to optimize  quad tree cab movements.

- the advantage of Dynamic ranges for grid updates in uber is that it adapts to varying densities.
