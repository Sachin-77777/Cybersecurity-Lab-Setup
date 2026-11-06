# Practical Cybersecurity Lab Setup (VirtualBox & Kali Linux)

## Overview
This repository documents the setup of an isolated, practical cybersecurity lab environment created using Oracle VirtualBox and Kali Linux as part of the **Network Walks Cybersecurity Internship Program**.

The primary goal is to establish a secure, controlled testing environment featuring a custom NAT Network subnet (`10.0.0.0/24`), static IP configuration (`10.0.0.2/24`), and shared resource integration between host and guest operating systems.

---

## Lab Architecture & Technical Specifications

| Parameter | Configuration |
| :--- | :--- |
| **Host System** | Windows 11 |
| **Hypervisor** | Oracle VirtualBox v7+ |
| **Attacking VM** | Kali Linux (Latest 64-bit release) |
| **Network Mode** | Custom NAT Network (`NatNetwork`) |
| **Subnet Range** | `10.0.0.0/24` |
| **Kali Static IP** | `10.0.0.2/24` |
| **Default Gateway** | `10.0.0.1` |
| **DNS Server** | `8.8.8.8` |
| **Shared Resources** | Bidirectional Clipboard & Drag-and-Drop |

---

## Step-by-Step Implementation

### Step 1: VirtualBox NAT Network Creation
1. Navigated to **VirtualBox Manager > Tools > Network > NAT Networks**.
2. Created a new custom network named `NatNetwork`.
3. Configured the IPv4 Prefix to `10.0.0.0/24` and verified **Enable DHCP** was selected.

### Step 2: Virtual Machine Settings & Guest Integration
1. **Network Adapter Setup:** Attached **Adapter 1** of the Kali VM to `NAT Network`, selected `NatNetwork`, and set Promiscuous Mode to `Allow All`.
2. **Shared Features:** Enabled **Bidirectional Shared Clipboard** and **Drag 'n' Drop** under **General > Advanced**.
3. **Shared Folder:** Mapped host folder `C:\Users\thinkpad\Downloads` to the VM with **Auto-mount** and **Full Access**.

### Step 3: Static IP Configuration inside Kali Linux
1. Booted Kali Linux and accessed **Network Manager** (`Edit Connections`).
2. Modified **Wired connection 1** IPv4 settings from DHCP to **Manual**:
   - **IP Address:** `10.0.0.2`
   - **Netmask:** `24`
   - **Gateway:** `10.0.0.1`
   - **DNS:** `8.8.8.8`

### Step 4: Troubleshooting & Network Verification
To prevent connection timeouts commonly observed in VirtualBox 7+ environments, the IPv4 DAD (Duplicate Address Detection) timeout was disabled via `nmcli`:

```bash
sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
sudo nmcli connection down "Wired connection 1"
sudo nmcli connection up "Wired connection 1"
```

### System Baseline Snapshot
Created a clean system baseline snapshot in VirtualBox titled:
My Fresh Kali Linux after installation
Visual Proof & Screenshots
1. NAT Network Configuration
<img width="959" height="539" alt="image" src="https://github.com/user-attachments/assets/f409753a-f80a-4484-999d-9643327343b6" />


2. Shared Folder Setup
<img width="667" height="368" alt="image" src="https://github.com/user-attachments/assets/a2cf4e4f-b985-4f89-ab6e-78d6586f1f13" />


3. Kali Linux Static IP Configuration
<img width="1066" height="562" alt="image" src="https://github.com/user-attachments/assets/d6d85409-b908-4c22-a9ad-2a43e0ff45d7" />


4. Terminal Ping & DAD Fix Verification
<img width="1030" height="570" alt="image" src="https://github.com/user-attachments/assets/f79cb95f-cb15-49e6-a9e7-96f33860d51f" />


Author & Acknowledgments
Author: Sachin Shrestha

Program: Network Walks Cybersecurity Internship Program
