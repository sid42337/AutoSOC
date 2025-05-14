# VMs/Environment Setup

---

The AutoSOC environment consists of a **hybrid setup** with the Windows client running locally and the servers hosted on the cloud:

| Component | Role | Location | OS  |
| --- | --- | --- | --- |
| `Win10-Client` | Endpoint / Log Source | VirtualBox (Local) | Windows 10 (x64) |
| `Wazuh-Server` | SIEM + XDR Manager | DigitalOcean (Cloud) | Ubuntu 22.04 |
| `TheHive-Server` | Case Management | DigitalOcean (Cloud) | Ubuntu 22.04 |

---

### 💻 System Specifications

| VM / Server | CPU Cores | RAM | Disk Space |
| --- | --- | --- | --- |
| `Win10-Client` | 2 | 4 GB | 50 GB |
| `Wazuh-Server` | 2 | 8 GB | 160 GB |
| `TheHive-Server` | 2 | 8 GB | 160 GB |

---

### ⚙️ Deployment Breakdown

### 💻 **Windows 10 Client**

![image.png](media/VMs%20Environment%20Setup%201d17b769b25a8016a44cc28d6389400b/image.png)

- Acts as the victim machine
- Sends logs to the Wazuh Server over the internet
- Tools:
    - Wazuh Agent (configured to forward to public IP of Wazuh Server)
    - “Sysmon” for rich log generation
    - “Mimikatz” for simulating an attack
    

### ☁️ **Wazuh Server**

![image.png](media/VMs%20Environment%20Setup%201d17b769b25a8016a44cc28d6389400b/image%201.png)

- Collects and analyzes logs from Windows client

### ☁️ **TheHive**

![image.png](media/VMs%20Environment%20Setup%201d17b769b25a8016a44cc28d6389400b/image%202.png)

- Manages incidents and runs automation
- Shuffle connects to Wazuh API + internet for enrichment

---

### 🌐 Network Diagram

![Network Diagram.PNG](media/VMs%20Environment%20Setup%201d17b769b25a8016a44cc28d6389400b/Network_Diagram.png)

---

### 🔥 Firewall Configuration

- Custom Firewall rule allowing ICMP, TCP and UDP data from the Client’s Public IP only.

![image.png](media/VMs%20Environment%20Setup%201d17b769b25a8016a44cc28d6389400b/image%203.png)

![image.png](media/VMs%20Environment%20Setup%201d17b769b25a8016a44cc28d6389400b/image%204.png)
