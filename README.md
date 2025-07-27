# SYN Flood Mitigation 🛡️

A comprehensive 3rd semester cybersecurity project that demonstrates **SYN Flood (DoS/DDoS) attack simulation** and **mitigation techniques** using Windows Firewall. This project includes real-time email alerts, detailed attack logging, automated IP blocking capabilities and graphical representation.

## 📋 Project Overview

This project simulates a realistic SYN Flood attack scenario between two networked computers and demonstrates how to effectively mitigate such attacks using built-in Windows security features. The system provides comprehensive monitoring, logging, and notification capabilities for network security analysis.

**Author:** Ibrar Ul Hassan Shami

## ⚠️ Important Notes

- **All commands must be executed in Command Prompt (CMD) with Administrator privileges**
- Test files should be ignored during deployment
- Only the core script files listed below are required for the simulation

## 📁 Core Project Files

The following files are essential for the project execution:

1. **`TCP Getting Interface.py`** - Network interface discovery utility
2. **`TCP Server Script.py`** - Main server application
3. **`TCP Server Check.py`** - Server connectivity verification
4. **`TCP Flood Script.py`** - SYN flood attack simulator
5. **`TCP Mitigation Script.py`** - Attack detection and mitigation system

## 🚀 Deployment Guide

### Prerequisites

- **Two Windows PCs** connected to the same network
- **Python 3.x** installed on both machines
- **Administrator access** on both systems
- **Gmail account** with App Password enabled (for email notifications)

### Step 1: Network Configuration

Execute the following commands on **both PCs** in Administrator CMD:

#### 1.1 Allow Python Network Access

```cmd
netsh advfirewall firewall add rule name="AllowPythonPrivate" dir=in action=allow program="C:\Users\DELL\AppData\Local\Programs\Python\Python313\python.exe" profile=private

netsh advfirewall firewall add rule name="AllowPythonPublic" dir=in action=allow program="C:\Users\DELL\AppData\Local\Programs\Python\Python313\python.exe" profile=public
```

> **Note:** Adjust the Python path according to your installation directory

#### 1.2 Enable ICMP Communication

```cmd
netsh advfirewall firewall add rule name="Allow ICMPv4-In" protocol=icmpv4 dir=in action=allow
```

#### 1.3 Test Network Connectivity

Verify that both PCs can communicate:

```cmd
# From Attacker PC
ping [Server_PC_IP_Address]

# From Server PC  
ping [Attacker_PC_IP_Address]
```

**To find your IP address:** Run `ipconfig` and note the **IPv4 Address**

### Step 2: Port Configuration

Allow TCP traffic through the custom simulation port on **both PCs**:

```cmd
netsh advfirewall firewall add rule name="Allow TCP Port 9999" protocol=TCP dir=in localport=9999 action=allow
```

### Step 3: Script Configuration

#### 3.1 File Distribution

**Server PC Scripts:**
- `TCP Getting Interface.py`
- `TCP Server Script.py`
- `TCP Mitigation Script.py`

**Attacker PC Scripts:**
- `TCP Server Check.py`
- `TCP Flood Script.py`

#### 3.2 IP Address Configuration

Make the following modifications to the script files:

**`TCP Server Script.py`** (Line 7)
```python
# Enter the Server's IP address
server_ip = "YOUR_SERVER_IP_HERE"
```

**`TCP Server Check.py`** (Line 3)
```python
# Enter the Server's IP address
target_ip = "YOUR_SERVER_IP_HERE"
```

**`TCP Flood Script.py`**
```python
# Line 5: Enter the Server's IP address
target_ip = "YOUR_SERVER_IP_HERE"

# Line 16: Enter the Attacker's IP address
source_ip = "YOUR_ATTACKER_IP_HERE"
```

### Step 4: Email Configuration

#### 4.1 Set Environment Variables

Open **PowerShell as Administrator** on the Server PC and configure email credentials:

```powershell
$env:SENDER_EMAIL="your_sender@gmail.com"
$env:RECEIVER_EMAIL="your_receiver@gmail.com"
$env:EMAIL_PASSWORD="xxxx xxxx xxxx xxxx"
```

> **📧 Gmail App Password Setup:** Search "Gmail App Password setup" on YouTube for detailed instructions

#### 4.2 Verify Email Configuration

```powershell
echo $env:SENDER_EMAIL
echo $env:RECEIVER_EMAIL
echo $env:EMAIL_PASSWORD
```

#### 4.3 Launch Development Environment

```powershell
code .
```

## 🎯 Execution Sequence

Follow this **exact order** for proper simulation execution. **Run each command in a separate terminal window:**

### Phase 1: Server Setup

**On Server PC:**

1. **Discover Network Interface**
   ```bash
   python "TCP Getting Interface.py"
   ```
   📝 **Note down the network interface name** - you'll need this later!

2. **Start the Server**
   ```bash
   python "TCP Server Script.py"
   ```

### Phase 2: Connectivity Verification

**On Attacker PC:**

3. **Verify Server Connection**
   ```bash
   python "TCP Server Check.py"
   ```

### Phase 3: Mitigation System

**On Server PC:**

4. **Initialize Mitigation System**
   ```bash
   python "TCP Mitigation Script.py"
   ```
   
   **Configuration Example:**
   - **Threshold:** `3` (connections before blocking)
   - **Time Window:** `10` (seconds)
   - **Interface:** Select the interface noted in Step 1

### Phase 4: Attack Simulation

**On Attacker PC:**

5. **Launch SYN Flood Attack**
   ```bash
   python "TCP Flood Script.py"
   ```

## 🎉 Results

Once all scripts are running, you'll observe:

- **Real-time attack detection** on the server
- **Automatic IP blocking** via Windows Firewall
- **Email notifications** sent to configured recipients
- **Detailed logging** of attack patterns and mitigation actions
- **Live monitoring** of network traffic and blocked connections

## 🔍 Learning Outcomes

This project demonstrates:

- **Network Security Fundamentals**
- **DoS/DDoS Attack Mechanics**
- **Windows Firewall Integration**
- **Real-time Threat Detection**
- **Automated Response Systems**
- **Network Traffic Analysis**

## 🎓 Educational Note

> **"Poke around and find out!"** - Experiment with different threshold values, time windows, and attack patterns to understand the relationship between attack intensity and mitigation effectiveness.

---
