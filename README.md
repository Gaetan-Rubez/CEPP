# How to get myQLM for the Fast-Start ?

## Before coming to the Fast-Start

In order to do the exercises of the hands-on session, you need a laptop.
The software for the exercises together with all the necessary dependencies
will run inside a "docker container" prepared in this purpose. 

The first step is to install the Docker Engine on your machine (you need administrator privileges on your system).
Instructions on how to install it can be found here:

for Ubuntu:
```bash
https://docs.docker.com/install/linux/docker-ce/ubuntu/
```

for CentOS:
```bash
https://docs.docker.com/install/linux/docker-ce/centos/
```

for Fedora:
```bash
https://docs.docker.com/install/linux/docker-ce/fedora/
```

for Debian:
```bash
https://docs.docker.com/install/linux/docker-ce/debian/
```

for Mac
```bash
https://docs.docker.com/docker-for-mac/
```

for Windows:
```bash
https://docs.docker.com/docker-for-windows/
```

The Docker ID could be useful for your if later on you want to create
your own docker images and upload them on the docker hub in order to make
them available to a large audience (they are public).

## Using the myQLM simulator from Atos Quantum Lab

Below are the instructions on how to download and use the myQLM docker image
for the workshop.

The image once installed is around 2.5GB; its export file is about 950MB.
 
1 – Retrieve the image
(equivalent of docker pull if our image was published on docker.io)

```bash
~> sftp myqlm@doorway.bull.com

myqlm@doorway.bull.com's password: ...see mail...

Connected to doorway.bull.com.

sftp> cd downloads

sftp> get myqlm-runtime-faststart-0.0.6.1_latest.export

Fetching…

sftp> bye
```

Note: This can be done from any machines connected to Internet.
 
2 – Import the image into your docker installation

```bash
~> zcat myqlm-runtime-0.0.6.1_latest.export | docker import - myqlm-runtime-0.0.6.1:latest
```

Note: One can use “docker images” to see the list of images
 
3 – Instantiate a container from the image and connect to it

```bash
~> [sudo] docker run -ti -p 8011:8888 myqlm-runtime-0.0.6.1:latest /bin/bash -l
```

Notes:

8011 here is an arbitrary port on the host side that will be mapped to the port 8888 inside the container (Jupyter server default port).

From another window, one can use “docker ps” to see the container.
       
The myQLM wheels are already installed except for myqlm-simulators and are located at /var/myqlm/dist/0.0.5/atos/myqlm-0.0.5-atos/
       
There is a README file that explains how to install myQLM at /var/myqlm/dist/0.0.5/atos/README.md
 
4 – Start a Jupyter server once inside the container
 
```bash
~> su – qatuser
~> cd qat-tutorial-0.0.6
~> jupyter-notebook --no-browser --ip="0.0.0.0"
…
```

Note: You can also work in command line mode

5 – Connect to the server from a browser

```bash
http://<localhost_or_host_ip>:8011
```

Note: Copy/paste the value of the token shown on the Jupyter console above

