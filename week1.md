Week 1 – System Planning and Distribution Selection
1. Overview

The aim of Week 1 was to plan the operating system deployment and justify all technical decisions before implementation. This phase focused on system architecture, distribution selection, workstation choice, network configuration, and initial system inspection using command-line tools.

2. System Architecture
Architecture Description

The system uses a dual-machine architecture consisting of a headless Linux server and a separate workstation. All administration is performed remotely via SSH from the workstation. This design enforces command-line proficiency and mirrors real-world server administration practices.

Architecture Diagram
[ Workstation System ]
- SSH Client
- Monitoring tools
IP: 192.168.56.102
        |
        | SSH (Port 22)
        |
[ Server System ]
- Ubuntu Server (Headless)
- OpenSSH Server
- Firewall
IP: 192.168.56.102

3. Linux Distribution Selection
Selected Distribution

Ubuntu Server 24.04 LTS

Justification

Ubuntu Server 24.04 LTS was selected due to its long-term support lifecycle, stability, and extensive documentation. As an LTS release, it receives security updates until 2029, making it suitable for server environments. The default headless installation aligns with the coursework requirement for command-line-only administration. Ubuntu also includes native support for AppArmor and unattended security updates.

Comparison with Alternatives
Distribution	Advantages	Disadvantages
Ubuntu Server	LTS support, AppArmor, strong community	Slightly larger footprint
Debian	Very stable	Older packages
CentOS Stream	Enterprise-like	Rolling updates
Arch Linux	Highly customisable	Too complex for coursework
4. Workstation Configuration Decision
Selected Option

Option B – Host Machine as Workstation

Justification

The host machine was selected as the workstation to reduce complexity and resource usage. Using the host OS with an SSH client provides a clear separation between server and administration environments while reflecting real-world professional practices.

5. Network Configuration
VirtualBox Network Settings

Adapter: Host-only Adapter
DHCP: Enabled

IP Addressing
System	Interface	IP Address
Workstation	eth0	192.168.56.102
Server	enp0s3	192.168.56.102
6. System Specification (CLI Evidence)

The following commands were executed on the server to document system specifications:

uname -a <img width="809" height="88" alt="Screenshot 2025-12-25 085726" src="https://github.com/user-attachments/assets/3d6dda48-9d08-41a8-a492-cb438deebc41" />

free -h  <img width="1275" height="131" alt="Screenshot 2025-12-25 090142" src="https://github.com/user-attachments/assets/bc5b60af-d0ff-4672-9739-3251bfc64172" />

df -h <img width="806" height="197" alt="Screenshot 2025-12-25 085822" src="https://github.com/user-attachments/assets/7f3b5656-76a3-4bec-9f32-e23c90fea439" />

ip addr <img width="811" height="244" alt="Screenshot 2025-12-25 085952" src="https://github.com/user-attachments/assets/b3751d02-9a9e-43c8-9406-b830024841d6" />

lsb_release -a <img width="1261" height="181" alt="Screenshot 2025-12-25 090057" src="https://github.com/user-attachments/assets/35025d71-93d5-40d9-8100-5bc98971d02b" />


7. Reflection

This week demonstrated the importance of careful planning before system configuration. The dual-system architecture and headless server design reinforce secure and professional operating system administration practices that will be developed further in later phases.
