# Performance Analysis of Virtualization: Type-1 vs Type-2 Hypervisors

## Overview

This laboratory experiment evaluates and compares the performance of virtual machines operating under two different virtualization architectures:

- **Type-1 Hypervisor:** Proxmox VE, running directly on physical hardware.
- **Type-2 Hypervisor:** VMware Workstation, running over a host operating system.

Ubuntu virtual machines were configured on both platforms and subjected to the same CPU benchmark using Sysbench. The performance was evaluated using execution time, total events, events per second, and latency.

---

# PART A: Performance Analysis Using Type-1 Hypervisor – Proxmox VE

## 1. Virtual Machine Specifications

| Parameter | Configuration |
| :--- | :--- |
| Hypervisor | Proxmox VE |
| Hypervisor Type | Type-1 |
| Node | Selected Proxmox Node (pve) |
| VM Name | CC-Experiment1-Type1 |
| Guest Operating System | Linux (Ubuntu 64-bit) |
| ISO Image | ubuntu-22.04.iso |
| CPU Allocation | 2 vCPU (1 Socket, 2 Cores) |
| Memory Allocation | 2048 MiB (2 GB RAM) |
| Disk Storage | 20 GB (local-lvm) |
| Network Bridge | vmbr0 (VirtIO) |

## 2. System Verification

The Ubuntu virtual machine was verified after installation using standard Linux system-monitoring commands.

### Hostname and OS Verification

```bash
hostnamectl
````

### CPU Configuration

```bash
lscpu
```

### Memory Configuration

```bash
free -h
```

### Disk Storage

```bash
df -h
```

### Real-Time System Monitoring

```bash
top
```

These commands were used to verify the operating system, CPU configuration, memory availability, disk usage, and current system activity.

## 3. CPU Performance Benchmark

The CPU performance of the virtual machine was tested using Sysbench with a maximum prime number of 20000.

```bash
sysbench cpu --cpu-max-prime=20000 run
```

## 4. Observation Table

| Parameter / Metric     | Observation / Result |
| :--------------------- | :------------------- |
| Hypervisor             | Proxmox VE           |
| Hypervisor Type        | Type-1               |
| Guest Operating System | Ubuntu               |
| CPU Allocation         | 2 vCPU               |
| Memory Allocation      | 2 GB                 |
| Disk Allocation        | 20 GB                |
| Total Execution Time   | 10.0006s             |
| Total Events           | 16903                |
| Events per Second      | 1689.43              |
| Minimum Latency        | 0.57 ms              |
| Average Latency        | 0.59 ms              |
| Maximum Latency        | 1.09 ms              |

## 5. Workflow

1. Connect to the designated network.
2. Open the Proxmox VE web interface at `https://<PROXMOX_SERVER_IP>:8006`.
3. Log in using the authorized credentials and select the appropriate realm.
4. Navigate to **Datacenter → pve**.
5. Launch the **Create VM** wizard.
6. Select the Ubuntu ISO image.
7. Configure the virtual disk with **20 GB** storage.
8. Configure the CPU with **2 vCPUs (1 Socket, 2 Cores)**.
9. Allocate **2048 MiB (2 GB)** of memory.
10. Configure the network using the `vmbr0` bridge with VirtIO.
11. Review and create the virtual machine.
12. Start the VM and open the **noVNC Console**.
13. Complete the Ubuntu installation and restart the VM.
14. Log in to the Ubuntu terminal.
15. Verify the system configuration using:

```bash
hostnamectl
lscpu
free -h
df -h
```

16. Install the Sysbench benchmarking utility.
17. Execute the CPU benchmark:

```bash
sysbench cpu --cpu-max-prime=20000 run
```

18. Record the benchmark results.
19. Monitor VM resource utilization from the Proxmox dashboard.
20. Gracefully shut down the VM after completing the experiment.

---

# PART B: Performance Analysis Using Type-2 Hypervisor – VMware Workstation

## 1. Virtual Machine Specifications

| Parameter              | Configuration                 |
| :--------------------- | :---------------------------- |
| Hypervisor             | VMware Workstation            |
| Hypervisor Type        | Type-2                        |
| VM Name                | CC-Experiment1-Type2          |
| Guest Operating System | Linux (Ubuntu 64-bit)         |
| ISO Image              | ubuntu-22.04.iso              |
| CPU Allocation         | 2 vCPU (1 Processor, 2 Cores) |
| Memory Allocation      | 8 GB (8192 MB)                |
| Disk Storage           | 20 GB (Single disk)           |
| Network Adapter        | NAT                           |

## 2. System Verification

The Ubuntu virtual machine was checked using the following commands.

### Hostname and OS Verification

```bash
hostnamectl
```

### CPU Configuration

```bash
lscpu
```

### Memory Configuration

```bash
free -h
```

### Disk Storage

```bash
df -h
```

### Real-Time System Monitoring

```bash
top
```

These commands were used to verify the guest operating system, processor configuration, available memory, storage utilization, and real-time resource usage.

## 3. CPU Performance Benchmark

The same Sysbench CPU workload was executed on the VMware Workstation virtual machine.

```bash
sysbench cpu --cpu-max-prime=20000 run
```

The benchmark parameters were kept the same so that the CPU performance of both virtualization environments could be compared.

## 4. Observation Table

| Parameter / Metric     | Observation / Result |
| :--------------------- | :------------------- |
| Hypervisor             | VMware Workstation   |
| Hypervisor Type        | Type-2               |
| Guest Operating System | Ubuntu               |
| CPU Allocation         | 2 vCPU               |
| Memory Allocation      | 8 GB                 |
| Disk Allocation        | 20 GB                |
| Total Execution Time   | 10.0003s             |
| Total Events           | 17588                |
| Events per Second      | 1758.60              |
| Minimum Latency        | 0.55 ms              |
| Average Latency        | 0.57 ms              |
| Maximum Latency        | 1.11 ms              |

## 5. Workflow

1. Launch VMware Workstation.
2. Select **Create a New Virtual Machine**.
3. Select the Ubuntu ISO installer.
4. Set the VM name as `CC-Experiment1-Type2`.
5. Select the required VM storage location.
6. Configure a **20 GB** virtual disk.
7. Open the hardware customization settings.
8. Allocate **2 vCPUs (1 Processor, 2 Cores)**.
9. Allocate **8 GB RAM**.
10. Configure the network adapter using **NAT**.
11. Power on the VM and complete the Ubuntu installation.
12. Log in to the Ubuntu terminal.
13. Verify the system configuration using:

```bash
hostnamectl
lscpu
free -h
df -h
```

14. Install Sysbench.
15. Run the CPU benchmark:

```bash
sysbench cpu --cpu-max-prime=20000 run
```

16. Record the obtained benchmark values.
17. Compare the results with the Proxmox VE VM.
18. Shut down the VM using:

```bash
sudo poweroff
```

---

# PART C: Comparative Performance Analysis

## 1. Side-by-Side Benchmark Comparison

| Metric / Parameter     | Type-1 Hypervisor (Proxmox VE)      | Type-2 Hypervisor (VMware Workstation) |
| :--------------------- | :---------------------------------- | :------------------------------------- |
| Architecture Level     | Bare-Metal (Direct hardware access) | Hosted (Runs on host OS)               |
| vCPU Allocation        | 2 vCPU                              | 2 vCPU                                 |
| Memory Allocation      | 2 GB                                | 8 GB                                   |
| Disk Allocation        | 20 GB                               | 20 GB                                  |
| Benchmark Test         | Sysbench CPU (Max Prime: 20000)     | Sysbench CPU (Max Prime: 20000)        |
| Total Execution Time   | 10.0006s                            | 10.0003s                               |
| Total Number of Events | 16903                               | 17588                                  |
| Events per Second      | 1689.43                             | 1758.60                                |
| Minimum Latency        | 0.57 ms                             | 0.55 ms                                |
| Average Latency        | 0.59 ms                             | 0.57 ms                                |
| Maximum Latency        | 1.09 ms                             | 1.11 ms                                |

## 2. Performance Analysis

### Throughput

VMware Workstation recorded **17,588 total events** with a throughput of **1758.60 events/second**. Proxmox VE recorded **16,903 total events** with a throughput of **1689.43 events/second**.

The difference in throughput can be affected by VM resource allocation, host hardware, system workload, and virtualization configuration. In this experiment, the VMware VM was allocated **8 GB RAM**, whereas the Proxmox VM was allocated **2 GB RAM**.

### Execution Time

The benchmark execution times recorded for both platforms were very close:

* **Proxmox VE:** 10.0006s
* **VMware Workstation:** 10.0003s

The small difference indicates that both environments completed the selected CPU workload in nearly the same amount of time.

### Latency Characteristics

Both hypervisors maintained sub-millisecond average latency.

For Proxmox VE:

* Minimum Latency: **0.57 ms**
* Average Latency: **0.59 ms**
* Maximum Latency: **1.09 ms**

For VMware Workstation:

* Minimum Latency: **0.55 ms**
* Average Latency: **0.57 ms**
* Maximum Latency: **1.11 ms**

The latency values were relatively close across both configurations. Proxmox VE recorded a maximum latency of **1.09 ms**, while VMware Workstation recorded **1.11 ms**.

### Type-1 Hypervisor

Proxmox VE follows a Type-1 virtualization architecture in which the hypervisor operates directly on the physical hardware.

Important characteristics include:

* Direct access to physical system resources.
* No conventional host operating system between the hypervisor and hardware.
* Centralized virtual machine management.
* Suitable for server and data-center environments.
* Efficient allocation of hardware resources among virtual machines.

### Type-2 Hypervisor

VMware Workstation follows a Type-2 virtualization architecture and operates on top of an existing host operating system.

Important characteristics include:

* Runs as software within the host operating system.
* Convenient for desktop-based virtualization.
* Useful for development, testing, and educational environments.
* Physical resources are shared between the host OS and virtual machines.
* Provides convenient integration with the host desktop environment.

### Architectural Comparison

The main architectural difference is the layer at which each hypervisor operates.

**Proxmox VE** operates directly on physical hardware and manages virtual machines from the hypervisor layer.

**VMware Workstation** operates above a host operating system, allowing users to run virtual machines alongside normal desktop applications.

The benchmark results show that the architectural difference did not result in a large variation in performance for the selected CPU workload. However, benchmark results can vary depending on CPU architecture, memory allocation, host workload, storage performance, VM configuration, and other system-level factors.

---

# 3. Result Summary

| Metric               | Proxmox VE | VMware Workstation |
| :------------------- | :--------: | :----------------: |
| Total Execution Time |  10.0006s  |      10.0003s      |
| Total Events         |    16903   |        17588       |
| Events per Second    |   1689.43  |       1758.60      |
| Minimum Latency      |   0.57 ms  |       0.55 ms      |
| Average Latency      |   0.59 ms  |       0.57 ms      |
| Maximum Latency      |   1.09 ms  |       1.11 ms      |

---

# Conclusion

This experiment compared the performance characteristics of **Type-1 and Type-2 hypervisors** using Proxmox VE and VMware Workstation.

Both platforms successfully hosted Ubuntu virtual machines and completed the same Sysbench CPU benchmark. Proxmox VE achieved **1689.43 events/second**, while VMware Workstation achieved **1758.60 events/second**.

The average latency was **0.59 ms** for Proxmox VE and **0.57 ms** for VMware Workstation. The measured execution times were also very close, with **10.0006s** for Proxmox VE and **10.0003s** for VMware Workstation.

The experiment demonstrates that VM performance depends on multiple factors, including hypervisor architecture, resource allocation, host hardware, and system configuration. It also provides a practical comparison between bare-metal and hosted virtualization environments.

```
```
