# Network-Attack-Simulation

## Objective
The Detection Lab is aimed to set up a virtualized network environment using VirtualBox, configure Ubuntu and Kali Linux virtual machines, and simulate network attacks and defenses. Key tasks included installing essential tools on both VMs, conducting a network scan using Kali Linux, configuring a firewall on Ubuntu for defense, and analyzing network traffic with Wireshark. This exercise demonstrates basic cybersecurity practices and network traffic monitoring in a controlled virtual environment.

## Skills Learned
- Configured VirtualBox to establish a NAT network
- Updating and upgrading Linux systems (Ubuntu and Kali).
- Installing essential tools and packages.
- Simulated network attacks using tools such as nmap.
- Configured and managed firewalls using UFW to secure the system.
- Captured and analyzed network traffic using Wireshark for monitoring and diagnostics.
- Applied IP addressing and routing concepts in a virtualized environment.
- Utilized Kali Linux to conduct reconnaissance and vulnerability scans.
- Diagnosed and resolved network connectivity and configuration issues.

## Tools Used
- Virtualization Platform (VirtualBox): Used for creating and managing virtual machines and virtual networks.
- Linux Operating Systems (Ubuntu and Kali Linux): Ubuntu as the target system for defense, and Kali Linux as the offensive security platform for network scanning and penetration testing.
- Network Scanning Tools (Nmap): Utilized for reconnaissance and vulnerability scanning.
- Firewall Configuration Tool (UFW): Configured on Ubuntu to manage and secure inbound and outbound network traffic.
- Network Traffic Analysis Tool (Wireshark): Used for capturing and analyzing live network traffic to identify patterns and potential threats.
- Penetration Testing Framework (Metasploit): Optional tool for conducting advanced penetration testing and exploit simulations.
- System Utilities (Git, Curl, Build-essential): Installed on Ubuntu to support software development and system management tasks.

## Network Diagram:

![image](https://github.com/user-attachments/assets/83709f15-49f5-4fce-9d7b-4686c7ad69d4)


## Steps

### 1. Set Up VirtualBox and Network Configuration
- Create Virtual Machines:
Set up two virtual machines in VirtualBox:
#### Ubuntu VM (Target System)
#### Kali Linux VM (Attacker System)
- Configure Network Settings:
In VirtualBox, go to Settings -> Network.
Attach both VMs to a NAT Network to allow them to communicate with each other and the internet while remaining isolated from the host network.

- Create a NAT Network:
Go to File -> Preferences -> Network.
Under the NAT Networks tab, click Add and configure the network (e.g., 10.0.2.0/24).

![image](https://github.com/user-attachments/assets/b03d7bb8-36b3-4afb-bfaa-487627daaf09)

- Connect VMs to the NAT Network:
In each VM’s Settings -> Network -> Adapter 1, select Attached to: NAT Network, and choose the created NAT Network.

![image](https://github.com/user-attachments/assets/487c5e10-0a61-42e5-97cc-58729b35bce3)

A NAT Network is created to enable secure communication between virtual machines (e.g., Ubuntu and Kali Linux) while isolating them from the host's external network. This allows for safe simulations of network attacks, defenses, and internet access for updates and tool installations.
### 2. Install Required Tools on Each VM
#### On Ubuntu VM (Target System):

- Update the system:
```bash
  sudo apt update && sudo apt upgrade -y
```
![image](https://github.com/user-attachments/assets/111f5f6f-241b-4f1a-b121-43ad74e34aec)

- Installed tools needed for building software (build-essential), managing code (Git), and downloading files from the internet (Curl and Wget).
```bash
  sudo apt install -y build-essential git curl wget
```
![image](https://github.com/user-attachments/assets/ed3d3f86-8322-4ce6-a688-cacad30c09de)

#### On Kali Linux VM (Attacker System):

- Update the system:
```bash
  sudo apt update && sudo apt upgrade -y
```
![image](https://github.com/user-attachments/assets/00e799c3-9fc1-4b17-8b98-33be5bb3f766)

- Installed Nmap, Wireshark, and Metasploit for network scanning, traffic analysis, and penetration testing.
```bash
  sudo apt install -y nmap wireshark metasploit-framework
```
![image](https://github.com/user-attachments/assets/c2f13764-a59a-4929-868e-7c36accfb6b8)

- check ip address on kali os
```bash
  ip a
```
![image](https://github.com/user-attachments/assets/75ec8cbe-64a2-4f51-aa3b-249d9d2a00b6)

- check ip address on ubuntu os
```bash
  ip a
```
![image](https://github.com/user-attachments/assets/52c4c8a2-1a57-4571-ba5b-0f9d76cd76cc)

### 3. Defend Against the Attack
#### On Ubuntu VM (Target):
-Install and enable UFW (Uncomplicated Firewall) to protect the system:
```bash
  sudo apt install ufw
```
![image](https://github.com/user-attachments/assets/ec3d45ab-d57a-44fa-b779-ff8b714d7979)

```bash
  sudo ufw enable
```
- Allow SSH connections to ensure remote access:
```bash
  sudo ufw allow ssh
```
![image](https://github.com/user-attachments/assets/c3defec1-1220-4b36-ae12-13d690089b04)

- Allow traffic only from Kali Linux VM IP:
```bash
  sudo ufw allow from 10.0.2.11
```
- Check the firewall status:
```bash
  sudo ufw status
```
![image](https://github.com/user-attachments/assets/11ea7e64-1dc1-4f90-b6fa-08b10b35b886)

### 4. Analyze Network Traffic
#### On Ubuntu VM (Target):
- Install Wireshark for capturing network traffic:
```bash
  sudo apt install wireshark
```
![image](https://github.com/user-attachments/assets/b7183c31-0381-4989-8fc5-e4e6f52aec14)

### 5. Disable the Firewall 
 #### On Ubuntu VM (Target):
 - turn off the firewall for allowing all traffic on target os.
```bash
  sudo ufw disable
```
![image](https://github.com/user-attachments/assets/1e4775fc-733e-48f4-bf31-0e0c225f51c1)


### 6. Simulate Network Attack
#### On Ubuntu VM (Target)
 - Start Wireshark and capture the network traffic to analyze incoming and outgoing packets.
```bash
  sudo wireshark
```
![image](https://github.com/user-attachments/assets/3a4ca74e-d397-4628-b0f5-83f5ebcace79)

#### On Kali Linux (Attacker):
Run a simple Nmap scan to discover open ports and services of the ubuntu VM : (10.0.2.15 > ubuntu ip)
```bash
  nmap -A 10.0.2.15
```
- We have successfully simulated an attack, as indicated by the red lines in the image below.
![image](https://github.com/user-attachments/assets/50bc309c-67a1-4d59-97b5-cff931faed41)

## Conclusion
This setup involves creating two VMs in VirtualBox: one with Ubuntu (target system) and one with Kali Linux (attacker system). Both VMs are connected via a NAT network, allowing them to communicate securely while isolated from the host system.

We installed necessary tools like Wireshark on Ubuntu and Nmap on Kali. On Ubuntu, we enabled UFW firewall for protection and allowed only Kali's IP to connect. After disabling the firewall for testing, we used Nmap on Kali to scan for open ports on Ubuntu, simulating a network attack. This setup demonstrates network attack simulations and defenses in a controlled environment.









