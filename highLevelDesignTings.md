# High level design stuff

## Things to know

### When Caching

- low  ttl implies high misses
- high TTL implies low consisetency ( meaning high chance data might get stale)

### SQL vs NoSQL

- NoSQL is better for sharding
- NoSQL is good for write heavy systems
- SQL is better for read heavy systems

### Problems with S3 storage

- it takes a while to download/updload files. This is indeed why there's a cache.

### About Lazy invalidation

- it cannot be done on the file name as it is needed for identification purposes.

## CAP Theorem

### Understanding the CAP acronym

- Your system can be characterized by three major benchmarks.
  1. **Consistency**: its about making sure that data is accurate to end users
  1. **Availability**: it's about making sure that the system is always available to the user
  1. **Partitioning tolerance**:its about making sure that the system is available and consistent despite having components on different servers.
- Note: These benchmarks are in the name of the theorem.

### Explanation of the CAP Theorem

- The theorem pretty much mentions how systems systems ( mostly distributed systems) can focus on two out of the three benchmarked characteristics, but not all three.
  - ex:  Consistency and Availability , Consistency and Partitioning tolerance,  Availability and Partitioning tolerance
- Note: in distributed systems , Consistency and Availability does not exist. We usually deal with CP or AP.

## Extening CAP Theorem ( ie PACELC)

### Understanding the PACELC acronym

- Basically the PAC stands for the same characteristics mentioned inside of CAP. The E is for else. and the LC is for
  - Latency
  - Consistency again

### Explanation of the PACELC theorem

- Basically its stating that when we have a partition tolerant system, we can only have AP or CP. Otherwise ( that's where the else comes in), we remove the partitioning tolerance and focus on Consistency and Latency.
  - We can have a few scenarios
    - High consistency  and Low latency
    - High Latency and low consistency
    - High consistency and High latency

## Master slave architectures and PACELC

### about master slave

- All nodes ( or components) can read and only the master writes. The master basically updates all the slaves

### Low latency scenario

- It goes as follows:
  - Client sends write request.
  - The master writes.
  - The master responds to client.
  - The master eventually updates slaves after returning to client
- Note: this involves **low consistency**

## Low latency + (perhaps medium ) consistency scenario

- It goes as follows:
  - Client sends write request.
  - The master writes.
  - The master updates only one slave.
  - The master responds to client.
  - The master eventually updates slaves after returning to client

## High consistency scenario

- It goes as follows:
  - Client sends write request.
  - The master writes.
  - The master updates all slaves.
  - The master responds to client.
- Note: this involves **low latency**

## Messaging app case study

### The MVP

#### Functional requirements

- Send a message to recipient
- See the message history
- See the recent conversations
- Real time chat

#### Estimations

- There are 20 billions of messages/day
- Size o the message can be around 200 bytes when you consider:
  - from : int ( 8 bytes)
  - to   : int ( 8 bytes)
  - content : text
  - timestamp : 4 bytes
  - attachements
  - subject  
- In the end. the storage needed could be:
  - 20 billion/day *  200 bytes  which would be 4 TB/day
  - Clearly, sharding will be needed

#### PACELC  goals

- We want high consistency and low latency.
- This is clearly a violation of the PACELC theorem.

#### Double send phenomenon

- it happens when a client woudl send a message twice due to lack of ACKs

#### API

- sendMessage(from,to, text)
- getMessages(conversationId,userId)
- getConsersations(userId)

#### Sharding

- It can be done by user_id or conversation_id
  - you would favor  conversation id if dealing with group chats
  - you would favor user id if dealing with 1-1 chats

## HDFS

- **HDFS** is used to save a file on multiple machines.
- Basically there are chunks. Each chunk could be the size of 128 Mb (or any size based on performance)
- CAPELC
  - Consistency over availability. ( this is  a file that we're talking about)
  - Note: there are different replicas.
- Disaster recovery is implemented using the rack-aware algorithm.
  - Note: each rack has multiple machine, and we store chunks in different nodes.

## Streaming

- The file can be downloaded in chunks
- Steps at writing
  1. client streams file to app server
  1. app server gets chunk size from NNS (ie name node server)
  1. check if buffer is full
  1. store data in NNS
  1. store data in data node

- Steps at reading
  1. app server receives request
  1. app server talks to NNS
  1. Appsserver asks data node for data
  1. App server sends chunks to client.  

## Nearest neighbor

- you implement quarding algorithm to divide your map into different grids. You do it based on the desired amount of points that you'd like to have inside of your grid.
- the grids are used to optimize the list of nearest neighbours when you are given a point.