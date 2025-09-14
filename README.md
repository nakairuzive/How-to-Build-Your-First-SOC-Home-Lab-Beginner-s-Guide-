# How to Build Your First SOC Home Lab - Beginner's Guide
<p> If you’re new to cybersecurity and looking for a structured, beginner-friendly way to get hands-on practice, you’re in the right place.</p>

<p> In this guide, I’ll walk you through the exact steps to set up your first **Security Operations Centre (SOC) Home Lab**. This is one of the best ways to gain practical experience, avoid common mistakes I made starting out, and show potential employers that you’re serious about learning. </p>

<p> Building a home lab demonstrates initiative, curiosity, and persistence—all qualities that will serve you well in the cybersecurity industry. Whether you’re still figuring out your career path or already have your eye on a SOC analyst role, this is an excellent starting point.</p>

### Chapter 1: Choosing Your Virtualisation Environment

The first step is deciding where you want to host your **virtual machines (VMs)**. Virtual machines let you run multiple operating systems on a single computer.

There are many virtualisation platforms available, such as VMware Workstation, Hyper-V, and VirtualBox.

For this tutorial, we’ll be using **VirtualBox** because it’s free, widely used, and beginner-friendly.

---

Use this link to download: https://www.virtualbox.org/wiki/Downloads

![image alt](https://github.com/nakairuzive/How-to-Build-Your-First-SOC-Home-Lab-Beginner-s-Guide-/blob/76e6585eae044d70f3f511e5cdc6b9d609f201de/Blog%201/Kali%20img1.png)

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
    
    ![image.png](attachment:3021ea36-267e-419d-87d7-07c9b360d75a:image.png)
    
2. Run the installer and select **“Create installation media”**.
3. Use the recommended options for your PC, then choose **“ISO file”**.
4. Once the ISO finishes downloading, open VirtualBox and click **“New”**.
    
    ![image.png](attachment:99271e95-2e9c-4646-b222-ece3ee58e6c6:image.png)
    
5. Name your VM, select the folder location, and attach the ISO file.
    
    ![image.png](attachment:ed51cd5d-d8b1-4bda-bd3c-00d4b2788cce:image.png)
    
6. Assign resources based on your computer’s capacity. Recommended minimums:
- **Memory (RAM):** 2 GB (2048 MB)
- **Processors:** 1 CPU
- **Virtual Hard Disk:** 50 GB.
    
    ![image.png](attachment:6b84dc57-2f0c-4a26-903b-7567d7383162:image.png)
    
    ![image.png](attachment:cd274ed7-e9ad-45f5-88fe-ba71d84fda7b:image.png)
    
1. Complete the setup and click **“Start”** to launch your Windows VM.

💡 When asked for a product key, choose **“I don’t have a product key.”** You’ll still be able to complete the installation.

### 2.2 Downloading and Installing Kali Linux

Next, we’ll add Kali Linux to our lab.

1. Go to the [Kali Linux download page](https://www.kali.org/get-kali/).
2. Under **Virtual Machines**, select the **VirtualBox image**. (This option makes setup much faster.)
    
    ![image.png](attachment:b85f91c1-ea87-4e3a-9cae-06f2a01ef38a:image.png)
    
    ![image.png](attachment:28b0e213-648e-4655-8952-8a086bd1ade1:image.png)
    
3. Install [7-Zip](https://www.7-zip.org/download.html) to extract the compressed folder.
    
    ![image.png](attachment:ffc75f6c-d8ba-459f-8429-0b2d61a9dc25:image.png)
    
4. Right-click the downloaded Kali file → **7-Zip → Extract to…**
    
    ![image.png](attachment:b12fed4b-7822-4e62-b311-e90c4daeb70f:image.png)
    
    ![image.png](attachment:382ef365-7b4b-4585-ba03-c32fcd2fd978:image.png)
    
5. Open the extracted folder and double-click the file ending in **“.vbox.”**
    - This automatically imports Kali into VirtualBox.
        
        ![image.png](attachment:796d1256-9926-4bb0-ba84-a7899ce7fba8:image.png)
        
        ![image.png](attachment:d9215dcb-8107-4634-9762-30672dc390f8:image.png)
        
        ![image.png](attachment:97c70dd2-5e7a-4780-9006-52f7fe39767e:image.png)
        
6. Start the Kali VM.

🔑 Default login:

- **Username:** `kali`
- **Password:** `kali`
