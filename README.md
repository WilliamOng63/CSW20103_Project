zxc
#  DistriFly: Enterprise Distributed System Replication Grid

DistriFly is a high-performance distributed systems simulation engine written in Java. The project evaluates the complex trade-offs between data replication techniques (Strong Sequential vs. Eventual Consistency) and network resolution topologies (Flat Distributed Hash Table vs. Hierarchical Structured Naming)[cite: 4, 9]. 

It simulates a concurrent airline flight booking engine across independent cluster nodes, exposing performance metrics under volatile WAN workloads and fault-injection environments.

---

##  System Architecture & Features

* **Multi-Scenario Simulation Framework:** Evaluates runtime infrastructure over three targeted operation modes: `NORMAL`, `HIGH_CONCURRENCY`, and `NODE_FAILURE`.
* **Pluggable Consistency Protocols:** Implements core data synchronization patterns[cite: 2]:
  * **Strong Sequential Consistency:** Leverages a synchronized global commit log, strict sequence tracking, and pessimistic lock management to block race conditions early.
  * **Optimistic Eventual Consistency:** Features a decentralized, background-propagated data scheme utilizing a timestamp duel engine for downstream **First-Write-Wins (FWW)** conflict resolution and active anti-entropy healing[cite: 5].
* **Network Name Resolution Engine:** A simulated naming service backing both linear flat tables modeled after Logarithmic DHT Chord-like hops, and deterministic Tree-based Structured Naming[cite: 9].
* **Virtual Fiber Messaging Topology:** Fully asynchronous, isolated execution threads that communicate via message-passing `Mailbox` layers utilizing randomized latency[cite: 4, 6].

---

##  Project Structure

A quick overview of the key directories and core files in this repository:
* `src/distributedsystem/` - Contains all core simulation engine source code.
  * `DistributedSystem.java` - The main testbench orchestrator deploying and monitoring runtime metrics across 4 distinct configuration combinations.
  * `DistributedNode.java` - Represents an isolated network cluster node capable of processing intercepted packets, managing state image footprints, and executing live hot migrations[cite: 3].
  * `consistencyHandler.java` - Interface defining standard synchronization handlers[cite: 2].
  * `SequentialConsistency.java` & `EventualConsistency.java` - Algorithmic implementations mapping the strict sequencing and optimistic FWW timelines respectively[cite: 5, 11].
  * `NameServer.java` - Manages node registration, routing hops calculations, and random transient WAN network packet drops[cite: 9].
  * `Mailbox.java` & `Message.java` - Asynchronous non-blocking message buffers simulating transport wires[cite: 6, 7].
* `.gitignore` - Verbatim reference tracking to explicitly exclude internal metadata paths (`/nbproject/private/`) and compiled transient targets (`/build/`) from repository history[cite: 1].

---

##  Prerequisites

Before compiling or running the benchmark engine, ensure you have:
* **Java Development Kit (JDK):** Version 8 or higher.
* **IDE Support:** Built natively using NetBeans IDE templates[cite: 2]. Compatible with IntelliJ IDEA or Eclipse.

---

## 🚀 Getting Started

### Installation & Compilation
1. **Clone the repository:**
```bash
   git clone [https://github.com/your-username/distrifly-replication-grid.git](https://github.com/your-username/distrifly-replication-grid.git)
2. **Open in NetBeans IDE:**

    Launch your NetBeans IDE.

    Navigate to File > Open Project...

    Select the root folder containing the project files.

Running the Benchmark

Execute the main entry point to run all 4 combination metrics profiles consecutively:  

    Inside NetBeans: Open DistributedSystem.java, right-click inside the file window, and select Run File (or hit F6).

    Via Command Line:

    javac distributedsystem/*.java

    java distributedsystem.DistributedSystem
