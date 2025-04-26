# Conclusion

---

### ✅ **Summary of Achievements**

- Successfully designed and implemented an automated SOC simulation environment combining Wazuh, TheHive, and Shuffle.
- Developed custom detection rules to identify Mimikatz-based credential dumping using Sysmon logs.
- Integrated alert-to-case workflows, enabling real-time detection, case generation, and optional automated triage.
- Deployed and tested the entire setup across VirtualBox (client) and cloud (DigitalOcean) infrastructure.
- Gained hands-on experience in configuring SIEM, case management, and SOAR tools in a unified pipeline.

---

### 🧩 **What Can Be Improved**

- Alert correlation and enrichment can be expanded to handle more complex detection scenarios.
- Real-time monitoring dashboards or visualizations (e.g., Kibana) could enhance visibility.
- Some parts of the workflow are **semi-automated**; tighter integration between all tools could make the flow more seamless.
- More attack scenarios can be added to simulate a wider range of threats beyond Mimikatz.
- Enable response automation such as isolating the host, blocking IPs, or disabling user accounts via Shuffle.