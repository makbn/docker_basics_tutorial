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

day 0, you're alone, no virtual machines , no hypervisor hole damn resources is yours!each application run on a dedicated server with a host OS.

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

    ​

### Hypervisor-based Virtualization

i believe that God sent **hypervisors** to save our lives!The hypervisor or virtual machine manager (VMM) **is generally a program or a combination of software and hardware that allows the abstraction of the underlying physical hardware**.

there are two major types of hypervisor :

- **Type I hypervisors** (native virtual machine) run directly on top of the hardware
  - Therefore, they take the place of the operating systems and interact directly with the ISA interface exposed by the underlying hardware, and they emulate this interface in order to allow the management of guest operating systems


- **Type II hypervisors** (hosted virtual machines) require the support of an operating system to provide virtualization services
  - This means that they are programs managed by the operating system, which interact with it through the ABI and emulate the ISA of virtual hardware for guest operating systems 

Moreover, virtualization technologies provide a virtual environment for not only executing applications but also for storage, memory, and networking

- **benefits**:

  - pay as need 

  - cost efficient 

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

  - security(opens the door to a new and unexpected form of phishing)

    ​

### container-based Virtualization

Container virtualization (often referred as operating system virtualization) is more than just a different kind of hypervisor. Containers use the **host operating system **as their base, and **not** the hypervisor. Rather than virtualizing the hardware (which requires full virtualized operating system images for each guest), containers virtualize the OS itself, **sharing the host OS kernel** and its resources with both the host and other containers.



———————|——————|——————|——————

|Container #1 |Container #2|Container #3|Container #4|         

|         App        |         App       |        App        |         App        |

|    Bins/Libs    |    Bins/Libs   |    Bins/Libs   |    Bins/Libs    |     

———————|——————|——————|——————

|                                   Container Engine                                   |

———————-——————-——————---——————

|                                               OS                                                 |       

———————-——————-——————---——————



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

  ​

- **disadvantage**:

  - **Containers don't run at bare-metal speeds**. Containers consume resources more efficiently than virtual machines. But containers are still subject to performance overhead due to overlay networking, interfacing between containers and the host system and so on. If you want 100 percent bare-metal performance, you need to use bare metal, not containers.
  - **Persistent data storage is complicated**. By design, all of the data inside a container disappears forever when the container shuts down, unless you save it somewhere else first. There are ways to save data persistently in Docker, such as Docker Data Volumes, but this is arguably a challenge that still has yet to be addressed in a seamless way.
  - **Graphical applications don't work well**. Docker was designed as a solution for deploying server applications that don't require a graphical interface. While there are some creative strategies (such as X11 video forwarding) that you can use to run a GUI app inside a container, these solutions are clunky at best.
  - **Not all applications benefit from containers**. In general, only applications that are designed to run as a set of discreet microservices stand to gain the most from containers. Otherwise, Docker's only real benefit is that it can simplify application delivery by providing an easy packaging mechanism.
