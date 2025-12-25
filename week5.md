Week 5 – Advanced Security and Monitoring Infrastructure

1. Overview

The aim of Week 5 was to extend the system’s security posture beyond basic hardening by implementing advanced security controls and automated monitoring. This phase introduced mandatory access control, intrusion detection, automated patching, and scripted verification to ensure security configurations are consistently enforced.

All configuration and monitoring tasks were performed remotely via SSH from the workstation, maintaining compliance with the administrative constraints of the coursework.

2. Mandatory Access Control with AppArmor
  AppArmor Status Verification
 sudo aa-status <img width="2222" height="163" alt="Screenshot 2025-12-25 094117" src="https://github.com/user-attachments/assets/2ea380b9-95cd-4e7f-a5f6-d80e37da8f37" />
The output confirms that the AppArmor kernel module is loaded and that profiles are operating in enforce mode.
Ubuntu Server includes AppArmor as its default mandatory access control framework. AppArmor was verified to be enabled and enforcing security profiles across the system.

2.2 Security Impact

Mandatory access control restricts what applications can access, even if they are compromised. This significantly reduces the potential impact of privilege escalation and lateral movement within the system. While not all services require individual profiles, system-wide enforcement confirms that access control policies are active.

3. Automatic Security Updates
3.1 Configuration of Unattended Upgrades

Automatic security updates were configured to ensure that critical patches are applied without manual intervention.
sudo apt install -y unattended-upgrades
sudo dpkg-reconfigure --priority=low unattended-upgrades <img width="3830" height="2092" alt="Screenshot 2025-12-25 061857" src="https://github.com/user-attachments/assets/fcb42bdd-b14d-4d23-afb0-644864fec9a1" />

sudo systemctl status unattended-upgrades
sudo unattended-upgrades --dry-run
<img width="2179" height="97" alt="Screenshot 2025-12-25 094430" src="https://github.com/user-attachments/assets/6cc2982a-97cb-48fc-98df-ed908afdc940" />

Label: Verification of automatic security updates

3.3 Security Impact
Automatic updates reduce the window of vulnerability by ensuring that security patches are applied promptly. This improves system resilience with minimal performance overhead.

4. Intrusion Detection with fail2ban

fail2ban was installed and configured to protect the SSH service from brute-force attacks.

sudo apt install -y fail2ban


A local jail configuration was created for SSH monitoring.

[sshd]
enabled = true
port = ssh
logpath = %(sshd_log)s
maxretry = 5
findtime = 600
bantime = 3600


4.2 Verification

fail2ban was restarted and its operational status verified.

sudo fail2ban-client status
sudo fail2ban-client status sshd


<img width="1786" height="277" alt="Screenshot 2025-12-25 094640" src="https://github.com/user-attachments/assets/4f2c7f0e-2dae-4f01-aa26-1f10e3faccf3" />

Label: fail2ban active intrusion detection for SSH

4.3 Security Impact

fail2ban provides active intrusion prevention by automatically blocking IP addresses that exhibit malicious behaviour. This complements SSH hardening and firewall rules by responding dynamically to attacks.

5. Security Baseline Verification Script
5.1 Script Purpose

A custom security verification script, security-baseline.sh, was created to provide repeatable validation of all security controls implemented in Weeks 4 and 5. This script checks SSH hardening, firewall status, AppArmor enforcement, fail2ban operation, and automatic updates.

5.2 Script Execution
./security-baseline.sh


<img width="1931" height="1994" alt="Screenshot 2025-12-25 064830" src="https://github.com/user-attachments/assets/10b42076-8573-45b4-9fe0-b0f61ac443d3" /> <img width="654" height="135" alt="Screenshot 2025-12-25 064840" src="https://github.com/user-attachments/assets/fbf946da-cf31-41f8-b0f9-f4b2e76448e3" />

Label: Security baseline verification script execution

5.3 Value of Automation

Automating security verification ensures consistency and reduces the likelihood of configuration drift. The script provides rapid assurance that the system remains compliant with the defined security baseline.

6. Remote Monitoring Script
6.1 Script Purpose

A remote monitoring script, monitor-server.sh, was created on the workstation. This script connects to the server via SSH and collects real-time performance metrics, including CPU usage, memory usage, disk utilisation, and uptime.

6.2 Script Execution
./monitor-server.sh


<img width="923" height="725" alt="Screenshot 2025-12-25 065037" src="https://github.com/user-attachments/assets/20f3d071-a9f7-4499-ae04-eac52e2faeb6" /> <img width="1932" height="1279" alt="Screenshot 2025-12-25 065256" src="https://github.com/user-attachments/assets/6cbe9837-9d12-49bb-9b11-516a7cb0fa16" />

Label: Remote monitoring via SSH

6.3 Monitoring Benefits

Remote monitoring minimises overhead on the server and reinforces best practice by separating administration and observation roles. This script also prepares the system for the performance evaluation conducted in Week 6.

7. Security vs Performance Considerations

The security controls implemented in this phase introduce minimal performance overhead while significantly improving system resilience. AppArmor restricts application behaviour, fail2ban adds lightweight log analysis, and unattended upgrades automate patch management. Together, these controls provide layered security without negatively impacting system responsiveness.

8. Reflection

Week 5 demonstrated the importance of moving beyond static configuration toward active, automated security enforcement. The use of mandatory access control, intrusion detection, and scripted verification improved both the robustness and maintainability of the system. Automation played a key role in balancing security effectiveness with operational efficiency.
