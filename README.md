# Home Lab Setup: Windows Domain and Kali Linux

## Overview
This is the **first project** I'm sharing on GitHub! It documents the step-by-step process I used to create a home lab environment for learning and testing system administration and cybersecurity concepts. 

The lab includes:
- **Windows Domain Controller** (Active Directory) to manage a domain.
- **Windows workstation** joined to the domain for testing.
- **Kali Linux** for simulating attacks and exploring cybersecurity techniques.

This environment serves as a foundation for practicing skills such as:
- Creating and managing **Group Policy Objects (GPOs)**.
- Performing **mass user creation** in Active Directory.
- Analyzing and responding to cybersecurity threats.

Future repositories will build on this lab, showcasing advanced Active Directory configurations and automation scripts.

---

## Objectives
- **Set up a secure Windows domain environment**.
- **Test Active Directory features** like GPOs and user management.
- **Simulate cybersecurity attacks** using Kali Linux.
- Analyze logs and improve defenses based on observed attack behaviors.

---

## Repository Structure
- **`documentation/`**: Detailed guides for setting up the lab and its components.
- **`configurations/`**: Configuration files for virtual machines, network settings, and AD structure.
- **`diagrams/`**: Visual representations of the lab setup, including network topology and workflows.
- **`examples/`**: Logs and reports from attack simulations and event analysis.

---

## Key Features
- **Active Directory Management**:
  - Create Organizational Units (OUs), users, and groups.
  - Manage Group Policy Objects (GPOs) for configuring domain-wide settings.
- **Attack Simulations**:
  - Perform reconnaissance and simulated exploits using Kali Linux tools like Nmap and Metasploit.
- **Log Analysis**:
  - Use Windows Event Viewer to track suspicious activities and analyze attack traces.
- **Scalable Design**:
  - Designed to grow as I add features like automated scripts and a SIEM server (Splunk).

---

## Getting Started
Follow these steps to replicate the home lab:
1. **Install VirtualBox**:
   - Download and install VirtualBox from [virtualbox.org](https://www.virtualbox.org/).
   - Install the VirtualBox Extension Pack for enhanced functionality.
2. **Set Up Virtual Machines**:
   - Follow the [Lab Setup Guide](documentation/lab-setup-guide.md) to configure the Windows Domain Controller, Windows workstation, and Kali Linux attacker VM.
3. **Experiment and Analyze**:
   - Use the lab to practice Active Directory tasks like GPO creation and user management.
   - Simulate attacks and analyze logs from the domain and workstation VMs.

---

## Why This Lab?
This lab represents the **starting point** for many of the projects I plan to share on GitHub. It provides:
- A platform to test and document my skills in system administration and cybersecurity.
- A way to practice **Active Directory configurations** like GPOs and automated user creation.
- A foundation for exploring advanced topics, such as SIEM integration and attack detection.

---

## Future Plans
- **Mass User Creation**: Automate bulk user creation in Active Directory using PowerShell.
- **Advanced GPO Management**: Apply custom GPOs to enforce security policies across the domain.
- **SIEM Integration**: Add a Splunk server to centralize log collection and analysis.
- **Custom Attack Scenarios**: Simulate more advanced threats like lateral movement and privilege escalation.

---

## Learning Outcomes
Through this project, you (and I!) will:
- Gain hands-on experience with Active Directory and domain management.
- Learn to build a functional virtualized network using VirtualBox.
- Understand how basic cybersecurity attacks work and how to detect them.
- Build a reusable guide for creating home labs.

---

## Contributing
This project is a work in progress! Feedback and suggestions are welcome. If you have ideas for improvements or extensions, feel free to open an issue or submit a pull request.

---

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.