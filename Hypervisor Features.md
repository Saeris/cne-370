# Cloning VMs

Virtual Machines (VMs) can be cloned in VirtualBox, which is convenient because it enables you to skip the OS installation and configuration process when you simply want to re-use a particular OS/configuration.

## Clone Virtual Machine Wizard

To clone a VM, you can open the clone wizard in one of three ways:

  1. By right-clicking on a VM in the list on the main window and selecting `Clone...` from the list of options.
     
     ![image](https://github.com/Saeris/cne-370/assets/3144549/c43e6462-7645-468d-9619-9fb7edcd71f9)

  3. By selecting a VM in the list on the main window and going to the `Machine` menu at the top of the window and selecting `Clone...` from the list of options.

     ![image](https://github.com/Saeris/cne-370/assets/3144549/2f1e6ae9-6836-497d-b996-1e1aa1763ca5)

  5. By selecting a VM in the list on the main window and pressing `ctrl + O`.  

This will bring up the clone wizard. On the first step, you will be prompted to enter a new name for the cloned VM and to select a location to save it to. You can also configure a MAC Address Policy, which is important when running clones at the same time as one another, as well as whether to keep the original disk names and Hardware UUIDs.

![image](https://github.com/Saeris/cne-370/assets/3144549/5cbf50a1-8b32-4a72-9f7a-da6ce5a78d55)

The second screen will ask whether you want a full clone or a linked clone. Unless you specifically need a linked clone and know what you are doing, full clones are easier to work with at the expense of additional disk space required.

![image](https://github.com/Saeris/cne-370/assets/3144549/50715999-9a08-407c-8aa2-a6e647e08f6b)

# Importing and Exporting VMs

VMs can also be exported to a file format that is portable between different computers and other virtual machine software.

## Exporting an Appliance in OVF Format

Exporting can be started one of two ways:

  1. By right-clicking on the VM in the list on the main window and selecting `Export to OCI...` from the list of options.

     ![image](https://github.com/Saeris/cne-370/assets/3144549/91b451bb-44c0-4591-8ab0-b8a2645f4bd8)

  3. By selecting the VM in the list on the main window and going to the `Machine` menu at the top of the window and selecting `Export to OCI...` from the list of options.

     ![image](https://github.com/Saeris/cne-370/assets/3144549/61dcc700-8f62-4482-a665-ecc894da5ae4)

This will bring up the Export Virtual Appliance wizard

![image](https://github.com/Saeris/cne-370/assets/3144549/4f6f7681-14f9-4b7b-9547-68416e8a6d9e)

![image](https://github.com/Saeris/cne-370/assets/3144549/4551bab8-2f78-4bc6-a39e-cb9b51e19022)

## Importing an Appliance in OVF Format

![image](https://github.com/Saeris/cne-370/assets/3144549/7b2b355e-d66b-4a27-bd55-123a6f58c7e1)

![image](https://github.com/Saeris/cne-370/assets/3144549/d0cff5c7-dc6e-440c-af1d-501fa7803d58)

![image](https://github.com/Saeris/cne-370/assets/3144549/9a50f4d7-fccf-425a-b609-c84ea99d06a8)

# Snapshots

## Take

![image](https://github.com/Saeris/cne-370/assets/3144549/6e029f52-829e-44e5-bcc5-e71b15647d5d)

## Restore

![image](https://github.com/Saeris/cne-370/assets/3144549/d69909ac-19bd-4851-bd38-13839e43706d)

![image](https://github.com/Saeris/cne-370/assets/3144549/4bdb2e98-b8dc-4fb1-b446-c76bea830240)

## Delete

![image](https://github.com/Saeris/cne-370/assets/3144549/e89d2322-9981-4995-af13-0756329dbaef)

# Clipboards

## Copying and Pasting from Host OS to Guest OS