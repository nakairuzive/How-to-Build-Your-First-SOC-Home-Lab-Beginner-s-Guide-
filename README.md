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

<img src= "Home Lab Images/image (2).png.jpg" width = 600 height = 600>

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
    
  <img src= "Home Lab Images/image (3).png.jpg" width = 600 height = 600>
   
    
3. Run the installer and select **“Create installation media”**.
4. Use the recommended options for your PC, then choose **“ISO file”**.
5. Once the ISO finishes downloading, open VirtualBox and click **“New”**.
    
    <img src= "Home Lab Images/image (4).png.jpg" width = 600 height = 600>
    
6. Name your VM, select the folder location, and attach the ISO file.
    
    <img src= "Home Lab Images/image (5).png.jpg" width = 600 height = 600>
    
7. Assign resources based on your computer’s capacity. Recommended minimums:
- **Memory (RAM):** 2 GB (2048 MB)
- **Processors:** 1 CPU
- **Virtual Hard Disk:** 50 GB.
    
    <img src= "Home Lab Images/image (6).png.jpg" width = 600 height = 600>
    
    <img src= "Home Lab Images/image (7).png.jpg" width = 600 height = 600>
    
1. Complete the setup and click **“Start”** to launch your Windows VM.

💡 When asked for a product key, choose **“I don’t have a product key.”** You’ll still be able to complete the installation.

### 2.2 Downloading and Installing Kali Linux

Next, we’ll add Kali Linux to our lab.

1. Go to the [Kali Linux download page](https://www.kali.org/get-kali/).
2. Under **Virtual Machines**, select the **VirtualBox image**. (This option makes setup much faster.)
    
   <img src= "Home Lab Images/image (8).png.jpg" width = 600 height = 600>
    
    <img src= "Home Lab Images/image (9).png.jpg" width = 600 height = 600>
    
3. Install [7-Zip](https://www.7-zip.org/download.html) to extract the compressed folder.
    
    <img src= "Home Lab Images/image (10).png.jpg" width = 600 height = 600>
    
4. Right-click the downloaded Kali file → **7-Zip → Extract to…**
    
   <img src= "Home Lab Images/image (11).png.jpg" width = 600 height = 600>
    
   <img src= "Home Lab Images/image (12).png.jpg" width = 600 height = 600>
    
5. Open the extracted folder and double-click the file ending in **“.vbox.”**
    - This automatically imports Kali into VirtualBox.
        
        ![image.png](attachment:796d1256-9926-4bb0-ba84-a7899ce7fba8:image.png)
        
        ![image.png](attachment:d9215dcb-8107-4634-9762-30672dc390f8:image.png)
        
        ![image.png](attachment:97c70dd2-5e7a-4780-9006-52f7fe39767e:image.png)
        
6. Start the Kali VM.
**Step 6**: Kali user name and password

The default username is “kali” and the password is also “kali”

### 2.3 Install Splunk Enterprise onto your Windows machine

**Step 1**: Install Splunk Enterprise; without this, you will not be able to log in through your web browser

![image.png](attachment:f1125cd7-5854-4e1e-a2b7-844cc09120e1:image.png)

![image.png](attachment:aabdaa95-8748-4fa9-9881-b6975cb2cc35:image.png)

![image.png](attachment:edc8462a-d021-4f27-9e3d-ecc0ed7d785f:image.png)

![image.png](attachment:f85cf261-455c-4e24-96ba-8334715324ad:image.png)

![image.png](attachment:7db41287-3bf0-4959-9ee6-b69fda0a318b:image.png)

### **4.6 Sysmon Installation & Configuration**

<aside>

**Why Sysmon?** 

Windows Event Logs are good, but Sysmon is great. It provides incredibly detailed information about process creations, network connections, file changes, and more. Using a robust configuration file (like Olaf Hartong's) applies a set of rules to filter out noise and log only the most security-relevant events.

</aside>

**Step 1**: Use this link to download Sysmon https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon

![image.png](attachment:b0b64794-f6e4-4835-b456-a29ed07ef6d7:image.png)

**Step 2**: Extract the Sysmon download file

**Step 3**: To configure Sysmon, we will use the Olaf configuration. Open the RAW file, right-click and save the file as “sysmonconfig”, and save it to the extracted Sysmon file

> **Concept note:** Without a good configuration, Sysmon can overwhelm you with irrelevant logs. Using a community-tested config ensures you capture useful security events.
> 

https://github.com/olafhartong/sysmon-modular/blob/a9ff298f6d228c181be71b213c73d111c6096f41/sysmonconfig.xml

**Step 4**: Copy the path address of the Sysmon file in your downloads. Next, open “Windows PowerShell” and run it as an administrator

![image.png](attachment:36e7be7d-7761-4056-b222-3fba0a159d7b:image.png)

**Step 5**:  Type in “cd + path address”, there after type in “.\Sysmon64.exe -i .\sysmonconfig.xml” to install Sysmon

![image.png](attachment:f0dcae88-db0c-410f-b584-6b018b34c51b:image.png)

> **Concept note:** Native Windows logs (like Security logs) capture basic events (e.g., logon success/failure). Sysmon adds the *depth* you need for threat detection, making it essential in a detection lab.
> 

## Chapter 3: Configure your network as an internal network

To reduce the risk of compromising your host machine when analysing malware in the virtual machine, we can reconfigure the network settings of the virtual machines.

**Step 1**: Open VirtualBox. 

**Step 2**: Click on the Windows Machine and then select the “Settings” option on the menubar and head to “Network”

**Step 3**: Change the network to an internal network, and give the network a name.

![image.png](attachment:acad5f95-fda2-435f-a885-d3e53362fa0c:image.png)

**Step 4**: Repeat the same steps for the Kali Machine

![image.png](attachment:bbb9660d-6557-4f61-a0d7-70d52aeca733:image.png)

![image.png](attachment:45a28631-0166-4f39-b612-a007e3953d41:image.png)

**Step 5**: Log on to your Windows machine

**Step 6**: Open the “Network and Internet settings” form, and there select the option to “Change network adapter”

![image.png](attachment:bd06ed3e-9272-4d06-a470-01ed4add968d:image.png)

![image.png](attachment:2d260c18-9775-4e16-98d9-fca8f43f3419:image.png)

**Step 7**: Open the Ethernet properties, select IPv4 and make the following changes

IP address: Pick your own IP address 

**Use this as a guide: 192.168.10.0/24** → usable IPs: `192.168.10.1` to `192.168.10.254`

Subnet Mask: 255.255.255.0

![image.png](attachment:b6eddbde-18a7-4e2a-a5c5-a55c2cbf10d6:image.png)

**Step 8**: Open the Command Prompt by typing in “cmd” into the search bar, and verify that your IP address has changed

**Step 9**: Log on to your Kali Machine

**Step 10**: Right-click on the Ethernet icon that can be found in the top right corner and select “Edit connections”

![image.png](attachment:5552c67b-20ed-45f3-9054-382c9823736e:image.png)

**Step 11**: Click on the “gear” icon at the bottom and make the following changes under “IPv4 Settings”

Method: Manual

Add a new Address:  **Use this as a guide: 192.168.10.0/24** → usable IPs: `192.168.10.1` to `192.168.10.254`

Netmask: 24

![image.png](attachment:895d1d57-83c1-4f81-aa4c-d91e16c943b3:image.png)

Hit the save button

**Step 12**: Right-click anywhere on the screen to open the terminal, type in “ifconfig” or “ip a” to verify the new IP address

![image.png](attachment:1b2d429d-42ba-43e9-9f01-1da564fd9c41:image.png)

**Step 13**: Check if there is connectivity between the two machines. On the Windows machine, open the command prompt to ping the Kali machine

Use this: ping IP(Kali)

- **Username:** `kali`
- **Password:** `kali`
