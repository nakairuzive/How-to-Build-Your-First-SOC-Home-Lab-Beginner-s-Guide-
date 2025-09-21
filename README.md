# How to Build Your First SOC Home Lab - Beginner's Guide
If you’re new to cybersecurity and looking for a structured, beginner-friendly way to get hands-on practice, you’re in the right place.

In this guide, I’ll walk you through the exact steps to set up your first **Security Operations Centre (SOC)** Home Lab. This is one of the best ways to gain practical experience, avoid common mistakes I made starting out, and show potential employers that you’re serious about learning.

Building a home lab demonstrates initiative, curiosity, and persistence—all qualities that will serve you well in the cybersecurity industry. Whether you’re still figuring out your career path or already have your eye on a SOC analyst role, this is an excellent starting point.

### Chapter 1: Choosing Your Virtualisation Environment

The first step is deciding where you want to host your **virtual machines (VMs)**. Virtual machines let you run multiple operating systems on a single computer.

There are many virtualisation platforms available, such as VMware Workstation, Hyper-V, and VirtualBox.

For this tutorial, we’ll be using **VirtualBox** because it’s free, widely used, and beginner-friendly.

---

[Use this link to download](https://www.virtualbox.org/wiki/Downloads)

<img src= "Home Lab Images/image (2).png" width = 600 height = 600>

Once downloaded:

1. Open the installer from your file explorer.
2. Follow the setup wizard and install VirtualBox.
3. Launch it—you’ll use this to create and manage your virtual machines.

### Chapter 2: Preparing Your Virtual Machines

One of the frustrations I had when learning from online tutorials was being told to “pause and download” software in the middle of the setup. To save you time, I recommend downloading everything up front.

For this beginner SOC lab, we’ll use two core systems:

- **Windows 10** (for simulating endpoints and practising detection)
- **Kali Linux** (a penetration testing and security tool powerhouse)

---

### 2.1 Downloading and Installing Windows 10

1. Go to the official [Windows 10 download page](https://www.microsoft.com/en-us/software-download/windows10).
    
  <img src= "Home Lab Images/image (3).png" width = 600 height = 600>
   
    
3. Run the installer and select **“Create installation media”**.
4. Use the recommended options for your PC, then choose **“ISO file”**.
5. Once the ISO finishes downloading, open VirtualBox and click **“New”**.
    
    <img src= "Home Lab Images/image (4).png" width = 600 height = 600>
    
6. Name your VM, select the folder location, and attach the ISO file.
    
    <img src= "Home Lab Images/image (5).png" width = 600 height = 600>
    
7. Assign resources based on your computer’s capacity. Recommended minimums:
- **Memory (RAM):** 2 GB (2048 MB)
- **Processors:** 1 CPU
- **Virtual Hard Disk:** 50 GB.
    
    <img src= "Home Lab Images/image (6).png" width = 600 height = 600>
    
    <img src= "Home Lab Images/image (7).png" width = 600 height = 600>
    
1. Complete the setup and click **“Start”** to launch your Windows VM.

💡 When asked for a product key, choose **“I don’t have a product key.”** You’ll still be able to complete the installation.

### 2.2 Downloading and Installing Kali Linux

Next, we’ll add Kali Linux to our lab.

1. Go to the [Kali Linux download page](https://www.kali.org/get-kali/).
2. Under **Virtual Machines**, select the **VirtualBox image**. (This option makes setup much faster.)
    
   <img src= "Home Lab Images/image (8).png" width = 600 height = 600>
    
    <img src= "Home Lab Images/image (9).png" width = 600 height = 600>
    
3. Install [7-Zip](https://www.7-zip.org/download.html) to extract the compressed folder.
    
    <img src= "Home Lab Images/image (10).png" width = 600 height = 600>
    
4. Right-click the downloaded Kali file → **7-Zip → Extract to…**
    
   <img src= "Home Lab Images/image (11).png" width = 600 height = 600>
    
   <img src= "Home Lab Images/image (12).png" width = 600 height = 600>
    
5. Open the extracted folder and double-click the file ending in **“.vbox.”**
    - This automatically imports Kali into VirtualBox.
        
       <img src= "Home Lab Images/image (13).png" width = 600 height = 600>
       <img src= "Home Lab Images/image (14).png" width = 600 height = 600>
       <img src= "Home Lab Images/image (15).png" width = 600 height = 600>
        
6. Start the Kali VM.
**Step 6**: Kali user name and password

The default username is “kali” and the password is also “kali”

### 2.3 Install Splunk Enterprise onto your Windows machine

**Step 1**: Install Splunk Enterprise; without this, you will not be able to log in through your web browser

<img src= "Home Lab Images/image (16).png" width = 600 height = 600>

<img src= "Home Lab Images/image (17).png" width = 600 height = 600>

<img src= "Home Lab Images/image (18).png" width = 600 height = 600>

<img src= "Home Lab Images/image (19).png" width = 600 height = 600>

<img src= "Home Lab Images/image (20).png" width = 600 height = 600>

### **2.4 Sysmon Installation & Configuration**

<aside>

**Why Sysmon?** 

Windows Event Logs are good, but Sysmon is great. It provides incredibly detailed information about process creations, network connections, file changes, and more. Using a robust configuration file (like Olaf Hartong's) applies a set of rules to filter out noise and log only the most security-relevant events.

</aside>

**Step 1**: Use this link to download Sysmon https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon

<img src= "Home Lab Images/image (21).png" width = 600 height = 600>

**Step 2**: Extract the Sysmon download file

**Step 3**: To configure Sysmon, we will use the Olaf configuration. Open the RAW file, right-click and save the file as “sysmonconfig”, and save it to the extracted Sysmon file

> **Concept note:** Without a good configuration, Sysmon can overwhelm you with irrelevant logs. Using a community-tested config ensures you capture useful security events.
> 

https://github.com/olafhartong/sysmon-modular/blob/a9ff298f6d228c181be71b213c73d111c6096f41/sysmonconfig.xml

**Step 4**: Copy the path address of the Sysmon file in your downloads. Next, open “Windows PowerShell” and run it as an administrator

<img src= "Home Lab Images/image (22).png" width = 600 height = 600>

**Step 5**:  Type in “cd + path address”, there after type in “.\Sysmon64.exe -i .\sysmonconfig.xml” to install Sysmon

<img src= "Home Lab Images/image (23).png" width = 600 height = 600>

> **Concept note:** Native Windows logs (like Security logs) capture basic events (e.g., logon success/failure). Sysmon adds the *depth* you need for threat detection, making it essential in a detection lab.
> 

## Chapter 3: Configure your network as an internal network

To reduce the risk of compromising your host machine when analysing malware in the virtual machine, we can reconfigure the network settings of the virtual machines.

**Step 1**: Open VirtualBox. 

**Step 2**: Click on the Windows Machine and then select the “Settings” option on the menubar and head to “Network”

**Step 3**: Change the network to an internal network, and give the network a name.

<img src= "Home Lab Images/image (24).png" width = 600 height = 600>

**Step 4**: Repeat the same steps for the Kali Machine

<img src= "Home Lab Images/image (25).png" width = 600 height = 600>

<img src= "Home Lab Images/image (26).png" width = 600 height = 600>

**Step 5**: Log on to your Windows machine

**Step 6**: Open the “Network and Internet settings” form, and there select the option to “Change network adapter”

<img src= "Home Lab Images/image (27).png" width = 600 height = 600>

<img src= "Home Lab Images/image (28).png" width = 600 height = 600>

**Step 7**: Open the Ethernet properties, select IPv4 and make the following changes

IP address: Pick your own IP address 

**Use this as a guide: 192.168.10.0/24** → usable IPs: `192.168.10.1` to `192.168.10.254`

Subnet Mask: 255.255.255.0

<img src= "Home Lab Images/image (29).png" width = 600 height = 600>

**Step 8**: Open the Command Prompt by typing in “cmd” into the search bar, and verify that your IP address has changed

**Step 9**: Log on to your Kali Machine

**Step 10**: Right-click on the Ethernet icon that can be found in the top right corner and select “Edit connections”

<img src= "Home Lab Images/image (30).png" width = 600 height = 600>

**Step 11**: Click on the “gear” icon at the bottom and make the following changes under “IPv4 Settings”

Method: Manual

Add a new Address:  **Use this as a guide: 192.168.10.0/24** → usable IPs: `192.168.10.1` to `192.168.10.254`

Netmask: 24
<img src= "Home Lab Images/image (31).png" width = 600 height = 600>

Hit the save button

**Step 12**: Right-click anywhere on the screen to open the terminal, type in “ifconfig” or “ip a” to verify the new IP address

<img src= "Home Lab Images/image (32).png" width = 600 height = 600>

**Step 13**: Check if there is connectivity between the two machines. On the Windows machine, open the command prompt to ping the Kali machine

Use this: ping IP(Kali)
<img src= "Home Lab Images/image (33).png" width = 600 height = 600>
