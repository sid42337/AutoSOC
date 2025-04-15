# Functional Flow

---

(Visual + description of your project structure.)

### 🧱 **Architecture Diagram**

![AutoSOC.png](Functional%20Flow%201d17b769b25a80f6a047f28cf18de23e/AutoSOC.png)

---

### 🔁 Data flow Diagram

![Basic Data Flow.png](Functional%20Flow%201d17b769b25a80f6a047f28cf18de23e/Basic_Data_Flow.png)

---

### 🧩 Functional Flow (Architecture + Data Movement)

1. **Windows 10 Client (Wazuh Agent)**
    
    → Sends system logs and security events to the **Wazuh Manager**.
    
2. **Wazuh Manager**
    
    → Receives events from the agent and processes them through detection rules.
    
    → If a threat is detected, it generates an alert.
    
3. **Wazuh Manager → Shuffle**
    
    → Alerts are sent to **Shuffle**, which acts as the central automation engine.
    
4. **Shuffle – Enrichment Phase**
    
    → Shuffle extracts IoCs (IP, hash, domain) from the alert.
    
    → Performs enrichment using services like VirusTotal, IPVoid, etc.
    
5. **Shuffle → TheHive**
    
    → After enrichment, Shuffle sends the alert (now enriched) to **TheHive** to create a new incident/case.
    
6. **Shuffle → Email System (via Internet)**
    
    → Sends an alert notification email to the **SOC Analyst** with key details.
    
7. **SOC Analyst**
    
    → Receives and reviews the alert email.
    
    → Investigates the case inside TheHive (connected via the internet or locally).
    
8. **SOC Analyst → Shuffle**
    
    → May trigger a response manually (via TheHive) or approve an automatic response.
    
    → Shuffle sends the response command to the relevant systems (e.g., IP block, host isolation).
    
9. **Shuffle → Wazuh Manager / Endpoint**
    
    → Shuffle issues response instructions (e.g., stop a process, isolate endpoint).
    
    → Wazuh Manager relays this to the endpoint for execution.
    
10. **Endpoint (Windows 10 Client)**
    
    → Performs the actual response action (e.g., blocks an IP, kills a process) as per Shuffle’s command.