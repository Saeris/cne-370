# Virtual Machine Setup Guide

This guide will walk you through the setup and configuration of virtual machines using VirtualBox.

## Before you start

First you will need to download VirtualBox, which you can find here: https://www.virtualbox.org/wiki/Downloads

Then, for this tutorial you will also need to download Lubuntu. We will be using a spcific version, 18.04.5 LTS Alternate 64-bit, which you can find on this page in the Alternate install image section: https://cdimages.ubuntu.com/lubuntu/releases/bionic/release/

## Install VirtualBox

Run the VirtualBox installer. You may be asked to confirm that installation will reset your network connections and download additional dependencies for your host operating system. Please refer to the user manual if you need additional help: https://www.virtualbox.org/manual/UserManual.html#installation

Once VirtualBox finishes installing, launch the program.

## Install Lubuntu

When you first run VirtualBox, you should see a screen similar to this:

![image](https://github.com/Saeris/cne-370/assets/3144549/cf91dc1b-5d87-4736-8338-2bd9d5609042)

Clicking the blue "New" button will open a dialog pictured below:

![image](https://github.com/Saeris/cne-370/assets/3144549/25b300c1-50a4-414b-921f-b74afea0ebad)

Fill out the Name field with whatever you would like the name this new VM. "Lubuntu" is fine for now but you may want to be more descriptive if you plan to have multiple VMs running the same OS in the future.

Using the ISO Image dropdown, select "Other..." from the list, which will open another dialog to search for a file on your PC. Navigate to and select the Lubuntu ISO file you downloaded previously.

With both of these fields configured you can proceed to the next step.

![image](https://github.com/Saeris/cne-370/assets/3144549/6ef4d7cf-5c33-41e0-b664-4aad2c2b3c12)

Here you will be able to customize the admin account details and the VM's network options. You can leave these at their default values as shown above and proceed to the next screen.

![image](https://github.com/Saeris/cne-370/assets/3144549/78665c20-5562-4af7-9cdc-b288c186ce86)

Here you can customize the CPU and memory resources available to the VM. The default values may vary depending on your host PC's capabilities. You can leave these at their default values as well and proceed to the next step.

![image](https://github.com/Saeris/cne-370/assets/3144549/ece2e290-f34a-455c-880c-16b25431cf34)

On this screen you can configure the vitual hard drive that will be used by this VM, or choose an existing one. You can lower the default value to something smaller, such as 3 GB. A special property of virtual hard disks in a program such as Virtualbox is that they can be resized as needed, so setting this to a smaller value at first is fine. Setting it too low may prevent the VM from being able to install however, so a few GB is generally a good number. If you select "Pre-allocate Full Size", the newly created disk file will take up the entire size you configure here. You can leave this unchecked and proceed to the next step.

![image](https://github.com/Saeris/cne-370/assets/3144549/eddea1a2-92ed-4734-b02c-c08f54b2881b)

Finally you will be shown a summary of the settings you configured. Click "Finish", after which VirtualBox will automatically start the new VM and proceed with the initial OS installation process for you.

## OS Installation

VirtualBox will automatically install the OS when following the steps outlined above. However, you may run into an error screen during installation. 
