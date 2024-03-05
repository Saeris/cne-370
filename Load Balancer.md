# Creating a Simple Load Balancer in VirtualBox

This guide will walk you through the steps necessary to build out a simple load balancer in VirtualBox using Ubuntu. We'll start by creating a new Ubuntu VM (which you can read how to do [here](./README.md)), on which we'll install [nginx](https://www.nginx.com/) and other necessary CLI tools. Then we'll create two clones of this VM which we'll use as our webservers to distribute traffic to. Finally we'll configure our original VM to be the load balancer and test it using our two webservers.

If you have an existing Ubuntu VM, just clone it to skip the initial OS installation. Name your VM `Load Balancer` so that we can easily distinguish it from other VMs later.

> [!NOTE]
> This guide uses Ubuntu 22.04, CLI commands and configuration paths may vary if you are using a different distribution of Linux or a different version of Ubuntu.
>
> It also assumes your user is configured to have `sudo` permissions and has installed the VirtualBox Guest Additions to facilitate clipboard access between the host and the VM.

## Required VM machine settings

Before starting your VM, first open the Network Manager tool, which can be found on the main window under the File -> Tools menu. Here we're going to create a new Host-only Network by clicking the Create button at the top of the screen. Then with the new network selected from the list, make sure that `Enable DHCP` is checked in the bottom portion of the screen. You can name this network however you like.

![image](https://github.com/Saeris/cne-370/assets/3144549/6d2b21be-83a6-4288-8a19-7c648484ee27)

Then we will need to config our VM's settings and go to the Network tab. Here you'll want to make sure Adapter 1 is attached to `NAT network` from the list of options. In the name field below that, select the network we just created.

![image](https://github.com/Saeris/cne-370/assets/3144549/199e53a3-a60f-4b5c-b421-66468f2fd92d)

## Setting up Nginx on Ubuntu

Open the Terminal app and run the following to install Nginx

```bash
sudo apt install nginx
```

Once this command completes, Nginx will be installed and will be running as a background process. You can test that it is working a few ways:

1. By running `nginx -v` to print the version to your console.
2. By running `curl localhost` which should print the default HTML file contents to your console.
3. By opening your browser and navigating to `localhost` which should render the default HTML file.

At this point we can shut down the VM and create two clones of it. We'll name these clones `Server01` and `Server02`.

Now, start all three VMs we've created as they will all need to be running at the same time for everything to work.

## Configuring Nginx on each VM
