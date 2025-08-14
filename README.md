# Distributed Consensus with Raft

 Due to academic integrity, the project source code and detailed report are private. This public summary outlines the core objectives, challenges, and achievements. Code/reports cannot be shared, even on request.

## Project Overview

This project implements a distributed consensus protocol using the Raft algorithm within the DSLabs framework. The goal was to design a fault-tolerant, replicated state machine that maintains strong consistency across a group of servers, even in the presence of network failures or server crashes.

I chose to implement Raft over Paxos due to its clarity, modularity, and practical advantages in real-world systems. Raft's leader-based approach enables efficient log replication with a single round-trip time (RTT) for steady-state client operations, amortizing the cost of leader election over many log entries. This design choice reflects industry trends favoring leader-based consensus for its operational simplicity and performance.

## Problem Statement

- Achieve consensus on a sequence of client commands across a fixed set of servers.
- Ensure linearizability and fault tolerance: the system must remain available and consistent as long as a majority of servers are operational and can communicate.
- Support log compaction (garbage collection) to prevent unbounded memory growth.
- Handle unreliable networks, message loss, and server failures (excluding persistent storage).

## High-Level Design

- **Raft Consensus Protocol:** Implemented leader election, log replication, and safety mechanisms as described in the Raft paper.
- **Leader-Based Replication:** Only the elected leader processes client requests and coordinates log replication, minimizing coordination overhead in the common case.
- **Fault Tolerance:** The system tolerates failures of minority servers and recovers from network partitions, ensuring progress and consistency.
- **Garbage Collection:** Periodically compacts the replicated log once entries are committed and applied by all servers.
- **Testing & Verification:** Passed all DSLabs-provided tests for safety, liveness, and correctness, including scenarios with network partitions and server failures.

## Key Learning Outcomes

- Deepened understanding of distributed consensus, fault tolerance, and the trade-offs between Paxos and Raft.
- Gained hands-on experience with the DSLabs framework for modeling and testing distributed protocols.
- Developed skills in designing robust, maintainable distributed systems with clear separation of concerns.
- Practiced rigorous testing and debugging in adversarial network conditions.

## Why Raft?

Raft was selected over Paxos for its approachable design and strong documentation, which enabled a more modular and understandable implementation. Raft's leader-based approach streamlines steady-state operation to a single RTT per command, with the cost of leader election amortized over many log entries. This makes Raft particularly well-suited for practical systems where throughput and maintainability are critical.
