# Active Directory Infrastructure Setup in Microsoft Azure
<p>
<p>

This guide walks you through setting up a Domain Controller (`dc-1`) and a client machine (`client-1`) in Microsoft Azure for lab/testing purposes.

---


📁 1. Create a Resource Group</summary>


- Go to the **Azure Portal** > **Resource Groups** > *Create*.

<img width="370" height="359" alt="image" src="https://github.com/user-attachments/assets/1e9fe007-feb7-4f8a-978c-d781febe87f5" />
  
- Set:
  
  - **Name**: `Active-D`
  - **Region**: your preferred region (e.g., `East US`)



---


🌐 2. Create a Virtual Network and Subnet</summary>

<img width="370" height="359" alt="image" src="https://github.com/user-attachments/assets/1a480008-8780-497c-9c4d-d3ac38c02ee2" />




- Go to **Virtual Networks** > *Create*.

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

<img width="370" height="359" alt="image" src="https://github.com/user-attachments/assets/4c41076b-80ea-42b7-93a4-1ef7fa90a150" />
  
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
 
<img width="483" height="361" alt="image" src="https://github.com/user-attachments/assets/9f7f545e-01e2-4238-8ee0-c237b3f0f8ee" />

    
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

<img width="370" height="359" alt="image" src="https://github.com/user-attachments/assets/2b216a88-34aa-4300-b2c8-d2110b9be1a9" />
  
- Configure:
  
  - **Name**: `client-1`
  - **Image**: Windows 10 (latest available)
  - **Username**: `labuser`
  - **Password**: `Cyberlab123!`
  - **Region**: same as dc-1
  - **Virtual Network**: `AD-VNet`
  - **Subnet**: `AD-Subnet`
  - **Public IP**: Enable
  - **Inbound Ports**: Allow **RDP (3389)**



---


🌐 6. Configure client-1 DNS Settings</summary>

- Go to **client-1** > **Networking** > **Network Settings** > **DNS Servers**
<p>
  <img width="150" height="350" alt="image" src="https://github.com/user-attachments/assets/ef16c031-8e9d-4e21-918b-405ae994c8a5" />

- Set:
  
  - **DNS**: **Custom**
  - Enter **dc-1’s private IP address**
    
- Click **Save**
  
- Go to **Client-1 VM** and **Restart** it from the Azure Portal






---
🔄 7. Test Network Connectivity</summary>

- RDP into **client-1**
  
- Open **PowerShell** or **Command Prompt**:
  
  - Run: `ping <DC-1 Private IP>`
  - Confirm that the ping is successful


- Run: `ipconfig /all`
  
  - Confirm that the **DNS Server** is set to **DC-1’s private IP**

<img width="830" height="169" alt="image" src="https://github.com/user-attachments/assets/396deab6-a2c6-4d47-b2a1-2992effe9f3e" />



