# 🔍 Remote Code Execution Detection

---

## :bookmark_tabs: Overview

In this lab, I will create a detection rule for potential Remote Code Execution (RCE) activity, focusing on PowerShell being used to automate the download and installation of an application. I will execute a PowerShell command (via cmd.exe) that uses Invoke-WebRequest and Start-Process to silently download and install 7-Zip from a remote source to simulate suspicious behavior. Using this activity, I’ll write a KQL query that looks for any PowerShell processes calling Invoke-WebRequest (and optionally Start-Process) within the last hour for my VM. Finally, I’ll use that query to create a detection rule that identifies and alerts on this behavior as a possible RCE event.

---
## 🛡️ Why This Lab Is Important

This lab is important because it simulates real-world Remote Code Execution (RCE) techniques, showing how attackers often abuse trusted tools like PowerShell to quietly download and execute malicious payloads. By recreating this behavior, you gain hands-on experience detecting attacker tradecraft that blends in with normal administrative activity. Writing a KQL query to identify suspicious PowerShell usage builds your skills in log analysis, event correlation, and interpreting security telemetry, while creating the detection rule reinforces core threat detection engineering concepts. Overall, this lab strengthens your ability to recognize early attack behaviors and improve an organization’s capability to identify and respond to RCE threats.

---

## Steps to Complete
1. Create a Windows VM
3. Disable the Windows Firewall (To allow VM to be discovered by bad actor on the Internet more easily)
4. Onboard VM in MDE
5. Ensure the logs are showing up in one of the tables in KQL
<img width="983" height="639" alt="image" src="https://github.com/user-attachments/assets/eee846f2-922f-4f7f-bba4-c62d5ee05f90" />

5. Run the below command in PowerShell Script:
   
**cmd.exe /c powershell.exe -ExecutionPolicy Bypass -NoProfile -Command "Invoke-WebRequest -Uri 'https://sacyberrange00.blob.core.windows.net/vm-applications/7z2408-x64.exe' -OutFile C:\ProgramData\7z2408-x64.exe; Start-Process 'C:\programdata\7z2408-x64.exe' -ArgumentList '/S' -Wait"**

This command launches PowerShell with security restrictions bypassed to silently download an executable from a remote URL and then run it without any user interaction. In other words, it automates the download and installation of an application (7-zip) in a way that closely resembles how attackers perform Remote Code Execution.

6. Create a Detection Rule Specific to your VM. Go to Microsoft Defender > Advanced Hunting
<img width="1542" height="555" alt="image" src="https://github.com/user-attachments/assets/32431379-4c15-4933-9382-53e7674de31e" />

a. General
<img width="1045" height="1264" alt="Screenshot 2025-11-14 at 6 51 42 PM" src="https://github.com/user-attachments/assets/bfdf7923-b34b-4378-9c76-cf716cb01afd" />

b. Alert Settings
<img width="600" height="1255" alt="Screenshot 2025-11-14 at 7 12 14 PM" src="https://github.com/user-attachments/assets/09ec3375-0e3d-4e22-8129-fe0282345327" />


c. Automated Actions (Endpoint Detection Response)

<img width="1034" height="732" alt="Screenshot 2025-11-14 at 6 56 42 PM" src="https://github.com/user-attachments/assets/52711397-f4c7-4af1-92de-a8f0e712fc00" />

d. Review and Create
<img width="965" height="1572" alt="Screenshot 2025-11-14 at 6 58 29 PM" src="https://github.com/user-attachments/assets/05405822-03d6-46fc-a1dc-5e2ecbbf2011" />




 
