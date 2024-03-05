# Creating a Simple Load Balancer in VirtualBox

This guide will walk you through the steps necessary to build out a simple load balancer in VirtualBox using Ubuntu. We'll start by creating a new Ubuntu VM (which you can read how to do [here](./README.md)), on which we'll install [nginx](https://www.nginx.com/) and other necessary CLI tools. Then we'll create two clones of this VM which we'll use as our webservers to distribute traffic to. Finally we'll configure our original VM to be the load balancer and test it using our two webservers.

If you have an existing Ubuntu VM, just clone it to skip the initial OS installation. Name your VM `Load Balancer` so that we can easily distinguish it from other VMs later.

> [!NOTE]
> This guide uses Ubuntu 22.04, CLI commands and configuration paths may vary if you are using a different distribution of Linux or a different version of Ubuntu.
>
> It also assumes your user is configured to have `sudo` permissions and has installed the VirtualBox Guest Additions to facilitate clipboard access between the host and the VM.

> [!TIP]
>
> If you are uncomfortable with using a terminal text editor such as `vim` or `nano`, consider installing Visual Studio Code on your Ubuntu VM.
>
> VSCode has it's own built-in terminal where you can run your typical linux commands, which you can open by pressing `` CTRL + Shift + ` `` or using the Terminal -> New Terminal menu at the top of the application window.
>
> You can install VSCode from either the Ubuntu Software app, or via the terminal using `sudo snap install code`
>
> Once installed, you can open and edit any file or folder with the `code` CLI command, such as `code /var/www/html/index.nginx-debian.html`

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

At this point we can shut down the VM and create two clones of it. We'll name these clones `Server01` and `Server02`. Make sure to select `Generate new MAC addresses for all network adapters` from the MAC Address Policy setting when cloning!

![image](https://github.com/Saeris/cne-370/assets/3144549/4cf777e0-b0c2-4755-86c1-33511119a454)

Next, we also need to configure our Load Balancer VM to be accessible by the Host OS. To do this, we'll open its settings and add a second adapter under the Network tab, choosing `Host-only Adapter` from the attach list, pictured below:

![image](https://github.com/Saeris/cne-370/assets/3144549/e5270652-d79a-4dc2-9183-5c259a755272)

Now, start all three VMs we've created as they will all need to be running at the same time for everything to work.

## Configuring Nginx on each VM

### Configure the Webservers

First we'll update our two web servers. In each we will want to do the following:

1. Open the default HTML file that Nginx serves so that we can make some changes to it. You can use the editor of your choice to modify `/var/www/html/index.nginx-debian.html`, or if you have VSCode installed, you can run the following command top open it:
 
   ```bash
   code /var/www/html/index.nginx-debian.html
   ```
2. Next we'll want to replace the body of the page with something that will uniquely identify each server. You can replace all of the code in this file with the following (using either `Server 1` or `Server 2` in the `<h1>` tag as appropriate):

    ```html
    <!DOCTYPE html>
    <html>
      <body>
        <h1>Server 1</h1>
      </body>
    </html>
    ```
3. Save this file. If you are using VSCode, you may get an error with a button that says `Retry as Sudo...` which you should click and then will be prompted for your password. If you are using a different text ediitor, it too will likely need to be run with `sudo` privilages.
4. Finally we need to take note of the IP address for this server, so run `hostname -I` to print it to the console.

### Configure the Load Balancer

With these steps completed on both servers, we'll need to go back to our Load Balancer VM and make some final changes there.

1. Open the Nginx configuration file which can be found at `/etc/nginx/sites-enabled/default`. If you have VSCode, you can instead open it with this command in your terminal:

   ```bash
   code /etc/nginx/sites-enabled/default
   ```
2. We're then going to replace the contents of this file with the following (replacing `SERVER_IP_1` and `SERVER_IP_2` with the console output from step 4 above):

   ```
   upstream web_backend {
   	 server SERVER_IP_1;
   	 server SERVER_IP_2;
   }
   
   server {
   	 listen 80;
   	 location / {
   	   proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
   	   proxy_pass http://web_backend;
     }
   }
   ```
3. Save this file. Like before, we will need `sudo` privilages to make changes to it.
4. Then, we need to restart Nginx to have it use our modified config. We can do that with the following command:

   ```bash
   sudo nginx -s reload
   ```
5. Finally, let's test whether everything works by opening our browser on this machine and navigating to `localhost`, or by running this command in our terminal:

   ```bash
   curl localhost
   ```

   Each time we refresh the page or run this command, we should get a different response, as our request is forwarded to one of our two web servers.

Assuming you didn't run into any unexpected errors along the way, you should now have a minimal working load balancer! Below is a screenshot of the result in action:

![image](https://github.com/Saeris/cne-370/assets/3144549/4005a3ba-1ecf-4597-985b-bd67c59d476f)


