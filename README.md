# NETWORKWALKS-B083-WK1-PM1-CYBERSECURITY-LAB-SETUP
A self-contained virtual laboratory designed to safely perform cybersecurity exercises and penetration testing using Kali Linux.
# **Virtual Penetration Testing Sandbox: Multi-OS Lab Setup**

**A secure, multi-node isolated environment constructed for ethical hacking, cross-platform vulnerability assessment, and network analysis.**

## **Executive Summary**

This project outlines the construction and expansion of a multi-OS virtual cybersecurity laboratory utilizing VirtualBox. The environment features a **Kali Linux** attacker instance alongside a diverse target network comprising **Windows 11, Windows 10, Windows Server 2016, and Android x86** virtual machines.  
The primary goal is to establish a safe, repeatable, and strictly controlled playground for practicing security concepts across desktop, server, and mobile operating systems. All instances reside on a private NAT network to enable controlled inter-node traffic, local subnet testing, and external patch management.  
> **⚠️ Ethical Disclaimer:** This laboratory and its toolsets are intended strictly for educational and authorized testing purposes. Activities must only be conducted against systems you explicitly own or have documented permission to test.

## 

## **Core Project Objectives**

* Deploy and configure a VirtualBox hypervisor on the host system.  
* Establish a private, dedicated NAT Network (10.0.0.0/24) for secure inter-VM communication.  
* Provision a **Kali Linux** instance to serve as the central security testing workstation.  
* Deploy multi-platform target nodes: **Windows 11**, **Windows 10**, **Windows Server 2016**, and **Android x86**.  
* Assign static IP addresses across all endpoint nodes to maintain a standardized testing matrix.  
* Execute cross-platform ICMP reachability and ping verification tests.  
* Validate external internet routing and DNS resolution.  
* Capture clean system snapshots for every VM node to establish reliable recovery baselines.

## **Complete Environment Specifications**

| Node / Category | System Type | IP Address | Subnet / Mask | Memory Allocation | Purpose |
| :---- | :---- | :---- | :---- | :---- | :---- |
| **Host System** | Windows 10 (Intel i7) | Host IP | N/A | 8 GB RAM | Hypervisor Host |
| **Hypervisor** | VirtualBox 7.2 | N/A | N/A | N/A | Virtualization Layer |
| **Network Gateway** | NAT Network | 10.0.0.1 | 255.255.255.0 | N/A | Virtual Router / Gateway |
| **Kali Linux** | Security OS | 10.0.0.2 | 255.255.255.0 |  4096 MB | Primary Attacker Workstation |
| **Windows 11** | Workstation Target | 10.0.0.11 | 255.255.255.0 | 4096 MB | Modern Client OS Endpoint |
| **Windows 10** | Workstation Target | 10.0.0.10 | 255.255.255.0 | 4096 MB | Enterprise Client OS Endpoint |
| **Win Server 2016** | Server Target | 10.0.0.16 | 255.255.255.0 | 4096 MB | Active Directory / Server Target |
| **Android x86** | Mobile Target | 10.0.0.9 | 255.255.255.0 | 3096 MB | Mobile Application Security Target |

## 

## **Deployment & Configuration Lifecycle**

### **Phase 1: Prerequisite & Hypervisor Setup**

> 1. Download and install **7-Zip** to extract archive packages.  
> 2. Install **VirtualBox 7.2** with virtualization extensions.

### **Phase 2: Virtual Network Construction**

> 1. Create a dedicated NAT Network in VirtualBox named NatNetwork.  
> 2. Configure network parameters:  
   * **IPv4 Prefix:** 10.0.0.0/24  
   * **DHCP:** Enabled  
   * **IPv6:** Disabled

### **Phase 3: Attacker Workstation Deployment**

> 1. Import the **Kali Linux 2026.2** VM package into VirtualBox.  
> 2. Attach network adapter 1 to NatNetwork (Adapter Type: Intel PRO/1000 MT Desktop).  
> 3. Assign static IPv4 parameters:  
   * **IP Address:** 10.0.0.2/24  
   * **Gateway:** 10.0.0.1  
   * **DNS:** 8.8.8.8

### 

### **Phase 4: Optional Target VM Provisioning**

> 1. **Windows 11 Target:** Provisioned with 4 GB RAM, attached to NatNetwork, and assigned static IP 10.0.0.11  
> 2. **Windows 10 Target:** Provisioned with 2 GB RAM, attached to NatNetwork, and assigned static IP 10.0.0.10  
> 3. **Windows Server 2016 Target:** Configured with 2 GB RAM, attached to NatNetwork, and assigned static IP 10.0.0.16  
> 4. **Android x86 Target:** Deployed as an emulation instance attached to NatNetwork with static IP 10.0.0.09

### **Phase 5: Baseline Snapshotting**

Take clean baseline recovery snapshots across all nodes before executing tests or modifications:

* Clean Kali \- Network Setup  
* Clean Windows 11 \- Initial  
* Clean Windows 10 \- Initial  
* Clean Win Server 2016 \- Initial  
* Clean Android \- Initial

## 

## **Quality Assurance & Connectivity Verification**

Cross-node connectivity and routing tests were performed from the **Kali Linux** workstation (10.0.0.2) across the target ecosystem.

All systems passed the test  

<img width="1915" height="952" alt="image" src="https://github.com/user-attachments/assets/a9ef2fb1-aee5-4a14-bc88-0fd37a6846c2" />
<img width="1920" height="786" alt="Screenshot (160)" src="https://github.com/user-attachments/assets/8def83c8-326b-4db8-b859-5effeccf0bbf" />
<img width="1917" height="887" alt="image" src="https://github.com/user-attachments/assets/8d386402-15de-4549-9f10-d68786a86fd1" />


## **Troubleshooting Log**

* **DNS Routing Failure Post-Static Configuration**
  **Symptom:** Loss of internet connection on Kali after applying manual interface settings.
  **Resolution:** Executed sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0 and reset the network daemon.

* **Ping Request Timeouts on Windows Target Nodes**  
  **Symptom:** ICMP ping tests from Kali (10.0.0.2) to Windows 10/11/Server targets timed out, despite valid IP configurations.  
  **Resolution:** Enabled File and Printer Sharing (Echo Request \- ICMPv4-In) in the Windows Defender Firewall Advanced Rules on each target VM.


## 


## **Key Takeaways**

* **Cross-Platform Reconnaissance:** Expanding the lab to include Windows Client, Windows Server, and Android platforms provides broad exposure to diverse network stacks and OS behavior.  
* **Isolated Subnet Management:** Confirmed that a single NatNetwork segment safely manages multi-node environments while preventing unwanted traffic exposure to the host network.  
* **Snapshot Hygiene:** Validated that taking snapshots immediately after OS setup ensures fast recovery during testing phases.

## **Metadata & Tools**

* **Author:** Abel Alex  
* **Program Context:** Cybersecurity Lab Setup Series  
* **Resource Links:** [VirtualBox Download](https://virtualbox.org/wiki/Downloads), [Kali Linux Download](https://www.google.com/search?q=https://kali.org/get-kali), [7-Zip Tools](https://7-zip.org/download.html)
qhLPRZXKyIx04vOXCM3ZhO23YTWfaMeXtXiVC7bNm7yW3xUV/jRj30d7ujQZG93avGZmAehoyIquEYW1FNr9VCsmVs511wKtTK5yNjpOTPdLgIBeEp+giG8MW2rCPefBqrxlx9V/z1rftyDnh8Xg8Ho+nf3mN+LfjTuP4DY/H4/F4PP2IuG9/zY7+n//n//l//p//5/8Nr3//D9zDohVMvavcAAAAAElFTkSuQmCC>
