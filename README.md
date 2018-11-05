# Kick-Start

### What is Docker?

- Docker by [Docker Official Website](https://www.docker.com/what-docker) :

  > Docker is the company driving the container movement and the only container **platform provider to address every application across the hybrid cloud.** Today’s businesses are under pressure to digitally transform but are constrained by existing applications and infrastructure while rationalizing an increasingly diverse portfolio of clouds, datacenters and application architectures. Docker enables true independence between applications and infrastructure and developers and IT ops to unlock their potential and creates a model for better collaboration and innovation.


- Docker by [Wikipedia]()

  > an open-source project that automates the deployment of software applications inside **containers**by providing an additional layer of abstraction and automation of **OS-level virtualization** on Linux.

- In summary:

  docker is an open-source project that use **OS-level virtualization technology** to provide an **isolated context** called **container** to **run application without overheads of virtual machines technology** that used tereditionally!

in few next paragraphs we will talk about virtualization technology!you can jump to Docker Hello World if you are not intrest!



# Virtualization history

Virtualization is a broad concept that refers to the creation of a virtual version of something, whether hardware, a software environment, storage, or a network.

In a virtualized environment there are three major components:

- **Guest**: represents the system component that interacts with the virtualization layer rather than with the host, as would normally happen
- **Host**: represents the original environment where the guest is supposed to be managed
- **Virtualization layer**: is responsible for recreating the same or a different environment where the guest will operate

### Pre-Virtualization World

Day 0, you're alone, no virtual machines , no hypervisor oh God whole damn resources are yours!each application run on a dedicated server with a goddamn super-fast host OS. but does God really forget us?

- **benefits**:

  - no overhead!
  - security
  - full and total access to its resources
  - performs an extremely high volume of read and/or write actions to the hard disk 

- **disadvantage**:

  - waste of money

  - waste of energy

  - waste of resource

  - no elasticity

  - no scalability

  - slow deploy

  - hard to migrate


### Hypervisor-based Virtualization

i believe that God sent **hypervisors** to save our money!The hypervisor or virtual machine manager (VMM) **is generally a program or a combination of software and hardware that allows the abstraction of the underlying physical hardware**.

there are two major types of hypervisor :

- **Type I hypervisors** (native virtual machine) run directly on top of the hardware
  - Therefore, they take the place of the operating systems and interact directly with the ISA interface exposed by the underlying hardware, and they emulate this interface in order to allow the management of guest operating systems


- **Type II hypervisors** (hosted virtual machines) require the support of an operating system to provide virtualization services
  - This means that they are programs managed by the operating system, which interact with it through the ABI and emulate the ISA of virtual hardware for guest operating systems 

Moreover, virtualization technologies provide a virtual environment for not only executing applications but also for storage, memory, and networking

- **benefits**:

  - pay as need 

  - cost efficient or sth like that

  - security(isolated context for deploying applications)

  - energy efficient

  - migration

  - easy to scale

    ​

- **disadvantage**:

  - long boot time

  - hard to migrate

  - overhead

  - slow deploy
  
  - not so frugel

  - security(opens the door to a new and unexpected form of phishing)

### container-based Virtualization

Container virtualization (often referred as operating system virtualization) is more than just a different kind of hypervisor. Containers use the **host operating system **as their base, and **not** the hypervisor. Rather than virtualizing the hardware (which requires full virtualized operating system images for each guest), containers virtualize the OS itself, **sharing the host OS kernel** and its resources with both the host and other containers.

![container](https://www.docker.com/sites/default/files/Container%402x.png)

- **benefits**:

  - pay as you need
  - elasticity
  - scalibility
  - fast deployment
  - easy to migrate
  - less overhead
  - fast boot 
  - energy efficient
  - consistent environment
  - layered filesystem
  - easy CI/CD
  - easy versioning 
  - super easy configuration

- **disadvantage**:

  - **Containers don't run at bare-metal speeds**. Containers consume resources more efficiently than virtual machines. But containers are still subject to performance overhead due to overlay networking, interfacing between containers and the host system and so on. If you want 100 percent bare-metal performance, you need to use bare metal, not containers.
  - **Persistent data storage is complicated**. By design, all of the data inside a container disappears forever when the container shuts down, unless you save it somewhere else first. There are ways to save data persistently in Docker, such as Docker Data Volumes, but this is arguably a challenge that still has yet to be addressed in a seamless way.
  - **Graphical applications don't work well**. Docker was designed as a solution for deploying server applications that don't require a graphical interface. While there are some creative strategies (such as X11 video forwarding) that you can use to run a GUI app inside a container, these solutions are clunky at best.
  - **Not all applications benefit from containers**. In general, only applications that are designed to run as a set of discreet microservices stand to gain the most from containers. Otherwise, Docker's only real benefit is that it can simplify application delivery by providing an easy packaging mechanism. honestly i mean micro-services!
  
  ![VM Vs. Container](https://blog.netapp.com/wp-content/uploads/2016/03/Screen-Shot-2018-03-20-at-9.24.09-AM-1024x548.png)
  

## Docker Performance and architecture

### Architecture

Docker uses a **client-server** architecture. The **Docker *client*** talks to the **Docker *daemon***, which does the heavy lifting of building, running, and distributing your Docker containers. The Docker client and daemon *can* run on the same system, or you can connect a Docker client to a remote Docker daemon. The Docker client and daemon communicate using a REST API, over UNIX sockets or a network interface.

![Docker Achitecture](https://hahoangv.files.wordpress.com/2016/08/docker_6.png?w=816&h=9999)

### Docker on Linux

On Linux systems, Docker directly leverages the kernel of the host system, and file system mounts are native. (home sweet home)

### Docker on WIndows

>  In Docker for Windows does each container run in separate VM?



> There are two types of Windows containers... Windows Containers & Hyper-V Containers. Windows Containers work the same way you know Linux based containers work... one or more in a host where the host can be a VM. Hyper-V containers are different though in that they run a single container within a tiny Hyper-V VM.
>
> We (not me) interviewed the guy who owns the Windows Container story for Microsoft recently on our podcast if you're interested in learning not only more about this, but where they are going & helping. I found it fascinating how much an old engineering team like Windows is contributing to an open source project!
>
> [http://www.microsoftcloudshow.com/podcast/Episodes/137-windows-containers-are-coming-talking-to-taylor-brown-about-the-container-wave-coming-to-the-microsoft-world480](http://www.microsoftcloudshow.com/podcast/Episodes/137-windows-containers-are-coming-talking-to-taylor-brown-about-the-container-wave-coming-to-the-microsoft-world)



### Docker on Mac

In June 2016 Docker announced **Docker for Mac**. The “new” way to run Docker on Mac with much easier installation and a more Linux-y experience for Docker users. **Docker for Mac** still starts a virtual machine (**even though it is super hidden**). It also brought its own hypervisor **hyperkit** and shared file system **osxfs**. Unfortunately, “osxfs” wasn’t very fast, and from the beginning there have been long discussions about it ([Docker](https://forums.docker.com/t/file-access-in-mounted-volumes-extremely-slow-cpu-bound/8076/23), [Github](https://github.com/docker/for-mac/issues/77)).

Docker has [steadily been working](https://docs.docker.com/docker-for-mac/osxfs/#performance-issues-solutions-and-roadmap) on performance improvements for **Docker for Mac** and [released improvements](https://docs.docker.com/docker-for-mac/osxfs-caching/) with 17.04 CE. 17.04 CE now brings new performance flags to mountpoints of **Docker Volumes (“**delegated” and “cached”**)**. Docker [talks about an 2x — 3.5x improvement](https://docs.docker.com/docker-for-mac/osxfs/#technology) when comparing **Docker for Mac** 17.04 CE vs older versions. I mean don't use docker for mac as a production level environment.

Mountpoint flags:
* `consistent`: perfect consistency (host and container have an identical view of the mount at all times)

* `cached`: the host’s view is authoritative (permit delays before updates on the host appear in the container)

* `delegated`: the container’s view is authoritative (permit delays before updates on the container appear in the host)





# Hello World

now we'll run our first docker image and create a new container:

```bash
docker run hello-world
```

and the result is:

```bash
Unable to find image 'hello-world:latest' locally
docker: Error response from daemon: error parsing HTTP 403 response body: invalid character '<' looking for beginning of value: "<html><body><h1>403 Forbidden</h1>\nSince Docker is a US company, we must comply with US export control regulations. In an effort to comply with these, we now block all IP addresses that are located in Cuba, Iran, North Korea, Republic of Crimea, Sudan, and Syria. If you are not in one of these cities, countries, or regions and are blocked, please reach out to https://support.docker.com\n</body></html>\n\n".
See 'docker run --help'.
```

lets see what happend! read the first line of output,we have diffrent scenario when we run a docker image:

- scenario 1

  after you try tu run hello-world image, docker search for this image on your local machine,if its stored there from befor, new container create from image will be create and sart

- scenario 2

  but what if docker cant find image locally?**if you're not connected from Iran, North Korea, Republic of Crimea, Sudan, and Syria**, in this scenario docker should search on an online repository to find this image!this repositories called **Registery**! after finding image docker will pull this requested image to your local machine storage and start your image to create new **container**

  but if you're a citizen of banned regions probeblly you will see this error:

  ```bash
  docker: Error response from daemon: error parsing HTTP 403 response body: invalid character '<' looking for beginning of value: "<html><body><h1>403 Forbidden</h1>\nSince Docker is a US company, we must comply with US export control regulations. In an effort to comply with these, we now block all IP addresses that are located in Cuba, Iran, North Korea, Republic of Crimea, Sudan, and Syria. If you are not in one of these cities, countries, or regions and are blocked, please reach out to https://support.docker.com\n</body></html>\n\n".
  See 'docker run --help'.
  ```

  All you need is a VPN!

OK, lets try again:

```bash
makbns-MacBook-Pro:~ makbn$ docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
ca4f61b1923c: Pull complete 
Digest: sha256:445b2fe9afea8b4aa0b2f27fe49dd6ad130dfe7a8fd0832be5de99625dad47cd
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.


```

docker couldn't find image locally then tries to download it from registery!after download finished, image saved locally and stared by docker deamon!

- [Where are Docker images stored on the host machine](https://stackoverflow.com/questions/19234831/where-are-docker-images-stored-on-the-host-machine)?



### Docker objects

When you use Docker, you are creating and using images, containers, networks, volumes, plugins, and other objects. This section is a brief overview of some of those objects.

#### IMAGES

An *image* is a read-only template with instructions for creating a Docker container. Often, an image is *based on*another image, with some additional customization. For example, you may build an image which is based on the `ubuntu` image, but installs the Apache web server and your application, as well as the configuration details needed to make your application run.

You might create your own images or you might only use those created by others and published in a registry. To build your own image, you create a *Dockerfile* with a simple syntax for defining the steps needed to create the image and run it. Each instruction in a Dockerfile creates a layer in the image. When you change the Dockerfile and rebuild the image, only those layers which have changed are rebuilt. This is part of what makes images so lightweight, small, and fast, when compared to other virtualization technologies.

#### CONTAINERS

A container is a runnable instance of an image. You can create, start, stop, move, or delete a container using the Docker API or CLI. You can connect a container to one or more networks, attach storage to it, or even create a new image based on its current state.

By default, a container is relatively well isolated from other containers and its host machine. You can control how isolated a container’s network, storage, or other underlying subsystems are from other containers or from the host machine.

A container is defined by its image as well as any configuration options you provide to it when you create or start it. When a container is removed, any changes to its state that are not stored in persistent storage disappear.



# Docker Basic Commands

## `docker run`

Run a command in a new container

```
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```

### options

| Name, shorthand    | Default | Description                              |
| ------------------ | ------- | ---------------------------------------- |
| --env , -e         |         | Set environment variables                |
| --expose           |         | Expose a port or a range of ports        |
| --rm               |         | Automatically remove the container when it exits |
| --tty , -t         |         | Allocate a pseudo-TTY                    |
| --interactive , -i |         | Keep STDIN open even if not attached     |
| -d                 |         | run in detached mode all the time        |

### example

```ba
docker run -it --name ubuntu_cont ubuntu:latest bash
```

```ba
docker run -it busybox:latest echo "hello world"
```







## `docker start`

Start one or more stopped containers in detached mode

```
docker start [OPTIONS] CONTAINER [CONTAINER...]
```

### options

| Name, shorthand    | Default | Description              |
| ------------------ | ------- | ------------------------ |
| --interactive , -i |         | Attach container’s STDIN |

### example

```ba
docker start -i ca765vb
```







## `docker ps`

list of containers

```bas
docker ps [OPTIONS]
```

### options

| Name, shorthand | Default | Description         |
| --------------- | ------- | ------------------- |
| —all , -a       |         | show all containers |

### example

```bash
docker ps -a
```







## `docker images`

list of images

```bash
docker images [OPTIONS] [REPOSITORY[:TAG]]
```

### options

| Name, shorthand | Default | Description     |
| --------------- | ------- | --------------- |
| —all , -a       |         | show all images |

- docker image have intermediate layers that increase reusability, decrease disk usage and spped up `docker build` by allowing each step to be cached! these intermediat layer are not shoen by default.

### example

```bas
docker images -a
```





## `docker stop`

Stop one or more running container

```bash
docker stop [OPTIONS] CONTAINER [CONTAINER...]
```

### options

| Name, shorthand | Default | Description                              |
| --------------- | ------- | ---------------------------------------- |
| —time, -t       | 10      | seconds to wait for stop before killing it |

### example

```bas
docker stop -t 100 34tfer 
```





## `docker kill`

Kill one or more running containers

```ba
docker kill [OPTIONS] CONTAINER [CONTAINER...]
```

### options

| Name, shorthand | Default | Description                     |
| --------------- | ------- | ------------------------------- |
| --signal , -s   | KILL    | Signal to send to the container |

- stop vs. kill?

### example

```ba
docker kill cae40c
```







## `docker exec`

Run a command in a running container

```b
dockr exec [OPTIONS] CONTAINER [ARGS...]
```

### options

| Name, shorthand    | Default | Description                              |
| ------------------ | ------- | ---------------------------------------- |
| --detach , -d      |         | Detached mode: run command in the background |
| --interactive , -i |         | Keep STDIN open even if not attached     |
| --tty , -t         |         | Allocate a pseudo-TTY                    |

- COMMAND should be an executable, a chained or a quoted command will not work. Example:
  -  `docker exec -ti my_container "echo a && echo b"` will not work, but 
  - `docker exec -ti my_container sh -c "echo a && echo b"` will.

### example

```bas
docker exec -it 120 bash
```







# `docker cp`

Copy files/folders between a container and the local filesystem

```bash
docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH|-
docker cp [OPTIONS] SRC_PATH|- CONTAINER:DEST_PATH
```

### example

```ba
docker cp /file_from_host my_cnt:/dir_in_cnt/
```







# `docker rm`

Remove one or more containers

```bash
docker rm [OPTIONS] CONTAINER [CONTAINER...]
```

### options

| Name, shorthand | Default | Description                              |
| --------------- | ------- | ---------------------------------------- |
| --force , -f    |         | Force the removal of a running container (uses SIGKILL) |
| --link , -l     |         | Remove the specified link                |
| --volumes , -v  |         | Remove the volumes associated with the container |

### example

```ba
docker rm 34fg 6hfg 
```



# Lifecycle of Docker Container

![Lifecycle](https://cdn-images-1.medium.com/max/2000/1*vca4e-SjpzSL5H401p4LCg.png)



# How to create your own images

before starting to create our own image its good to know more about docker images structure:

- Images are read only templates used to create containers.
- Images are created with the `docker build` command, either by us or by other docker users.
- Images are composed of layers of other images.
- Images are stored in a Docker registry.

there are two ways to create new image, **change an existing image** and **create a Dockerfile**:

### `docker commit`

for create new image from an existing image you should create a container from source image and make your change on container and commit your change with `docker commit` to create new image!



```
docker commit [OPTIONS] CONTAINER [REPOSITORY[:TAG]]
```

| Name, shorthand | Default | Description                              |
| --------------- | ------- | ---------------------------------------- |
| --author , -a   |         | Author ( “Mehdi Akbarian Rastaghi [mehdi74akbarian@gmail.com](mailto:mehdi74akbarian@gmail.com)”) |
| --change , -c   |         | Apply Dockerfile instruction to the created image |
| --message , -m  |         | Commit message                           |
| --pause , -p    | true    | Pause container during commit            |

//TODO: dockerfile

### `docker build`

```
docker build [OPTIONS] PATH | URL | -
```

Docker can build images automatically by reading the instructions from a `Dockerfile`. A `Dockerfile` is a text document that contains all the commands a user could call on the command line to assemble an image. Using `docker build` users can create an automated build that executes several command-line instructions in succession.

Let us start with the the overall flow, which goes something like this:

1. You create a Dockerfile with the required instructions.
2. Then you will use the docker build command to create a Docker image based on the Dockerfile that you created in step 1.

now, open up the vi editor and create our first Dockerfile as shown below:

```
From ubuntu:latest

# run echo command (during build)
RUN echo 'we are running some # of cool things'

RUN echo 'we are running some # of cool things again'

MAINTAINER mehdi akbarian (mehdi74akbarian@gmail.com)
```

the **[FROM](https://docs.docker.com/reference/builder/#from)**command sets the base image for the rest of the instructions. 

the [**RUN**](https://docs.docker.com/reference/builder/#run) instruction is used to execute any commands 

the **MAINTAINER** command tells who is the author of the generated images.



Now, save the file and come back to the prompt.

```ba
docker build -t my_repo/ubuntu:dockerfile -f /Users/makbn/Desktop/dockerfile_dir/Dockerfile .
```

and the result is:

```ba
makbns-MacBook-Pro:dockerfile_dir makbn$ docker build -t my_repo/ubuntu:dockerfile -f /Users/makbn/Desktop/dockerfile_dir/Dockerfile .
Sending build context to Docker daemon  2.048kB
Step 1/4 : FROM ubuntu:latest
 ---> 747cb2d60bbe
Step 2/4 : RUN echo 'we are running some # of cool things'
 ---> Using cache
 ---> 613fbf091316
Step 3/4 : CMD ping localhost
 ---> Running in ee923ff849a4
 ---> f3bb5c7c36ed
Removing intermediate container ee923ff849a4
Step 4/4 : MAINTAINER mehdi akbarian (mehdi74akbarian@gmail.com)
 ---> Running in b1d91fd2dd9b
 ---> 915046d9576f
Removing intermediate container b1d91fd2dd9b
Successfully built 915046d9576f
Successfully tagged my_repo/ubuntu:dockerfile
```



- Each RUN command will execute the command on the top writable layerof the container, then commit the container as a new image.
- The new image is used for the next step in the Dockerfile. So each RUN instruction will create a new image layer.
- It is recommended to chain the RUN instructions in the Dockerfile to reduce the number of image layers it creates.

example:

```dockerfile
From ubuntu:latest

RUN apt-get update
RUN apt-get install -y git
RUN apt-get instal -y vim
```

result:

```b
makbns-MacBook-Pro:dockerfile_dir makbn$ docker build -t my_repo/ubuntu:dockerfile -f /Users/makbn/Desktop/dockerfile_dir/Dockerfile .
Sending build context to Docker daemon  2.048kB
Step 1/4 : FROM ubuntu:latest
 ---> 747cb2d60bbe
Step 2/4 : RUN apt-get update
 ---> Using cache
 ---> 6f046193d94a
Step 3/4 : RUN apt-get install -y git
 ---> Using cache
 ---> 0234fac19063
Step 4/4 : RUN apt-get install -y vim
 ---> Running in 063aa832c462
Reading package lists...
Building dependency tree...
Reading state information...
The following additional packages will be installed:
  file libgpm2 libmagic1 libmpdec2 libpython3.5 libpython3.5-minimal
  libpython3.5-stdlib mime-support vim-common vim-runtime
...
Processing triggers for libc-bin (2.23-0ubuntu9) ...
 ---> 1fa2877725e9
Removing intermediate container 063aa832c462
Successfully built 1fa2877725e9
Successfully tagged my_repo/ubuntu:dockerfile
```

- using cache?

this file takes 4 steps to build but with chaining the RUN instructions we can reduce the number of image layers:

```dockerfile
From ubuntu:latest

RUN apt-get update && apt-get install -y \ git \ vim
```

just 2 steps!



### CMD

The command CMD, similarly to RUN, can be used for executing a specific command. However, unlike RUN it is not executed during build, but when a container is instantiated using the image being built. Therefore, it should be considered as an initial, default command that gets executed (i.e. run) with the creation of containers based on the image.

**To clarify:** an example for CMD would be running an application upon creation of a container which is already installed using RUN (e.g. RUN apt-get install …) inside the image. This default application execution command that is set with CMD becomes the default and replaces any command which is passed during the creation.

```dockerfile
From ubuntu:latest

RUN apt-get update
RUN apt-get install -y git
RUN apt-get install -y vim

CMD ["echo", "hello world"]
```



### COPY and ADD

The `COPY` instruction copies new files or directories from `<src>` and adds them to the filesystem of the container at the path `<dest>`.

```ba
COPY <src>... <dest>
```

- ADD?

### EXPOSE

```
EXPOSE <port> [<port>/<protocol>...]
```

The `EXPOSE` instruction informs Docker that the container listens on the specified network ports at runtime. You can specify whether the port listens on TCP or UDP, and the default is TCP if the protocol is not specified.



### example

```dockerfile
FROM ubuntu
MAINTAINER Mehdi akbarian
RUN apt-get update
RUN apt-get install -y nginx
EXPOSE 80
```

The ENTRYPOINT is then running the nginx executable and we are using the EXPOSE command here to inform what port the container will be listening on.

- build & run

```b
docker run -it -p80:80 my_repo/ubuntu:nginx bash
```

```ba
/etc/init.d/nginx start
```

# Network

One of the reasons Docker containers and services are so powerful is that you can connect them together, or connect them to non-Docker workloads. Docker containers and services do not even need to be aware that they are deployed on Docker, or whether their peers are also Docker workloads or not. Whether your Docker hosts run Linux, Windows, or a mix of the two, you can use Docker to manage them in a platform-agnostic way.

### Network drivers
Docker’s networking subsystem is pluggable, using drivers. Several drivers exist by default, and provide core networking functionality:

* **bridge:** The default network driver. If you don’t specify a driver, this is the type of network you are creating. Bridge networks are usually used when your applications run in standalone containers that need to communicate. See bridge networks.

* **host:** For standalone containers, remove network isolation between the container and the Docker host, and use the host’s networking directly. host is only available for swarm services on Docker 17.06 and higher. See use the host network.

* **overlay:** Overlay networks connect multiple Docker daemons together and enable swarm services to communicate with each other. You can also use overlay networks to facilitate communication between a swarm service and a standalone container, or between two standalone containers on different Docker daemons. This strategy removes the need to do OS-level routing between these containers. See overlay networks.

* **none:** For this container, disable all networking. Usually used in conjunction with a custom network driver. none is not available for swarm services. See disable container networking.


### Docker Machine

Docker Machine is a tool that lets you install Docker Engine on virtual hosts, and manage the hosts with `docker-machine` commands. You can use Machine to create Docker hosts on your local Mac or Windows box, on your company network, in your data center, or on cloud providers like Azure, AWS, or Digital Ocean.

Using `docker-machine` commands, you can **start**, **inspect**, **stop**, and **restart** a managed host, upgrade the Docker client and daemon, and configure a Docker client to talk to your host.


# References

* https://docs.docker.com/
* https://www.udemy.com/docker-tutorial-for-devops-run-docker-containers/
* https://devopscube.com/what-is-docker/

# Presentation Link



![QR Code](https://api.qrserver.com/v1/create-qr-code/?color=000000&bgcolor=FFFFFF&data=https%3A%2F%2Fgithub.com%2Fmakbn%2Fdocker_basics_tutorial&qzone=1&margin=0&size=200x200&ecc=L)

Link : https://github.com/makbn/docker_basics_tutorial

