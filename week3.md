Week 3 – Application Selection for Performance Testing
1. Overview

The objective of Week 3 was to select representative applications that stress different operating system subsystems, enabling meaningful performance analysis.

2. Application Selection Matrix
Workload Type	Application	Justification
CPU-intensive	stress-ng	Controlled CPU stress testing <img width="1795" height="256" alt="Screenshot 2025-12-25 081501" src="https://github.com/user-attachments/assets/7b0cfd42-ea21-4d1e-9278-7f398c7864d7" />

Memory-intensive	stress-ng (VM stressors)	Memory pressure analysis
Disk I/O	fio	Industry-standard disk benchmarking <img width="3226" height="1076" alt="Screenshot 2025-12-25 080235" src="https://github.com/user-attachments/assets/809e9df5-d0b3-430b-84af-4bad3738815d" />

Network	iperf3	Network throughput measurement <img width="2475" height="600" alt="Screenshot 2025-12-25 080448" src="https://github.com/user-attachments/assets/0e1ccbd7-8a26-402d-85b5-f0222ec76d22" />

Server workload	nginx	Realistic server application <img width="1834" height="352" alt="Screenshot 2025-12-25 092637" src="https://github.com/user-attachments/assets/bcc56d84-5bd3-4ea0-8d4f-7be26876288a" />

<img width="1866" height="151" alt="Screenshot 2025-12-25 080844" src="https://github.com/user-attachments/assets/4593292e-48ac-48da-8a0a-f6056b39bac2" />


Installation commands: 
sudo apt update
sudo apt install -y stress-ng fio iperf3 nginx

4. Expected Resource Profiles
| Application        | CPU      | Memory | Disk | Network  |
| ------------------ | -------- | ------ | ---- | -------- |
| stress-ng (CPU)    | High     | Low    | Low  | None     |
| stress-ng (Memory) | Moderate | High   | Low  | None     |
| fio                | Low      | Low    | High | None     |
| iperf3             | Moderate | Low    | None | High     |
| nginx              | Low      | Low    | Low  | Moderate |


 5. Monitoring Strategy

Each application will be monitored using relevant CLI tools such as top, vmstat, iostat, and ping, allowing quantitative comparison under different load scenarios.

6. Reflection

Combining synthetic benchmarks with a real server application provides a comprehensive view of operating system behaviour across different workloads.
