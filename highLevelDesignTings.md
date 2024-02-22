# High level design stuff

## Things to know

### When Caching

- low  ttl implies high misses
- high TTL implies low consisetency ( meaning high chance data might get stale)

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