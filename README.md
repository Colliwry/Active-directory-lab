# Active Directory Lab on Oracle VirtualBox

This project involves setting up a virtualized Active Directory (AD) environment using Oracle VirtualBox. The lab simulates a real-world corporate network, providing hands-on experience with Active Directory administration, network security configurations, and penetration testing.

## Project Overview

In this lab, an isolated network is simulated where AD services are configured, security policies are enforced, and vulnerabilities are explored using various penetration testing techniques. This project demonstrates a deep understanding of Active Directory, security protocols, and attack vectors—an excellent addition to any Cybersecurity Analyst Portfolio.

## Tools & Technologies Utilized

- **Oracle VirtualBox:** Virtualization platform to simulate a secure AD environment.
- **Windows Server 2022/2019:** Operating system used to deploy Active Directory.
- **Windows 10:** Client machine used to join the domain and simulate user activity.
- **PowerShell:** For automation and managing Active Directory users and groups.
- **Mimikatz and BloodHound:** Tools for testing AD vulnerabilities and exploring privilege escalation paths.

## Project Steps

### Step 1: Install Oracle VirtualBox

- Download and install Oracle VirtualBox to efficiently manage virtual machines (VMs).
- Configure VirtualBox to allocate appropriate resources (e.g., RAM, CPU) for optimal VM performance.

### Step 2: Virtual Machine Setup

Create two VMs for the lab:

- **Domain Controller (DC):** The central component managing user authentication and network policies.
- **Client Machine (Windows 10):** Simulates an end-user device to join the domain and interact with the AD server.

#### Creating the Domain Controller (DC):

- Create a VM in VirtualBox running Windows Server 2022/2019.
- Allocate at least 2GB of RAM and 30GB of storage.
- Assign a static IP address (e.g., `192.168.1.10`) for stable internal communication.
- Install Active Directory Domain Services (AD DS) and promote the server to a Domain Controller (e.g., `example.local`).

#### Creating the Client Machine:

- Create a second VM running Windows 10.
- Set a static IP address (e.g., `192.168.1.20`) and configure the DNS to point to the DC’s IP (`192.168.1.10`).
- Configure the VM’s network adapter to use an Internal Network, ensuring isolation from external networks.

### Step 3: Configuring Networking for Secure Communication

- Assign static IP addresses to both VMs to avoid issues with dynamic IP assignment.
- Configure DNS on the Client VM to resolve the Domain Controller's address, enabling domain joining and resource access.

### Step 4: Installing and Configuring Active Directory

- Use Server Manager on the Domain Controller to install the AD DS role.
- Promote the server to a Domain Controller by creating a new domain (e.g., `example.local`) and configuring DNS to ensure a fully functional AD environment.

### Step 5: Joining the Client Machine to the Domain

- Change the domain settings on the Windows 10 Client to `example.local`.
- Provide Domain Administrator credentials and reboot the client machine.
- Log in using domain credentials to verify successful integration with the domain.

### Step 6: Adding Users and Managing Active Directory via PowerShell

- **Create Users via PowerShell:** Use the `New-ADUser` cmdlet. Example:

  ```powershell
  New-ADUser -Name "John Doe" -SamAccountName "jdoe" -UserPrincipalName "jdoe@example.local" -AccountPassword (ConvertTo-SecureString "P@ssw0rd" -AsPlainText -Force) -Enabled $true

