
# 🕸️ Distributed System over TCP

## 🧠 Project Overview

This project implements a distributed system in a local lab environment where multiple machines collaborate via TCP socket connections to perform file processing tasks. Although tasks are distributed, the system behaves as a unified entity from the user's perspective.

### System Components
- **Master server** (`Master.py`) responsible for coordinating operations.
- **Client workers** (`Worker.py`) that handle distributed processing tasks.

---

## ⚙️ Architecture & Execution Workflow

The system runs through six core phases simulating a distributed processing pipeline:

### 🔁 Phase 1 — Initialization
The master sends the names of the files to be processed to the client machines.

### 🔄 Phase 2 — Initial Data Distribution (Shuffle1)
Clients connect to each other via TCP and distribute the words contained in the files.

### 📬 Phase 3 — Local Grouping
Each client calculates word frequencies and sends the result back to the master.

### 📦 Phase 4 — Balanced Redistribution
The master aggregates all frequency data, evenly splits it, and redistributes it to the clients.

### 🔃 Phase 5 — Inter-client Exchange (Shuffle2)
Clients exchange sub-lists among themselves for final sorting based on frequency.

### ✅ Phase 6 — Sorting & Final Output
Each client sorts words by frequency (and alphabetically if needed) and returns the final result to the master.

---

## 📊 Performance Insight — Amdahl’s Law

Amdahl’s Law is considered to evaluate the scalability of parallel systems. It emphasizes that even with more machines, the sequential portion of the program limits the overall speedup due to communication and coordination overhead.

---

## 🚀 Getting Started

Make sure all client machines are reachable via SSH and that the network configuration is correctly set up before running the system.

### 🔧 Step 1 — Configure `Deployement.sh`
Update the script with:
- SSH username for remote access
- Scripts to be executed on the client machines
- IPs or hostnames of the client machines

### 🖥️ Step 2 — Launch the Deployment Script
On any machine, unzip the project folder and run:
```bash
./Deployement.sh
```
The script will initiate TCP connections with all specified client machines. A successful connection logs messages like:
```bash
Socket bound to port {port} after {attempt + 1} attempts
```

### 🧩 Step 3 — Run the Master Script
Once all connections are established:
```bash
python Master.py
```
The master coordinates the tasks and handles communication with the workers.

---

## 📁 Output

- Once processing is complete, the master generates a file `resultats.txt` containing the final sorted word frequencies.
- All TCP connections are gracefully closed at the end of the run.

---

