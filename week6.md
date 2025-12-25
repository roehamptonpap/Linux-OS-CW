📘 Week 6 – Performance Evaluation and Analysis

⬅ Home
 | Week 7 ➡

1. Overview

The aim of Week 6 was to evaluate operating system performance under different workloads and analyse how Linux behaves when system resources are stressed. Baseline measurements were established, targeted load testing was performed, performance bottlenecks were identified, and kernel-level optimisation was applied to demonstrate measurable improvements.

All testing and monitoring were conducted remotely via SSH from the workstation, in line with the coursework administrative constraints.

2. Baseline System Performance (Idle)

Before applying any load, baseline performance metrics were captured to establish a reference point for comparison.

Observed Baseline Metrics

Load Average (1 min): 0.00

CPU Idle: ~90%

Total Memory: 1.9 GiB

Available Memory: 848 MiB

Swap Usage: 0 B

These values confirm that the system was idle and stable prior to testing.

<img width="1267" height="334" alt="Screenshot 2025-12-25 081304" src="https://github.com/user-attachments/assets/4d30d78d-e7fb-45d9-9091-403290dbbc25" />
Label: Baseline CPU and memory usage (idle)

3. CPU Performance Under Load

A CPU-intensive workload was generated using stress-ng to evaluate scheduler behaviour under sustained computational demand.

Test Command
stress-ng --cpu 2 --timeout 60s

Observations

Two CPU workers were dispatched successfully

CPU load increased significantly during execution

The system remained responsive throughout the test

No failed stressors were reported

This demonstrates effective CPU scheduling by the Linux kernel under contention.

<img width="1795" height="256" alt="Screenshot 2025-12-25 081501" src="https://github.com/user-attachments/assets/fa1a5e3d-cb8d-4a51-9df5-18376209a5e9" />
Label: CPU stress test execution using stress-ng

4. Disk I/O Performance Analysis

Disk performance was evaluated using a random write workload to identify storage-related bottlenecks.

Test Configuration

Tool: fio

Block size: 4 KB

Runtime: 60 seconds

I/O engine: libaio

Queue depth: 1

Key Results
Metric	Observed Value
Bandwidth	13.4 MiB/s
IOPS	3420
Disk Utilisation	87.97%
Average Latency	~22 ms
Maximum Latency	~1.17 s

High disk utilisation and increased latency indicate that disk I/O became a performance bottleneck under random write workloads, which is typical in virtualised environments.

<img width="2880" height="1017" alt="Screenshot 2025-12-25 084828" src="https://github.com/user-attachments/assets/0d552be5-99a0-43b7-b925-c9150372653c" />
Label: Disk I/O stress test results using fio

5. Network Performance Evaluation
5.1 Throughput Testing

Network throughput was measured using iperf3.

Metric	Value
Average Throughput	12.8 Gbits/sec
Data Transferred	14.9 GB (10 s)
Retransmissions	61

📸 Insert Screenshot Here
Screenshot: iperf3 -c SERVER_IP
Label: Network throughput measurement using iperf3

5.2 Latency Testing

Latency was measured using ICMP echo requests.

Metric	Value
Minimum RTT	0.030 ms
Average RTT	0.069 ms
Maximum RTT	0.267 ms
Packet Loss	0%

<img width="1880" height="489" alt="Screenshot 2025-12-25 080545" src="https://github.com/user-attachments/assets/639a0d5e-17bd-4dcb-9c90-a81314501b73" />
Screenshot: ping -c 10 SERVER_IP
Label: Network latency measurement

Analysis

The extremely high throughput and low latency are a result of the VirtualBox host-only network, which operates largely in memory. This confirms that network performance is not a limiting factor in this environment, allowing other system bottlenecks to be analysed independently.

6. Server Application Performance (nginx)

To evaluate real-world application performance, response time for a locally hosted nginx web server was measured.

Test Command
time curl http://localhost

Observed Results
Metric	Value
Response Time (real)	50 ms
User CPU Time	11 ms
System CPU Time	22 ms

This demonstrates efficient HTTP request handling under low load conditions.

<img width="2245" height="817" alt="Screenshot 2025-12-25 080748" src="https://github.com/user-attachments/assets/226babdf-47bd-40d8-ae3f-d65117b791dd" />
Label: nginx response time measurement

7. Performance Optimisation – Memory Tuning
Optimisation Applied

The kernel swappiness parameter was reduced to prioritise RAM usage over swap.

sudo sysctl vm.swappiness=10


<img width="1362" height="124" alt="Screenshot 2025-12-25 080814" src="https://github.com/user-attachments/assets/5cce2988-8a2c-4fa3-9d2c-3d409d6f9d75" />
Label: Memory optimisation: reduced swappiness

Post-Optimisation Memory State
Metric	Value
Available Memory	848 MiB
Swap Usage	0 B

<img width="1866" height="151" alt="Screenshot 2025-12-25 080844" src="https://github.com/user-attachments/assets/cbf7c061-7dd3-41b6-b550-9320d90aa1be" />
Label: Memory usage after optimisation

Reducing swappiness eliminated swap usage and improved memory availability, increasing system responsiveness under memory pressure.

| Test Category | Metric | Observed Value |
|--------------|--------|---------------|
| CPU | Load Average (Idle) | 0.00 |
| CPU | CPU Idle (%) | ~90% |
| Disk I/O | Bandwidth | 13.4 MiB/s |
| Disk I/O | IOPS | 3420 |
| Disk I/O | Disk Utilisation | 87.97% |
| Network | Throughput | 12.8 Gbits/sec |
| Network | Latency (avg) | 0.069 ms |
| nginx | Response Time | 50 ms |
| Memory | Available RAM | 848 MiB |
| Memory | Swap Used | 0 B |

9. Performance Analysis and Bottlenecks

The results show that disk I/O is the primary performance bottleneck under load, as evidenced by high utilisation and increased latency during random write operations. CPU-bound workloads were handled efficiently by the Linux scheduler, while network performance was effectively unconstrained due to the virtual host-only network. Kernel-level tuning through reduced swappiness improved memory behaviour and responsiveness.

10. Reflection

This week demonstrated how operating system behaviour changes under different workload types and how performance bottlenecks can be identified through structured testing. Applying targeted optimisations highlighted the trade-off between performance tuning and system stability, reinforcing the importance of evidence-based configuration decisions in system administration.
