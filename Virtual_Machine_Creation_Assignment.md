__NAME__: Phone Myat Minn Thu (Brandon)

__EMAIL__: phonemyat.minnthu@student.hamk.fi

__DATE__: 21 JAN 2026

# Week 1 - Creating Virtual Machine(Linux Ubuntu) on Azure

This is the markdown assignment for creating VM with Microsoft Azure.

## Step 1 - Creating Azure Account

The first step for us was to create an account in Microsoft Azure. We needed to sign up with our school's email, so that we can activate __Azure for Students__. We then activated the free credits with our student's account.

## Step 2 - Creating Resource Group & VM
### Step 2.1 - Creating Resource Group
Before we created the VM, first we had to make a resource group. 

Name of the resource group: **Robotics-students**

Subscription of the resource group: **Azure for students**

Location of the resource group: **North Europe**

### Step 2.2 - Creating VM

I faced multiple challenges while creating the VM as I was using Macbook. I'll explain each step I took down below.

We had to go to create Virtual Machine tab to create a VM. In the basics tab, I chose __Azure for Students__ for **Subscription** and __Robotics-students__ for **Resource group**. Then the next step is to name the VM, choose the region, and select availability.

__Virtual machine name__: brandon-ubuntu-vm-robotics

__Region__: (Europe) North Europe

__Availability options__: No infrastructure redundancy required

Next, we had to choose Image, VM architecture, and Size. This is where I started facing problems. In the image, I first chose ARM64 version and the all of the sizes were not compatible with the ARM64 architecture. So I chose x64 and the most popular size, which was 

__Size__: **standard B2ls v2 (2 vcpus, 4 GiB memory)**.

For __Authentication type__ I chose **SSH public key** and for __Username__ I chose **azureuser**. I name the __Key pair name__ the same as my VM name. I downloaded the .pem file for the key and followed the required steps.
## Pictures

![alt text](<Screenshots/Screenshot 2026-01-16 at 1.47.17 PM.png>)

![](<Screenshots/Screenshot 2026-01-16 at 1.47.19 PM.png>)

![alt text](<Screenshots/Screenshot 2026-01-16 at 1.47.26 PM.png>)

![alt text](<Screenshots/Screenshot 2026-01-16 at 1.51.50 PM.png>)

![alt text](<Screenshots/Screenshot 2026-01-16 at 1.55.35 PM.png>)

![alt text](<Screenshots/Screenshot 2026-01-16 at 1.56.26 PM.png>)

![alt text](<Screenshots/Screenshot 2026-01-16 at 1.56.30 PM.png>)

![alt text](<Screenshots/Screenshot 2026-01-16 at 2.34.11 PM.png>)

## Errors and challenges

After following the necessary steps, in the review page, most of us couldn't create the VM, so we had to choose locations one by one until it worked. Another problem I faced was, I couldn't open powershell on MacOS. So I had to use nested virtual machine. I first opened Windows Virtual Machine with VMWare, and logged in on Azure, and emailed myself the .pem file and followed the necessary steps. After that, I could use the Azure Linux VM.



