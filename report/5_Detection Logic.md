# Detection Logic

---

### Mimikatz Detection via Wazuh

**Creating a custom rule for Mimikatz**

1. Go to Management → Rules → Manage rules files
    
    ![image.png](media/Detection%20Logic%201d47b769b25a80bd8351d974cadaeb5d/image.png)
    
2. Now go to “Custom rules” and Open the file found to edit it to add the custom rule.
    
    ![image.png](media/Detection%20Logic%201d47b769b25a80bd8351d974cadaeb5d/image%201.png)
    

**Note:** 

- Indentation is very important in rules.
- Custom rules is start after 100000
- Case sensitivity

**Rule:**

```jsx
<rule id="100002" level="15">
  <if_group>sysmon_event1</if_group>
  <field name="win.eventdata.originalFileName" type="pcre2">(?i)mimikatz\.exe</field>
  <description>Mimikatz usage Detected</description>
  <mitre>
    <id>T1003</id>
  </mitre>
</rule>

```

Explanation

- **Rule ID:** `100002` – Custom rule ID to avoid conflict with built-in Wazuh rules
- **Level:** `15` – High severity, indicating a critical security event
- **If Group:** `sysmon_event1` – Refers to Sysmon Event ID 1 (Process Creation)
- **Field Monitored:** `originalFileName` – Detects if the process name matches `mimikatz.exe` (case-insensitive)
- **Regex Used:** `(?i)mimikatz\.exe` – Ensures detection regardless of case
- **MITRE Mapping:** `T1003` – Credential Dumping

**How It Works**

1. Sysmon logs process creation events on the Windows 10 client.
2. Wazuh agent reads and parses the logs, sending them to the Wazuh server.
3. The custom rule matches if `mimikatz.exe` appears in `originalFileName`.
4. If a match is found, an alert is generated with severity level 15. (Level 15 just for fun :) )
5. The alert is forwarded to TheHive via integration for case creation.
6. Shuffle can pick up the alert and trigger automation workflows (optional).