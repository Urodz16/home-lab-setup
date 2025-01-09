# Lab Setup Guide

This guide walks you through setting up a home lab for testing virtualization, configuring a Windows Domain Controller, a target Windows machine, and a Kali Linux attacker VM.

---

## Table of Contents
1. [Setup Virtualization Environment](#1-setup-virtualization-environment)
2. [Create Virtual Machines](#2-create-virtual-machines)
   - [Windows Server 2019 (DC) VM](#windows-server-2019-dc-vm)
   - [Windows Target VM](#windows-target-vm)
   - [Kali Linux Attacker VM](#kali-linux-attacker-vm)
3. [Network Setup](#3-network-setup)
4. [Further VM Setup](#4-further-vm-setup)
   - [Windows Server 2019 (DC) VM](#windows-server-2019-dc-vm-1)
   - [Creating Organizational Units (OUs) and Users](#creating-organizational-units-ous-and-users)
   - [Adding Target-PC to the Domain](#adding-target-pc-to-the-domain)
   - [Kali Linux Attacker VM](#kali-linux-attacker-vm-1)

---

## 1. Setup Virtualization Environment
1. **Download VirtualBox**:
   - Visit the [VirtualBox Official Site](https://www.virtualbox.org/) and download the latest version.
2. **Install VirtualBox**:
   - If prompted about missing prerequisites like Microsoft Visual C++ 2019, download it from [here](https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170).
   - Launch VirtualBox to verify it installed correctly.

**![SCREENSHOT HERE: VirtualBox](/screenshots/virtualbox-dashboard.png)**
A preview of what our end state will look like (plus a sneak peek of my Splunk Project!).

---

## 2. Create Virtual Machines

### **Windows Server 2019 (DC) VM**
1. Open VirtualBox and click **New**.
2. Name it `DC01` (optional, name it however you like).
3. Select your downloaded **Windows Server ISO**.
4. Check **"Skip Unattended Installation"**.
5. Allocate:
   - **RAM**: Normal (at least 2GB recommended).
   - **CPU**: 1 core is fine.
   - **Storage**: Over 50GB.
6. Start the VM and follow these installation steps:
   - Select your **language** and **keyboard layout**, then click **Install**.
   - Choose **Windows Server Desktop Edition**.
   - Select **Custom Installation**.
7. Complete the installation, create a **username and password**, and use the defaults to reach **Server Manager**.
8. Once you're in, **take a snapshot** in VirtualBox and name it "Base".
9. (Optional) Turn off the VM for now.

---

### **Windows Target VM**
1. Set up the Windows workstation:
   - Click **New** in VirtualBox, name it (e.g., `Workstation`), and select the **Windows 10 Pro ISO**.
   - Check **"Skip Unattended Installation"**.
   - Allocate resources:
     - **RAM**: Decent (e.g., 2GB+).
     - **Storage**: Over 50GB.
2. Start the VM and follow the installation process:
   - Choose your language and keyboard layout.
   - When prompted for a key, select **"I don’t have a key"**.
   - Select **Windows 10 Pro**.
   - Choose **Custom Installation**.
3. During setup:
   - Select **Office Environment** when asked (to prep it for a domain).
   - Set up a **local account** and password.
   - Skip location services, Cortana, and unnecessary features.
4. Verify login works, then take a **snapshot** named "Base".
5. Feel free to turn off the VM.

---

### **Kali Linux Attacker VM**
1. Download the **VirtualBox version** of Kali Linux from [Kali.org](https://www.kali.org/).
2. Unzip the downloaded file.
3. Double-click the `.ova` file (blue cube icon) to import it into VirtualBox.
4. Start the VM and log in:
   - **Username**: kali  
   - **Password**: kali
5. If successful, take a **snapshot** named "Base".

---

## 3. Network Setup

1. Open VirtualBox and go to **Tools** → **Network**.
2. Under **NAT Networks**, click **Create**.
   - Name it "HomeLab" (or something similar).
   - Adjust the **IPv4 Prefix** to match your intended network setup.
   - Leave **DHCP** enabled and click **Apply**.
3. For each VM:
   - Go to the **Settings** of the VM.
   - Under **Network**, attach **Adapter 1** to the NAT Network you just created.
   - Repeat this for all VMs.
4. Start all VMs and verify they’re on the same network.

**![VirtualBox NAT Network setup](/screenshots/nat-setup.png)**

---

## 4. Further VM Setup

### **Windows Server 2019 (DC) VM**
1. Log in and open **Server Manager**.
2. Rename the machine:
   - Click the name next to "Computer Name".
   - Select **Change**, rename it to `ADDC01` (Active Directory Domain Controller 01), and restart.
3. Assign a static IP:
   - Open **Network & Internet Settings** → **Change Adapter Options**.
   - Double-click **Ethernet** → **Properties** → **Internet Protocol Version 4**.
   - Set the following:
     - **IP Address**: 192.168.10.5
     - **Subnet**: 255.255.255.0
     - **Default Gateway**: 192.168.10.1
     - **DNS**: 8.8.8.8
   - Save and restart if prompted.
4. Take a **snapshot** named "Name and IP".
5. Set up Active Directory:
   - In **Server Manager**, go to **Manage** → **Add Roles and Features**.
   - Select **Active Directory Domain Services** and install it.
   - Once installed, promote the server to a domain controller:
     - Select **Add a new forest** → Name it `home.local`.
     - Leave the rest Default → Review Configuration.
     - Install and wait for server to restart.

**![ADDS Install](/screenshots/adds-install.png)**

---

### **Creating Organizational Units (OUs) and Users**
1. Open **Active Directory Users and Computers**:
   - In **Server Manager**, click **Tools** → **Active Directory Users and Computers**.
2. Create two Organizational Units (OUs):
   - Right-click the domain (`home.local`) → **New** → **Organizational Unit**.
   - Name the first OU **IT**, and the second **HR**.
3. Add users to each OU:
   - Right-click the **IT** OU → **New** → **User**.
     - Name: Tony Stark  
     - Logon Name: `tony.stark`
   - Repeat for the **HR** OU, creating Steve Rogers (`steve.rogers`).
4. Assign Tony Stark to the **Domain Admins** group:
   - Right-click Tony Stark → **Add to a group** → Type `Domain Admins` → OK.

**![Creating a user in AD](/screenshots/tony-stark.png)**

---

### **Adding Target-PC to the Domain**
1. Rename the Workstation PC to `Target-PC` and restart.
2. Set its static IP:
   - Use the same process as above but use:
     - **IP Address**: 192.168.10.10
     - **DNS**: 192.168.10.5 (points to DC).
3. Join the domain:
   - Open **Advanced System Settings** → **Computer Name** → **Change**.
   - Select **Domain** and type `home.local`.
   - Provide credentials for a domain admin (e.g., `tony.stark`).
   - Restart when prompted.

---

### **Kali Linux Attacker VM**
1. Verify it’s connected to the NAT Network and has internet access.
2. Use this VM for reconnaissance and attack simulations.

**![Network-diagram](/diagrams/network-diagram.png)**

---

## Notes for me
- Add scripts for automating repetitive tasks (e.g., AD user creation).
- Take snapshots frequently during setup.
- Document errors or troubleshooting steps in a separate file.
