# Running Nginx via Docker on Ubuntu

> [!NOTE]
> 
> Before anything else, follow along with [How to install Docker CE on Ubunutu](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-22-04) to properly install Docker CE on your Ubuntu VM. The rest of this guide assumes that you have Docker installed.

This guide will walk through the steps required to run Nginx via a Docker container on your VM.

First, double-check your machine settings and ensure that under the Network tab that you have enabled an adapter with a `Host-only Adapter` configured. This will allow us to visit our Nginx server from our Host OS later on.

![image](https://github.com/Saeris/cne-370/assets/3144549/09a70c6f-17a2-4c50-bdbf-2c15d964287e)

Then once you have your VM booted up, open your terminal app of choice and run the following command to create a new container with Nginx. 

```bash
ocker run --name test-nginx -d -p 8080:80 nginx
```

`--name` will enable us to name this new container something friendly, which we'll set to `test-nginx`

`-d` will detach the container, running it in the background, and `-p` followed by `8080:80` configures the container to bind port `8080` of the VM to port `80` of the container, which is how we'll expose access to the container to the Host OS.

Lastly, `nginx` as the final argument to `docker run` will instruct docker to run a container image with the same name, downloading it from the container registry if it does not already exist on the local machine.

We can then check whether we were successful by running `docker ps`, which will list currently running container procresses:

![image](https://github.com/Saeris/cne-370/assets/3144549/f4cad9bf-7c0f-4415-a20b-ab0e166311a5)

We can then verify we can access the Nginx server by opening the browser in the VM and navigating to `localhost:8080`, which should load the default Nginx welcome page:

![image](https://github.com/Saeris/cne-370/assets/3144549/574b1399-9455-485d-b6c5-4b8cc3ad0b2a)

Finally, we'll want to check that we can access this page from our Host OS. To do this, first we'll need to get the IP address of our Host-Only adapter. We can do that with `ifconfig` or `hostname -I`. You may have multiple network adapters, so you will want to look for the IP address with the same subnet that your host machine is on. In this case it is `192.168.56.102`.

![image](https://github.com/Saeris/cne-370/assets/3144549/1603cbfc-b7b2-4221-9dae-864a2312c7d1)

With that IP address, we can now open a browser on our Host OS and navigate to our server:

![image](https://github.com/Saeris/cne-370/assets/3144549/6b8baf1e-f064-4081-97f0-928f57c35f5b)

To stop your container, you can run `docker stop test-nginx`, and to start it again, you can use `docker start test-nginx`. Use `docker --help` to get more information on other useful commands.
