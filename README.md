# Active Directory Infrastructure Setup in Microsoft Azure
<p>
<p>

This guide walks you through setting up a Domain Controller (`dc-1`) and a client machine (`client-1`) in Microsoft Azure for lab/testing purposes.

---


📁 1. Create a Resource Group</summary>


- Go to the **Azure Portal** > **Resource Groups** > *Create*.

  <img width="463" height="449" alt="Image" src="https://github.com/user-attachments/assets/195d5ff3-6037-4586-8748-555513616761" />
  
- Set:
  
  - **Name**: `Active-D`
  - **Region**: your preferred region (e.g., `East US`)



---


🌐 2. Create a Virtual Network and Subnet</summary>



- Go to **Virtual Networks** > *Create*.

  <img width="466" height="449" alt="Image" src="https://github.com/user-attachments/assets/7eaa8600-066f-453f-a7e1-a2af0c7fd8de" />


- Configure:
  
  - **Name**: `AD-VNet`
  - **Address space**: `10.0.0.0/16`
  - **Subnet name**: `AD-Subnet`
  - **Subnet range**: `10.0.1.0/24`
  - **Region**: same as the Resource Group



---


🖥️ 3. Create the Domain Controller VM (dc-1)</summary>
<p>



- Go to **Virtual Machines** > *Create*.

  <img width="548" height="444" alt="Image" src="https://github.com/user-attachments/assets/ed2da35c-813d-4541-ad75-abeda564be89" />
  
- Configure:
  
  - **Name**: `dc-1`
  - **Image**: Windows Server 2022
  - **Username**: `labuser`
  - **Password**: `Cyberlab123!`
  - **Region**: same as VNet
  - **Size**: `Standard_D2s_v3 - 2 vcpus, 8 GiB memory`
  - **Virtual Network**: `AD-VNet`
  - **Subnet**: `AD-Subnet`
  - **Public IP**: Enable (for RDP)
  - **Inbound Ports**: Allow **RDP (3389)**



---


🔧 4. Configure dc-1 Networking</summary>

<p>
  
- After VM creation:
  
  - Go to **dc-1** > **Networking** > **Network Settings** > **IP Configurations**
  - Set **Private IP address** to **Static**
  <p></p>

  <img width="483" height="361" alt="Image" src="https://github.com/user-attachments/assets/dbfcb103-40e0-4379-907a-90deb3cb3b5e" />
    
- RDP into **dc-1**
  
  - Open **Windows Defender Firewall**
  - Turn off the firewall for all profiles:
    - `Domain`
    - `Private`
    - `Public`
       
  ⚠️ *Only disable firewall in controlled lab environments.*



---


💻 5. Create the Client VM (client-1)</summary>

- Go to **Virtual Machines** > *Create*.

  <img width="546" height="420" alt="Image" src="https://github.com/user-attachments/assets/4eb2a1fc-4ba9-4ca6-a3f0-97768b26d870" />
  
- Configure:
  
  - **Name**: `client-1`
  - **Image**: `Windows 10` (latest available)
  - **Username**: `labuser`
  - **Password**: `Cyberlab123!`
  - **Region**: same as dc-1
  - **Virtual Network**: `AD-VNet`
  - **Subnet**: `AD-Subnet`
  - **Public IP**: `Enable`
  - **Inbound Ports**: `Allow` **RDP (3389)**



---


🌐 6. Configure client-1 DNS Settings</summary>

- Go to **client-1** > **Networking** > **Network Settings** > **DNS Servers**

  
  <img width="122" height="327" alt="Image" src="https://github.com/user-attachments/assets/d7e466ce-df12-4d54-9105-0f5d99c728d4" />

- Set:
  
  - **DNS**: **Custom**
  - Enter **dc-1’s private IP address**
    
- Click **Save**
  
- Go to **Client-1 VM** and **Restart** it from the Azure Portal






---
🔄 7. Test Network Connectivity</summary>

- RDP into **client-1**
  
- Open **PowerShell** or **Command Prompt**:
  
  - Run: `ping <dc-1 Private IP>`
  - Confirm that the ping is successful


- Run: `ipconfig /all`
  
  - Confirm that the **DNS Server** is set to **dc-1’s private IP**
    <p></p>

  <img width="830" height="169" alt="Image" src="https://github.com/user-attachments/assets/d2fd53b5-0c3e-421a-9039-4d17f6530de1" />



