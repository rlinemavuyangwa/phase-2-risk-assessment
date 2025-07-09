# Risk and Compliance Assessment Report – Phase 2
**By:** Rulane Hlongwani  
**Date:** July 2025

---

## Step 1: Asset Identification

| Asset Name        | Description                           | Type                |
| ----------------- | ------------------------------------- | ------------------- |
| Ubuntu + OpenCart | Online shop (website)                 | Digital/Software    |
| Windows 10        | Simulated employee PC                 | Digital/Workstation |
| Kali Linux        | Attacker tools & Myself,ethical hacker| Digital/Attacker    |
| pfSense           | Firewall – filters traffic            | Network/Service     |
| Wazuh Server      | Monitors logs                         | Security Tool       |
| Security Onion    | Detects threats on the network        | Security Tool       |
| Metasploitable2   | Intentionally vulnerable system       | Testing Target      |
| Dell G3           | Host machine for all VMs              | Physical Asset      |
| Myself            | The person testing everything         | Human Asset         |

---

## Step 2: Threats and Vulnerabilities

| Asset             | Threat Example                  | Vulnerability Example                           |
| ----------------- | ------------------------------- | ----------------------------------------------- |
| OpenCart (Ubuntu) | SQL Injection, defacement       | No input validation, old software version       |
| Windows 10        | Malware, phishing, ransomware   | Weak password, no antivirus                     |
| pfSense           | Bypass firewall, rule misconfig | Default rules, no logging                       |
| Wazuh Server      | Log tampering or bypass         | No log integrity checks, default password       |
| Security Onion    | Missed attack detection         | Not tuned alerts, default config                |
| Metasploitable2   | Exploited by attacker           | Designed to be vulnerable – open ports/services |
| Kali Linux        | Misused or misconfigured        | Could accidentally harm other systems           |
| Myself            | Social engineering              | You may click malicious links or forget configs |

---

## Step 3: Risk Testing (Without Protection)

### Test 1: Nmap Scan on Metasploitable2
- **Tool used:** Nmap  
- **Command:** `nmap -sV 192.168.18.108`  
- **Findings:**
  - 23 open ports detected.
  - Outdated services include FTP, MySQL, Samba, Telnet, and more.
  - A backdoor shell is running on port 1524.

### Test 2: Nikto Scan on OpenCart
- **Tool used:** Nikto  
- **Command:** `nikto -h http://192.168.18.103`  
- **Findings:**
  - Missing headers: X-Frame-Options, X-Content-Type-Options
  - Insecure cookies and exposed configuration files
  - Public directory indexing enabled

### Screenshots
- ![Nmap Scan](./screenshots/nmap_scan.png)
- ![Nikto Scan](./screenshots/nikto_scan.png)

---

## Additional Evidence: Logs and Packet Captures

### Wireshark
- ![Wireshark Nmap](./screenshots/wireshark1.png)
- ![Wireshark Nikto](./screenshots/wireshark2.png)
- ![Wireshark TCP Stream](./screenshots/wireshark3.png)

### Kibana / Security Onion
- ![Kibana Alert 1](./screenshots/kibana1.png)
- ![Kibana Alert 2](./screenshots/kibana2.png)

These screenshots confirm that:
- Nmap and Nikto traffic was successfully captured
- Security Onion detected scanning behavior in real-time

---

## Step 4: Third-Party Risk Analysis

| Component         | Third-Party Involved       | Potential Risk                                   |
|------------------|----------------------------|--------------------------------------------------|
| OpenCart          | Payment plugin (e.g., PayPal) | Stolen card data via plugin vulnerability      |
| OpenCart          | Shipping API                | Exposure of customer delivery information        |
| Ubuntu Server     | Software repositories       | Malicious packages if repo is hijacked           |
| Wazuh             | External update sources     | False updates or backdoors in monitoring tool    |
| Kali Linux Tools  | Public tools (Nikto, Hydra) | Altered tools reporting false or risky behavior  |

---

## Step 5: Compliance Requirements Summary

| Standard     | Requirement Summary                        | Lab Relevance                                       |
|--------------|---------------------------------------------|----------------------------------------------------|
| ISO 27001    | Assess, manage, and mitigate risks          | Structured testing using Nmap, Nikto               |
| GDPR         | Protects EU citizen data                    | Customer data simulation in OpenCart               |
| PCI DSS      | Secures cardholder data                    | Payment system risks assessed                      |
| DPDPA        | Indian data privacy law                    | Third-party risks evaluated                        |
| IT Act 2000  | Prevents cybercrime                        | Simulated ethical attacks (Kali Linux)             |

---

## Step 6: GRC (Governance, Risk, and Compliance) Findings

### Governance

- Simulated security roles (admin + analyst)
- Used tools: pfSense (firewall), Wazuh (SIEM), Security Onion (IDS), Kali (scanner)

### Risk Management

- 23 open ports on Metasploitable2
- Weak headers and config files exposed on OpenCart
- Full vulnerability scan performed

### Compliance

- ISO, GDPR, PCI-DSS, and DPDPA matched to lab activity
- Tools and scenarios support data privacy and monitoring best practices

---

## Step 7: Conclusion and Next Steps

### Conclusion

This hands-on lab simulated a real business network to identify, test, and document risks. The full risk lifecycle was followed: asset identification, threat discovery, risk testing, compliance alignment, and reporting.

Key Takeaways:
- Found real vulnerabilities using Nmap and Nikto
- Captured evidence via Wireshark and Kibana
- Applied governance and mapped actions to legal standards

### Next Steps

- Apply protections: firewall rules, alerts, system updates
- Re-scan to confirm threat reduction
- Write Wazuh custom rules
- Continue documenting and sharing research on GitHub and LinkedIn

---

📁 **Screenshots saved in `/screenshots/` folder**

---

> ⚠️ For educational use only. Do not test on live systems without permission.
