# Active Directory Infrastructure Setup in Microsoft Azure
<p>
<p>

This guide walks you through setting up a Domain Controller (`DC-1`) and a client machine (`Client-1`) in Microsoft Azure for lab/testing purposes.

---


📁 1. Create a Resource Group</summary>

<img width="463" height="449" alt="image" src="https://github.com/user-attachments/assets/1e9fe007-feb7-4f8a-978c-d781febe87f5" />

- Go to the **Azure Portal** > **Resource Groups** > *Create*.
  
- Set:
  - **Name**: `Active-D`
  - **Region**: your preferred region (e.g., `East US`)



---


🌐 2. Create a Virtual Network and Subnet</summary>

<img width="466" height="449" alt="image" src="https://github.com/user-attachments/assets/1a480008-8780-497c-9c4d-d3ac38c02ee2" />




- Go to **Virtual Networks** > *Create*.

- Configure:
  - **Name**: `AD-VNet`
  - **Address space**: `10.0.0.0/16`
  - **Subnet name**: `AD-Subnet`
  - **Subnet range**: `10.0.1.0/24`
  - **Region**: same as the Resource Group



---


🖥️ 3. Create the Domain Controller VM (DC-1)</summary>

- Go to **Virtual Machines** > *Create*.
- Configure:
  - **Name**: `DC-1`
  - **Image**: Windows Server 2022
  - **Username**: `labuser`
  - **Password**: `Cyberlab123!`
  - **Region**: same as VNet
  - **Virtual Network**: `AD-VNet`
  - **Subnet**: `AD-Subnet`
  - **Public IP**: Enable (for RDP)
  - **Inbound Ports**: Allow **RDP (3389)**



---


🔧 4. Configure DC-1 Networking</summary>

- After VM creation:
  - Go to **DC-1** > **Networking** > **Network Interface** > **IP Configurations**
  - Set **Private IP address** to **Static**
- RDP into **DC-1**
  - Open **Windows Defender Firewall**
  - Turn off the firewall for all profiles:
    - Domain
    - Private
    - Public  
  ⚠️ *Only disable firewall in controlled lab environments.*



---


💻 5. Create the Client VM (Client-1)</summary>

- Go to **Virtual Machines** > *Create*.
- Configure:
  - **Name**: `Client-1`
  - **Image**: Windows 10 (latest available)
  - **Username**: `labuser`
  - **Password**: `Cyberlab123!`
  - **Region**: same as DC-1
  - **Virtual Network**: `AD-VNet`
  - **Subnet**: `AD-Subnet`
  - **Public IP**: Enable
  - **Inbound Ports**: Allow **RDP (3389)**



---


🌐 6. Configure Client-1 DNS Settings</summary>

- Go to **Client-1** > **Networking** > **Network Interface** > **DNS Servers**
- Set:
  - **DNS**: **Custom**
  - Enter **DC-1’s private IP address**
- Click **Save**
- Go to **Client-1 VM** and **Restart** it from the Azure Portal



---
🔄 7. Test Network Connectivity</summary>

- RDP into **Client-1**
- Open **PowerShell** or **Command Prompt**:
  - Run: `ping <DC-1 Private IP>`
  - Confirm that the ping is successful
- Run: `ipconfig /all`
  - Confirm that the **DNS Server** is set to **DC-1’s private IP**


