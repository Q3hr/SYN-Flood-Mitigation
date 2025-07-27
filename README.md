# SYN-Flood-Mitigation
This 3rd Semester Project was created to simulate a SYN Flood (DoS/DDoS) on a Server and it how it is mitigated via the Windows Firewall. It also contains email alerts, attack logs and blocked IP logs.

**Author**: Ibrar Ul Hassan Shami

## ⚠️ Important Notes

1. **All commands must be run in Command Prompt (CMD) with Administrator privileges.**
2. **Ignore all test files.**
3. Only these files are important:
   - `TCP Getting Interface.py`
   - `TCP Server Script.py`
   - `TCP Server Check.py`
   - `TCP Flood Script.py`
   - `TCP Mitigation Script.py`

---

## 🖥️ Deployment Guide

### Step 1: Setup

- Acquire **two PCs** on the **same internet connection** (one will act as **Server**, the other as **Attacker**).

---

### Step 2: Allow Python through Windows Firewall

Run the following commands on **both PCs** (adjust the path to your installed Python version if necessary):

```cmd
netsh advfirewall firewall add rule name="AllowPythonPrivate" dir=in action=allow program="C:\Users\DELL\AppData\Local\Programs\Python\Python313\python.exe" profile=private

Step 3: Enable ICMP (Ping) Communication
Allow ICMP traffic on both PCs:

cmd
Copy
Edit
netsh advfirewall firewall add rule name="Allow ICMPv4-In" protocol=icmpv4 dir=in action=allow
Test communication:

c
Copy
Edit
Attacker_PC: ping <Server_PC_IP>
Server_PC: ping <Attacker_PC_IP>
You can get the IP address by running ipconfig and checking the IPv4 Address.

Step 4: Allow Custom TCP Port
Allow TCP traffic through port 9999 on both machines:

cmd
Copy
Edit
netsh advfirewall firewall add rule name="Allow TCP Port 9999" protocol=TCP dir=in localport=9999 action=allow
Step 5: Code Configuration
💻 Server PC Scripts:
TCP Getting Interface.py

TCP Server Script.py

TCP Mitigation Script.py

🧨 Attacker PC Scripts:
TCP Server Check.py

TCP Flood Script.py

🔧 Modify the following lines:
TCP Server Script.py

Line 7 → Enter Server PC's IP

TCP Server Check.py

Line 3 → Enter Server PC's IP

TCP Flood Script.py

Line 5 → Enter Server PC's IP

Line 16 → Enter Attacker PC's IP

Step 6: Configure Email Alerts (Optional but Recommended)
In PowerShell (Admin) on Server PC, set environment variables:

powershell
Copy
Edit
$env:SENDER_EMAIL="sender@gmail.com"
$env:RECEIVER_EMAIL="receiver@gmail.com"
$env:EMAIL_PASSWORD="xxxx xxxx xxxx xxxx"
Verify the variables:

powershell
Copy
Edit
echo $env:SENDER_EMAIL
echo $env:RECEIVER_EMAIL
echo $env:EMAIL_PASSWORD
Now launch VS Code:

powershell
Copy
Edit
code .
Step 7: Running the Project
On Server PC:
cmd
Copy
Edit
python "TCP Getting Interface.py"
Note or remember the name of the active interface.

c
Copy
Edit
python "TCP Server Script.py"
On Attacker PC:
cmd
Copy
Edit
python "TCP Server Check.py"
Back to Server PC:
cmd
Copy
Edit
python "TCP Mitigation Script.py"
Enter appropriate values:

Example: Threshold: 3, Time: 10, then select your noted interface.

Finally, on Attacker PC:
cmd
Copy
Edit
python "TCP Flood Script.py"
✅ Result
Watch the magic happen! The server should detect the SYN Flood and take mitigation actions (like blocking the attacker's IP and sending alerts via email).

🔍 Final Note
Poke around and find out!
Explore the code, tweak the thresholds, and understand the working of real-time TCP flood detection.
