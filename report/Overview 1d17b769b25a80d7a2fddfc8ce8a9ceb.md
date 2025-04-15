# Overview

---

### 🤖 **What is AutoSOC**

AutoSOC is a self-contained, simulated Security Operations Center (SOC) environment designed to demonstrate how security monitoring, alerting, and response workflows can be automated. It integrates open-source tools to detect and respond to simulated attacks with minimal manual intervention.

---

### 🎯 **Goals and Objectives**

- Create a practical SOC lab environment using open-source technologies.
- Automate alert triage, case creation, and basic incident response actions.
- Simulate real-world attack scenarios to test and validate the detection pipeline.
- Gain hands-on experience in SOC automation, SIEM, SOAR, and threat detection.

---

### ⚠️ **Problem Statement**

Traditional SOCs often deal with alert fatigue, manual processes, and delayed response times. This project addresses the need for automation in SOC operations by streamlining the detection and response pipeline, allowing faster and more reliable incident handling.

---

### ✨ **Key Features**

- Automated detection of credential dumping using Mimikatz.
- Custom Wazuh rule integration for behavior-based detection.
- End-to-end alert-to-case flow using Wazuh and TheHive.
- Optional automated response via Shuffle SOAR.
- Cloud-hosted server infrastructure and VM-based client for realistic simulation.

---

### 🔍 **Use Case**

Simulate a credential dumping attack on a Windows 10 client using Mimikatz. The attack is detected by Wazuh through a custom rule, sent to TheHive for case management, and optionally handled by Shuffle for automated response actions such as notifications or tagging.

---

### 🛠️ **Tools & Technologies Used**

- **Wazuh**
    
    Wazuh is an open-source SIEM that provides threat detection, integrity monitoring, and incident response capabilities. It collects and analyzes security events, applies custom rules, and generates alerts based on suspicious behavior observed in the system logs.
    
- **TheHive**
    
    TheHive is a scalable, open-source Security Incident Response Platform (SIRP) that helps manage and investigate alerts. It organizes security events into structured cases, allowing analysts to collaborate efficiently during incident handling.
    

- **Shuffle**
    
    Shuffle is an open-source SOAR (Security Orchestration, Automation, and Response) platform that connects various tools and automates repetitive SOC workflows. It helps reduce response time by triggering pre-defined actions on alerts without human intervention.
    

- **Mimikatz**
    
    Mimikatz is a powerful post-exploitation tool used to extract plaintext passwords, hash values, and Kerberos tickets from memory. In this project, it is used to simulate credential dumping attacks for testing the detection capabilities of the SOC setup.
    

- **Sysmon (System Monitor)**
    
    Sysmon is a Windows system service that logs detailed information about process creations, network connections, and file changes. It's used to monitor system activity and generate rich telemetry data for Wazuh to analyze and detect threats.
    
- DigitalOcean (Cloud Hosting)
    
    DigitalOcean provides a scalable cloud infrastructure where the Wazuh and TheHive servers are hosted. It allows for real-world deployment of detection and response tools in a reliable and accessible environment.
    
- VirtualBox (Virtualization)
    
    VirtualBox is used to create and run the Windows 10 client machine in a controlled virtual environment. It helps simulate endpoint activity and attacks, making the setup more flexible and isolated from the host system.