Week 2 – Security Planning and Performance Testing Methodology
1. Overview

Week 2 focused on planning the system’s security baseline and defining a structured performance testing methodology. No security controls were implemented during this phase.

2. Performance Testing Plan
Monitoring Approach

All performance monitoring will be conducted remotely via SSH from the workstation. This approach ensures minimal overhead on the server and enforces remote administration skills.

Tools Used
top / htop	CPU and memory monitoring <img width="3839" height="1427" alt="Screenshot 2025-12-25 091158" src="https://github.com/user-attachments/assets/5ed85d22-6da7-4ce5-b74a-cfa8c8e8634c" />

vmstat	System activity <img width="1387" height="215" alt="Screenshot 2025-12-25 091118" src="https://github.com/user-attachments/assets/13cab84d-226c-47ac-ab51-20fe3119c2f2" />

iostat	Disk I/O <img width="3754" height="1275" alt="Screenshot 2025-12-25 074851" src="https://github.com/user-attachments/assets/f01f0e68-3270-43f0-8a5f-046abdb0dbef" />

free	Memory usage <img width="1866" height="151" alt="Screenshot 2025-12-25 080844" src="https://github.com/user-attachments/assets/e87760bd-1a8c-4ed9-89c2-02e1dccf8786" />

iperf3	Network throughput <img width="2475" height="600" alt="Screenshot 2025-12-25 080448" src="https://github.com/user-attachments/assets/632c9a7b-ce02-4f81-ac71-846590ff32c0" />

ping	Network latency <img width="1880" height="489" alt="Screenshot 2025-12-25 080545" src="https://github.com/user-attachments/assets/5d7809d6-612d-411b-b9c9-a6af3a3acee2" />

time	Command execution timing <img width="2245" height="817" alt="Screenshot 2025-12-25 080748" src="https://github.com/user-attachments/assets/788416a9-a00c-4018-b201-e823148490b9" />

3. Security Configuration Checklist

Planned security controls include:

SSH hardening (key-based auth, no root login)

Firewall configuration (restrictive inbound rules)

AppArmor mandatory access control

Automatic security updates

Least-privilege user management

Network service minimisation <img width="2296" height="2009" alt="Screenshot 2025-12-25 091752" src="https://github.com/user-attachments/assets/60d23f12-8447-4a9c-a744-ca15bff995a8" />



4. Threat Model
Threat	Description	Mitigation
SSH brute-force attacks	Automated login attempts	Key-based auth, firewall rules
Privilege escalation	Misconfigured permissions	Non-root admin user, sudo
Denial of Service	Resource exhaustion	Monitoring, firewall controls
5. Security vs Performance Considerations

Security controls may introduce minimal performance overhead; however, this is justified by the significant reduction in attack surface. Performance testing in later phases will quantify this impact.

6. Reflection

This planning phase highlighted how structured security design and performance evaluation must be considered together to balance system protection and efficiency.
