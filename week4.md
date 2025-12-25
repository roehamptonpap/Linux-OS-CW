Week 4 – Initial System Configuration & Security Implementation
1. Overview

Week 4 involved implementing foundational security controls on the server, transitioning from basic access to secure remote administration.

2. User and Privilege Management

A non-root administrative user (sysadmin) was created and granted sudo privileges. This enforces the principle of least privilege and reduces the risk associated with root-level access.

(Insert screenshots: adduser, groups, sudo whoami) <img width="1239" height="104" alt="Screenshot 2025-12-25 093033" src="https://github.com/user-attachments/assets/d13cf873-0ba0-4fb0-828b-31c1521013aa" />  <img width="1036" height="118" alt="Screenshot 2025-12-25 093046" src="https://github.com/user-attachments/assets/5f43c04e-23e1-447c-a4d4-c80cc17643bd" /> 



3. SSH Key-Based Authentication

SSH key-based authentication was configured to replace password-based logins. This significantly reduces the risk of brute-force attacks. <img width="1963" height="540" alt="Screenshot 2025-12-25 093010" src="https://github.com/user-attachments/assets/2a379693-2cd4-48c0-9611-b40584f37cde" />


Key changes:

Root login disabled

Password authentication disabled

Key-based authentication enforced

Access restricted to authorised user

(Insert before/after sshd_config screenshots) <img width="2366" height="265" alt="Screenshot 2025-12-25 093114" src="https://github.com/user-attachments/assets/70b71fc2-9681-48dc-b02e-8e6b76b30381" />
 <img width="2404" height="256" alt="Screenshot 2025-12-25 093428" src="https://github.com/user-attachments/assets/443d611c-f440-4836-82b2-45ac3b4d3dc9" />

4. Firewall Configuration

UFW was configured with a default deny policy for incoming traffic. SSH access was explicitly permitted only from the workstation IP address.
sudo ufw default deny incoming
sudo ufw allow from 192.168.56.10 to any port 22
sudo ufw enable
<img width="1508" height="378" alt="Screenshot 2025-12-25 093133" src="https://github.com/user-attachments/assets/a884f5c6-c60c-4b4a-90d7-068b9fdc856d" />

5. Remote Administration Evidence

All configuration steps were performed via SSH from the workstation, demonstrating compliance with the administrative constraint.

6. Reflection

Implementing SSH hardening and restrictive firewall rules significantly improved the system’s security posture. This phase highlighted the importance of sequencing changes carefully to avoid loss of remote access.
