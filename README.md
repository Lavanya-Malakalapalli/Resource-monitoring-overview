# Resource Monitoring in an Open Virtualized RAN

## 📌 Overview

Virtualized Radio Access Networks (vRAN) allow 5G network functions to run as software on general-purpose servers instead of dedicated hardware. While this makes networks more flexible and scalable, monitoring the computing resources used by different RAN components becomes increasingly important.

In this work, we developed a lightweight resource monitoring framework using **EdgeRIC** to monitor the infrastructure-level resource utilization of virtualized Centralized Unit (vCU) and Distributed Unit (vDU).

The framework collects CPU usage, memory consumption, and disk utilization in real time through a lightweight µApp. The collected metrics provide better visibility into resource usage and can support intelligent resource management in Open RAN environments.

## 🏗️ System Architecture

The proposed framework extends the EdgeRIC architecture to collect and monitor system-level metrics from virtualized CU and DU components.

The architecture consists of:

- **5G O-RAN Environment:** OpenAirInterface (OAI)-based 5G Standalone (SA) deployment with disaggregated vCU and vDU.
- **EdgeRIC:** Provides an execution environment for µApps that support real-time monitoring and control.
- **Metric Collection:** Collects CPU usage, virtual memory consumption, and disk utilization from the vCU and vDU.
- **Communication:** ZeroMQ (ZMQ) and Protocol Buffers (Protobuf) are used for lightweight messaging and efficient data serialization.
- **Monitoring and Visualization:** Prometheus collects and stores the metrics, while Grafana provides interactive dashboards for visualization.

## ⚙️ Implementation and Methodology

A custom µApp was developed within EdgeRIC to periodically collect infrastructure-level metrics from the vCU and vDU.

The metric collection process involves:

1. Collecting metrics at the PDCP layer of the vCU and MAC layer of the vDU.
2. Extracting system-level metrics through EdgeRIC wrapper modules.
3. Serializing the metrics using Protocol Buffers.
4. Transmitting the data through ZeroMQ.
5. Receiving and processing CU and DU metrics independently.
6. Integrating the collected metrics within the µApp for monitoring and visualization.

The metrics are averaged over 60-second intervals to provide a consistent view of resource utilization.

## 🧪 Experimental Setup

The experiments were conducted using an OAI-based 5G Standalone EdgeRIC testbed.

**Environment configuration:**

- vCU and vDU deployed as separate virtualized components.
- Core Network (CN) deployed using Docker containers.
- UE simulated using a Docker container.
- Prometheus and Grafana integrated for monitoring and visualization.

**Hardware configuration:**

| Resource | Configuration |
|---|---|
| CPU | 16 cores |
| Memory | 16 GB |
| Disk | 200 GB |

### Resource Stress Testing

The `stress-ng` tool was used to generate controlled workloads and evaluate the monitoring framework under different resource conditions.

The experiment consisted of three phases:

| Phase | Workload | Duration |
|---|---|---|
| 1 | CPU stress (20%–100%) | 25 minutes |
| 2 | Memory stress (20%–100%) | 25 minutes |
| 3 | Disk I/O stress (20%–100%) | 25 minutes |

The workloads were applied independently to the vCU and vDU to observe their resource utilization patterns under different stress conditions.

## 📊 Experimental Results

The monitoring framework successfully captured and visualized real-time resource utilization across both virtualized RAN components.

**Key observations:**

**1. CPU Utilization**
- CPU utilization increased progressively with the applied CPU workload.
- It reached approximately 100% during the CPU stress phase.
- During memory stress, CPU utilization remained below 10%.
- A modest increase of around 10–15% was observed during disk stress.

**2. Memory Utilization**
- During CPU stress, memory usage remained relatively stable at approximately 13.2 GB for vCU and 14.2 GB for vDU.
- During memory stress, usage increased to approximately 15.5 GB as the workload increased.

**3. Disk Utilization**
- During CPU and memory stress, disk usage remained relatively stable at approximately 118 GB for vCU and 102 GB for vDU.
- During disk stress, utilization increased to approximately 188 GB for vCU and 170 GB for vDU.

These results demonstrate that the EdgeRIC-based µApp can capture resource utilization changes and provide fine-grained visibility into the behaviour of virtualized RAN components.

## 💡 Potential Applications

The collected resource metrics can support intelligent resource management in virtualized RAN environments.

Some potential applications include:

- Dynamic CPU resource allocation based on workload requirements.
- CPU frequency scaling during periods of low resource demand.
- Improved CPU core pinning and task allocation.
- Proactive resource management to avoid resource exhaustion.
- Scaling computing resources based on changing network workloads.

These capabilities can contribute to improved resource utilization and reduced operational costs.

## 🛠️ Technologies and Tools

- **5G RAN:** OpenAirInterface (OAI), O-RAN
- **Edge Intelligence:** EdgeRIC, µApp
- **Communication:** ZeroMQ, Protocol Buffers
- **Monitoring:** Prometheus, Grafana
- **Virtualization:** Docker
- **Stress Testing:** stress-ng
- **Programming:** C/C++, Python
- **Environment:** Linux

## 📄 Publication

**Resource Monitoring in an Open Virtualized RAN**

Authors: Lavanya Malakalapalli, Abhishek Bhattacharyya, Andrea Fumagalli, and Koteswararao Kondepu.

Published in: 2025 IEEE Future Networks World Forum (FNWF).

DOI: [10.1109/FNWF66845.2025.11317187](https://doi.org/10.1109/FNWF66845.2025.11317187)

## 📁 Repository Information

This repository presents an overview of the research, including the system architecture, implementation methodology, experimental setup, and key findings.

The work demonstrates how lightweight edge applications can provide real-time infrastructure-level monitoring in virtualized Open RAN environments.

## 💻 Code Availability

The implementation and experimental environment used in this work are maintained separately and are not included in this public repository.

This repository focuses on documenting the proposed architecture, implementation workflow, experimental methodology, and results presented in the IEEE FNWF 2025 paper.

The complete implementation involves modifications to the OAI-based vCU/vDU environment, EdgeRIC modules, ZeroMQ communication, Protobuf serialization, and the custom µApp.
