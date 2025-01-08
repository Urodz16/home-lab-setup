# Troubleshooting Guide

This file lists common issues encountered while setting up the home lab and their solutions. If you run into other problems or find better fixes, feel free to open an issue or submit a pull request to contribute to this guide!

---

## Table of Contents
1. [Install Windows Server with Desktop Experience](#1-install-windows-server-with-desktop-experience)
2. [Error When Launching VMs for the First Time](#2-error-when-launching-vms-for-the-first-time)
3. [Cannot Ping Windows Computers](#3-cannot-ping-windows-computers)
4. [VMs Fail to Access the Internet](#4-vms-fail-to-access-the-internet)
5. [Host Machine Runs Out of Resources](#5-host-machine-runs-out-of-resources)
6. [Future Additions](#future-additions)

---

## 1. **Install Windows Server with Desktop Experience**
- **Issue**: You may accidentally install the version without a GUI (Core Edition) instead of Desktop Experience.
- **Fix**: During the Windows Server installation, ensure you select **Windows Server with Desktop Experience** to get the full GUI version.

---

## 2. **Error When Launching VMs for the First Time**
- **Issue**: Virtual machines fail to start and display a storage-related error message.
- **Fix**: Power off the VM, double-check the storage controller configuration in VirtualBox, and try starting it again.

---

## 3. **Cannot Ping Windows Computers**
- **Issue**: Windows machines are unresponsive to ping requests, even though they are on the same network.
- **Fix**: ICMP (ping) requests are blocked by default in Windows. Create a firewall rule to allow ICMP:
  1. Open **Windows Defender Firewall with Advanced Security**.
  2. Click **Inbound Rules** → **New Rule**.
  3. Select **Custom** → **Protocol and Ports**.
  4. Choose **ICMPv4** → Allow the connection.
  5. Apply the rule.

---

## 4. **VMs Fail to Access the Internet**
- **Issue**: VMs connected to the NAT network can't access the internet.
- **Fix**: Ensure the NAT network in VirtualBox is configured correctly:
  1. Go to **File** → **Preferences** → **Network** → **NAT Networks**.
  2. Verify the NAT network has DHCP enabled.
  3. Restart the VMs to apply the changes.

---

## 5. **Host Machine Runs Out of Resources**
- **Issue**: The host machine becomes slow or unresponsive while running multiple VMs.
- **Fix**:
  - Reduce the amount of RAM or CPU allocated to each VM.
  - Close unnecessary programs on the host machine.
  - Increase the host machine’s swap space (virtual memory).

---

## Future Additions
I’ll continue adding to this file as I encounter more issues during the setup or as I expand the lab.  
Feel free to **Issue** or submit a **Pull Request** if you find or fix any other issues while replicating this lab. Your contributions are welcome!
