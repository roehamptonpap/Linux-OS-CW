Week 7 – Security Audit and System Evaluation


1. Overview

The aim of Week 7 was to conduct a comprehensive security audit of the Linux server and evaluate the effectiveness of the implemented security controls. This phase focused on identifying vulnerabilities, validating configuration choices, assessing exposed services, and reflecting on residual risk and security–performance trade-offs.

Industry-standard auditing and scanning tools were used to ensure an evidence-based evaluation of the system’s security posture.

2. Infrastructure Security Audit with Lynis
2.1 Initial Lynis Audit

Lynis was used to perform a full system security audit, analysing configuration files, permissions, kernel settings, and installed services.

sudo lynis audit system


The initial scan produced a security hardening index along with warnings and suggestions highlighting areas for improvement.

<img width="1792" height="1839" alt="Screenshot 2025-12-25 095849" src="https://github.com/user-attachments/assets/25c3d77b-7296-4cb8-ac16-b3f564f52d17" />

Label: Initial Lynis security audit showing hardening index and warnings

2.2 Identified Issues

Common findings included:

Recommendations for stricter file permissions

Suggestions to enable additional monitoring features

General hardening improvements related to system configuration

These findings were reviewed to determine which changes could be safely applied without disrupting system functionality.

3. Security Remediation and Re-Audit
3.1 Applied Remediations

Selected Lynis recommendations were implemented to improve the system’s security posture. Examples include tightening configuration file permissions and enabling additional system monitoring features.

sudo chmod 600 /etc/ssh/sshd_config
sudo apt install -y acct
sudo systemctl enable acct --now


These changes were chosen because they improved audit results while maintaining system stability.

3.2 Post-Remediation Audit

After remediation, Lynis was run again to measure improvement.

sudo lynis audit system


The hardening index increased, demonstrating measurable security improvement.

<img width="1792" height="1839" alt="Screenshot 2025-12-25 095849" src="https://github.com/user-attachments/assets/a04a2af2-c5bf-4bd4-84b2-294415d7db9b" />
Label: Lynis security audit results after remediation

4. Network Security Assessment (nmap)

To evaluate externally exposed services, a network scan was performed from the workstation using nmap.

sudo nmap -sS -p- SERVER_IP


The scan revealed that only port 22/tcp (SSH) was open.

<img width="1259" height="342" alt="Screenshot 2025-12-25 100552" src="https://github.com/user-attachments/assets/e955a1bb-4def-4786-b7e4-27c0cd584e20" />
Label: Network scan showing only SSH exposed

Analysis

Limiting exposed services significantly reduces the attack surface. Restricting external access to SSH alone aligns with best practices for headless server administration.

5. SSH Security Verification

The effective SSH configuration was verified to ensure that secure authentication policies were enforced.

sudo sshd -T | grep -E "permitrootlogin|passwordauthentication|pubkeyauthentication"


The output confirms:

Root login disabled

Password authentication disabled

Key-based authentication enabled

<img width="2404" height="256" alt="Screenshot 2025-12-25 093428" src="https://github.com/user-attachments/assets/3a53a068-c030-46f6-9adf-36d4a2276f94" />
Label: SSH configuration enforcing secure authentication

6. Service Inventory and Justification

All running services were reviewed to ensure they were necessary and justified.

systemctl list-units --type=service --state=running

Running Services Justification
| Service             | Purpose               | Justification                         |
| ------------------- | --------------------- | ------------------------------------- |
| ssh                 | Remote administration | Required for secure headless access   |
| nginx               | Web server            | Used for performance testing          |
| fail2ban            | Intrusion prevention  | Protects SSH from brute-force attacks |
| unattended-upgrades | Patch automation      | Ensures timely security updates       |
| apparmor            | Access control        | Enforces mandatory access control     |
| systemd-journald    | Logging               | Required for auditing and monitoring  |

Unnecessary services were avoided to minimise resource usage and security exposure.

<img width="2343" height="1242" alt="Screenshot 2025-12-25 100432" src="https://github.com/user-attachments/assets/ca5a395c-7d2c-4bea-8c36-3433110865b2" />
Label: Service inventory and running services

7. Residual Risk Assessment

Despite comprehensive hardening, residual risks remain:

SSH exposure: Required for administration but mitigated through firewall restrictions, key-based authentication, and fail2ban.

Insider threat: Legitimate users may still misuse access; mitigated through least privilege and auditing.

Zero-day vulnerabilities: Unknown vulnerabilities may exist; mitigated through automatic updates and monitoring.

Recognising residual risk demonstrates realistic security evaluation rather than assuming absolute protection.

8. Security vs Performance Evaluation

Security controls inevitably introduce some overhead; however, the impact on performance was minimal:

fail2ban performs lightweight log analysis

AppArmor restricts behaviour without measurable performance degradation

Automated updates reduce administrative effort

The overall configuration demonstrates that strong security can be achieved without sacrificing system responsiveness.

9. Final System Evaluation

Across the coursework, the system evolved from a minimal headless server into a securely configured and well-monitored environment. Layered security controls, regular auditing, and automation ensure both resilience and maintainability. Performance testing confirmed that security enhancements did not significantly degrade system behaviour, highlighting effective configuration trade-offs.

10. Reflection

Week 7 reinforced the importance of continuous security evaluation rather than one-time configuration. Auditing tools such as Lynis and nmap provide objective insight into system weaknesses, while remediation and re-testing ensure measurable improvement. This phase highlighted how operating system security is an ongoing process that must balance risk, usability, and performance.
