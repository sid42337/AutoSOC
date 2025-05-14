# Tool Installation & Configuration

---

### Sysmon setup in Windows-10

1. Downloading Sysmon from Microsoft
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image.png)
    
2. Downloading Configuration file (.xml) from GitHub
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%201.png)
    
3. Installing Sysmon using PowerShell
    
    Admin rights are required to the PowerShell is open with Admin right
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%202.png)
    
4. Check if “Sysmon” have been installed
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%203.png)
    

---

### TheHive Server setup on Cloud (Digital Ocean)

**Installation:**

Requirements: 

1. Java - Programming Language
2. Cassandra - NoSQL Database
3. ElasticSearch - Search and analytic engine

After installing these prerequisites, start installing TheHive

![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%204.png)

Command :

wget -O- [https://archives.strangebee.com/keys/strangebee.gpg](https://archives.strangebee.com/keys/strangebee.gpg) | sudo gpg --dearmor -o /usr/share/keyrings/strangebee-archive-keyring.gpg
echo 'deb [signed-by=/usr/share/keyrings/strangebee-archive-keyring.gpg] [https://deb.strangebee.com](https://deb.strangebee.com/) thehive-5.2 main' | sudo tee -a /etc/apt/sources.list.d/strangebee.list
sudo apt-get update
sudo apt-get install -y thehive

Default Credentials on port : 9000
credentials are 'admin@thehive.local' with a password of 'secret'

**Configurations:**

1. Edit Cassandra’s Configuration files.
    
    Location of config file: /etc/Cassandra/Cassandra.yaml
    
    1. Change the Cluster Name to “AutoSOC”
        
        ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%205.png)
        
    2. Change “listen_address” to the public address of the TheHive (209.38.142.194)
        
        ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%206.png)
        
    3. Change “rpc_address” to the public address of the TheHive (209.38.142.194). The rpc_address is the address of Cassandra Server that TheHive uses.
        
        ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%207.png)
        
    4. Change the “seed_provider” to the public address of TheHive
    
2. Stop Cassandra and remove the old file which was downloaded from the package. After deleting start the Cassandra 
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%208.png)
    
3. Edit Elasticsearch’s Configuration files.
    
    Location of config file: /etc/elasticsearch/elasticsearch.yml
    
    1. Change the Cluster Name to “thehive”
        
        ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%209.png)
        
    2. Remove the comment for “node.name: node-1”
        
        ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2010.png)
        
    3. Remove the comment for “network.host” and change the IP address to Public IP of TheHive
        
        ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2011.png)
        
    4. Remove he comment from “http.port”
        
        ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2012.png)
        
    5. Remove comment from “cluster.initial_master_nodes” and remove the “node-2” because we only have one node here.
        
        ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2013.png)
        
    
4. Start “elasticsearch” using systemctl . Then enable “elasticsearch”. Check its status using systemctl for confirmation.
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2014.png)
    
5. Check if hive user and group has access to a particular file path.
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2015.png)
    
    We can see that “root” is the owner and hive does not have access to it. We need to change that
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2016.png)
    
6. Edit TheHive’s Configuration files.
    1. Change all the “hostname” to TheHive Public IP
        
        ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2017.png)
        
    2. Change the “cluster-name” to AutoSOC ( should be same as the one entered in “Cassandra”)
        
        ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2018.png)
        
    3. Change the IP address in “application.baseURL” to TheHive Public IP
        
        ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2019.png)
        
    
7. Start “thehive” using systemctl. Check its status using systemctl for confirmation.
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2020.png)
    

---

### Wazuh Server setup on Cloud (DigitalOcean)

**Installation**

The Wazuh is installed using the command: “curl -sO [https://packages.wazuh.com/4.7/wazuh-install.sh](https://packages.wazuh.com/4.7/wazuh-install.sh) && sudo bash ./wazuh-install.sh -a” 

![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2021.png)

Installation is completed.

![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2022.png)

Note: (Do Not worry about showing the admin credentials in open as the all the droplets and VM’s have been deleted after the successful implementation of the project )

*This is being done because by default Wazuh does not display all logs. It only displays the logs which trigger and alert. So manually enable ingestion of all the logs*

**Configuring Wazuh manager to Log all system activity**

1. Create a backup of “ossec.conf” file before changing it.
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2023.png)
    
2. Open the “ossec.conf” file in nano
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2024.png)
    
    1. Change the “logall” to yes
        
        ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2025.png)
        
    2. Change the “logall_json” to yes
        
        ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2026.png)
        
    
3. Restart the “wazuh-manager” using systemctl
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2027.png)
    
    After restarting Wazuh will create an archive in which all the logs will be stored. Now configure it to start ingesting these logs.
    
4. Open the file “filebeat.yml” in nano.
    
    Change the value of “enabled” under “archives”, under “filebeat.modules” to true.
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2028.png)
    
5. Restart “filebeat” using systemctl
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2029.png)
    

---


### Mimikatz setup on Windows-10

1. Disable Windows Defender
2. Download Mimikatz zip file from github
3. Extract the file 
4. Open PowerShell with Administrator privileges and execute “mimikatz.exe”
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2038.png)
    

---

### Wazuh Dashboard Setup

**Create a new Index for archived logs**

1. Go to Stack Management → Index Patterns
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2039.png)
    
2. Add “wazuh-archives-*” logs
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2040.png)
    
3. Select “timestamp” for the “timefield”
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2041.png)
    

---

### Wazuh Agent Setup in Windows-10

**Setting up Wazuh agent**

1. Open the Wazuh dashboard on a bowser and enter the credentials

![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2030.png)

2. Since there are no agents installed, we will install one.
    1. Select the Windows as we will install the agent on windows-10 Client
        
        ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2031.png)
        
    2. Give Wazuh’s Public IP address in the Server address and Assign the Agent name as “AutoSOC”
        
        ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2032.png)
        
    3. Now copy the “Run” command and run the command in the PowerShell of the Windows-10 Client with administrator privileges.
        
        ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2033.png)
        
        ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2034.png)
        

**Configuring Wazuh agent configuration file to ingest “Sysmon” logs**

file location: C:\Program Files (x86)\ossec-agent\ossec.conf

1. Add “localfile” tag under “Log Analysis” section
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2035.png)
    
2. Change the location to Sysmon channel name
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2036.png)
    
3. Remove the “Security” part and “System” part which are forwarding their respective logs only.
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2037.png)
    
4. Restart Wazuh service

---


### Shuffle Setup

**Workflow**

1. Configuring Wazuh to connect to Shuffle Webhook
    
    Add the URI provided to the “ossec.conf” file.
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2042.png)
    
2. Adding Regex in “SHA256 Regex” to filter the alert file to get hash value.
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2043.png)
    
3. Add “VirusTotal” to the workflow, authenticate it using the VirusTotal API key . Change “Find Action” to “Get a Hash Report” and take input from “SHA256-regex”
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2044.png)
    
4. Add “TheHive” to the workflow, authenticate it using the TheHive “SOAR user“ API key . Fill the details according to the information an Analyst would want .
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2045.png)
    
5. Now this is for the just sending the request. We will now edit this and add http API to send curl request to Wazuh to get authentication . Also add Wazuh API and edit the workflow to be able to send the responsive actions taken by the user.
    
    ![image.png](media/Tool%20Installation%20&%20Configuration%201d17b769b25a80ffa98bda6e9a4c5f3f/image%2046.png)
