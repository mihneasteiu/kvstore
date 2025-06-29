# Concurrent and Distributed Key-Value Store

This repository contains my implementation of a concurrent and distributed key-value store, developed as part of the **[CSCI 0300 (Fundamentals of Computer Systems)](https://csci0300.github.io)** course at Brown University. You can find more information about the project at these two links: [Part A](https://csci0300.github.io/assign/projects/project5.html) and [Part B](https://csci0300.github.io/assign/projects/project6.html).

The project is split into two parts:

---

## Concurrent Store

A multi-threaded key-value store supporting the following operations:
- `get`, `put`, `append`, `delete`
- `multiget`, `multiput`

### Technical Highlights
- **Thread Safety:** Used `std::mutex` and `std::shared_mutex` to implement both coarse-grained and fine-grained locking.
- **Bucket-Based Store:** Internal structure based on a fixed-size hash table (`DbMap`) with per-bucket locks.
- **Atomic Multi-Key Operations:** Ensured consistency and isolation across multi-key requests.
- **Performance:** Met required 2x throughput over the sequential version through parallelism and reduced lock contention.

---

## Distributed Store

Extended the key-value store to a sharded distributed system across multiple servers.

### Components
- **Shardcontroller:** Central service maintaining shard-to-server mappings (`Join`, `Leave`, `Move`, `Query` operations).
- **Server:** Automatically registers with the shardcontroller, migrates shard data on reconfiguration, and handles client requests.
- **Client:** Routes each request to the appropriate server(s) based on the latest shard configuration.

### Technical Highlights
- **Key-Based Sharding:** Mapped keys to shard ranges and routed requests accordingly.
- **Dynamic Reconfiguration:** Servers transfer and delete shard data on reassignment.
- **Thread-Safe Controllers:** Ensured concurrent access to configuration metadata using locking.
- **Networked Communication:** Used structured RPC-style request-response between clients, servers, and the shardcontroller.

---

## Note
To comply with Brown’s academic code, this repository does not include the source code. If you are a potential employer and would like access to my implementation, please contact me at **mihnea_steiu@brown.edu**.
