
## Installing the virtual machine
1.Virtualization software (such as VirtualBox or VMware Workstation)

2.An operating system ISO (such as Kali Linux, Ubuntu, or Windows)

## Step 1: Download VirtualBox
- Go to: https://www.virtualbox.org/wiki/Downloads
- Download the Windows hosts installer (if you're using Windows).
  <img width="1907" height="976" alt="6" src="https://github.com/user-attachments/assets/3e13b945-fdea-4fb7-84ca-11092fb71020" /><img width="1917" height="971" alt="8" src="https://github.com/user-attachments/assets/d9628563-75d5-4c6a-a52d-57024e757053" />

  <img width="1913" height="979" alt="7" src="https://github.com/user-attachments/assets/86005322-c651-41a0-999c-37b54b572001" />

<img width="1917" height="971" alt="8" src="https://github.com/user-attachments/assets/6690a89b-f0ac-4681-84f2-eb0c368d96b2" />

## Step 2: Install VirtualBox
- Double-click the downloaded .exe file.
- Click Next through the setup wizard.
- Accept the default options.
- Click Install.
- Click Finish when installation completes.

## Installing the Wazuh agent
 
## Step 3: Download an Operating System ISO
 Ubuntu: https://ubuntu.com/download/desktop
 <img width="1907" height="976" alt="1" src="https://github.com/user-attachments/assets/8bfc889f-d3aa-44dc-bd36-6f374f1dc7fa" />

## Step 4: Create a New Virtual Machine
- Open VirtualBox.
- Click New.
- Enter a name (e.g., Kali Linux).
- Select the downloaded ISO file.
- Allocate resources:
- RAM: 4 GB or more
- CPU: 2 cores or more
- Storage: 40–60 GB (dynamically allocated is fine)
- Click Finish.
<img width="972" height="735" alt="9" src="https://github.com/user-attachments/assets/1e1e6672-a83c-42f5-b918-0c4593810d99" />

## Step 5: Start the VM

- Select the VM and click Start.
- Follow the operating system installation process.

# Installing Wazuh

- Download and run the Wazuh installation assistant.
  <img width="1290" height="794" alt="11" src="https://github.com/user-attachments/assets/c4136497-254a-4a19-8b4d-e5d977859b9a" />
<img width="1314" height="800" alt="12" src="https://github.com/user-attachments/assets/ba86bcf6-c1f4-4284-a8ee-b08d51259fb9" />
"curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh && sudo bash ./wazuh-install.sh -a"
<img width="1277" height="805" alt="13" src="https://github.com/user-attachments/assets/c7841ed8-414f-422a-9267-bb800215f64c" />

Once the assistant finishes the installation, the output shows the access credentials and a message that confirms that the installation was successful.
<img width="770" height="188" alt="image" src="https://github.com/user-attachments/assets/f1e103ad-5b96-4448-a333-f8a03b4187fe" />
Step 1: Open the dashboard

In your browser: https://<VM-IP>

<img width="902" height="508" alt="Screenshot 2026-07-21 063451" src="https://github.com/user-attachments/assets/c2584daf-657a-44fe-9045-a7f7f1cac4ba" />
<img width="1904" height="1024" alt="17" src="https://github.com/user-attachments/assets/41212e96-1b6e-47d2-abc8-0c3267125841" />

- Username: admin
- Password: (generated password)

<img width="1919" height="1073" alt="18" src="https://github.com/user-attachments/assets/cfabd745-6f7f-4946-8ecf-493e7ed63e94" />

step 2. Add a Open Agent Management
Go to:

☰ Menu → Agents management → Summary → Deploy new agent. This wizard generates the correct installation command for your operating system.
<img width="473" height="982" alt="image" src="https://github.com/user-attachments/assets/425e890f-854e-4544-a9fc-5f90a84c55ad" />

Step 3: Select the agent settings
Operating System: Windows 
Server address: Your Wazuh Manager IP (for example, 172.24.-.-)
Agent name: e.g. win-agent
<img width="1917" height="1079" alt="Screenshot 2026-07-20 152145" src="https://github.com/user-attachments/assets/b1510d57-85b2-469e-9d24-15e00fe74569" />
<img width="1919" height="1077" alt="Screenshot 2026-07-20 152122" src="https://github.com/user-attachments/assets/115b9243-db09-4d79-8b92-de93ed3082bb" />

Step 4: Run the generated command on the agent machine
<img width="973" height="927" alt="Screenshot 2026-07-20 152219" src="https://github.com/user-attachments/assets/12d4dd22-b36d-4430-b3fc-faadc0b04b20" />

" Invoke-WebRequest -Uri https://packages.wazuh.com/4.x/windows/wazuh-agent-4.14.6-1.msi -OutFile $env:tmp\wazuh-agent; msiexec.exe /i $env:tmp\wazuh-agent /q WAZUH_MANAGER='172.24.-.-' WAZUH_AGENT_NAME='win' "
<img width="972" height="382" alt="Screenshot 2026-07-21 070410" src="https://github.com/user-attachments/assets/0143433d-5806-4b18-8b93-e8465d8566c0" />

" NET START Wazuh "
<img width="408" height="112" alt="Screenshot 2026-07-21 070842" src="https://github.com/user-attachments/assets/d5feb24e-a87c-475a-adb2-56dbe2b28a49" />

<img width="897" height="707" alt="Screenshot 2026-07-21 070915" src="https://github.com/user-attachments/assets/9ecf205e-4dc0-4467-b7fe-309e16a0ca34" />

step 5: Open the configuration file
- If it's not already open:
- sudo nano /var/ossec/etc/ossec.conf
  <img width="1918" height="257" alt="Screenshot 2026-07-21 043925" src="https://github.com/user-attachments/assets/f691ae90-283e-47cd-b173-5afa046d4da2" />
 - Enables JSON output for alerts.
Keep it as yes.
- Stores alerts in the alert log.
Keep it as yes.
<img width="1476" height="337" alt="Screenshot 2026-07-21 052804" src="https://github.com/user-attachments/assets/1bc4b681-5348-4f09-8168-d52ffcb30e1e" />

- no = File Integrity Monitoring (FIM) is enabled.
- yes = FIM is disabled.
<img width="1476" height="287" alt="Screenshot 2026-07-21 052823" src="https://github.com/user-attachments/assets/bd077c2b-8e07-4f26-85dc-3274d6705e8a" />

Agter Edit Run this " sudo systemctl restart wazuh-agent "

# VirusTotal Integration 






