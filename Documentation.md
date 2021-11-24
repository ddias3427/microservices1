# Introduction

## Containers

Containers are an Operative System Virtualization technology that allows you to package (containerize!) applications and services, its dependencies and configurations in Isolated environments. This allows you to:

-  **Portability**: Standardize you environment across   different infrastructures allowing developers to deploy applications with little to no modification.
-  **Isolation**: Isolate applications from each other on a shared OS providing more security and avoiding dependency problems.
-  **Agility**: Have a much smaller footprint by making use of the Host OS resources, allowing also to start/stop much faster a service. 
-  **Scalability**: Allows you to increase the number of replicas running of a container.

Containers are created from container images that act like templates that hold all the required information for a container to run. Images are created in layers in which 1 image can be used to run multiple containers or also to create another more complex image that then can be used to run multiple containers. 

Containers doesn't care what you ship in it: It can be build in your laptop and be deployed on the cloud in the other side of the world, it is interchangeable, stackable, portable and as generic as possible.

![image-20210621090129570](images1/image-20210621090129570.png)

## Virtual Machines

Virtual machines are based on computer architectures and provide functionality of a physical computer. Their implementations may involve specialized hardware, software, or a combination. They provide a substitute for a real machine. They provide functionality needed to execute entire operating systems. A hypervisor uses native execution to share and manage hardware, allowing for multiple environments which are isolated from one another, yet exist on the same physical machine

![image-20210621085521523](images1/image-20210621085521523.png)

## Monolithic Architecture

Monolithic Architecture puts together complex applications that solve multiple problems and have multiple functions into a single environment, workspace and much larger code bases. 

**Advantages:**

-  It’s simple to develop as there is either no modularity or less formal modularity.
-  It’s easy to deploy as one single file is deployed.
-  There are less security concerns as software consists of single code base.
-  Because of the single code base, there is no network latency so application has better performance.
-  It’s easy to track bugs and do end-to-end testing because of single code base.

**Disadvantages:**

-  When a bug affects a single aspect of the code base, it impacts everything!!!.
-  Even if a small change is required, then whole application needs to be redeployed.
-  Thorough regression testing is required even if a small change is made.
-  You cannot scale the components, you have to scale the whole application.  
-  If you want to use a new technology you have to re-write the whole application.
-  As code base size increases, it becomes difficult to manage code and overall deployment time also increases.
-  If a new developer joins the project, it’s very difficult for him to understand the code and work-flows.

## Micro-services Architecture

In a Micro-services architecture you create smaller applications that are deployed independently as loosely coupled services, and tied together through application integration.  The business logic may encompass multiple platforms, including software and databases from multiple sources. From a developer perspective, micro-services are simpler to develop, smaller and faster to deploy. Which allows continuous integration and continuous delivery `CI/CD`. They can be written in any programming language and they can communicate with other micro-services  through `APIs`.

-  **Continuous Integration CI:** Is the process of automating the build and testing of code.
-  **Continuous Delivery CD:** Is the ability of automating the deployment process of an application.
-  **Application Programming Interface APIs:** Is a set of calls programmed to make use of a service or application.

## Architectures comparison

### A simplified example

![image-20210628095049568](images1/image-20210628095049568.png)

The above is the type of representation that you might be able to find all over the internet where we just indicate that in the Monolithic Architecture everything its interdepedant and connected and there is a `two-way` communication while in the Microservices Architecture everything is sort of loose and the communication comes and goes in different directions and across components.

### A more realistic example

Imagine you are developing the code for a web application used by a shoe store that requires:

-  Creating invoices
-  Maintaining inventory
-  Creating reports
-  Customer communications

#### Monolithic Architecture

In a monolithic architecture the infrastructure along with the application in an over simplified example that is using a single server might look something like this:

![image-20210628110446171](images1/image-20210628110446171.png)

#### Micro-service Architecture

The same application in a micro-service architecture will look something like this:

![image-20210628114009688](images1/image-20210628114009688.png)

Notice how all the dependencies on regards of the location, server, operative system, language, and database no longer exist and the re-utilization of services is wider and easier by communicating among services using APIs.

## Twelve-Factors of SaaS

The twelve-factor application is a methodology for building software-as-a-service applications that:

-  Use **declarative** formats for setup automation, to minimize time and cost for new developers joining the project;
-  Offering **maximum portability** between execution environments;
-  Are suitable for **deployment** on modern **cloud platforms**, obviating the need for servers and systems administration;
-  **Minimize divergence** between development and production, enabling **continuous deployment** for maximum agility;
-  And can **scale up** without significant changes to tooling, architecture, or development practices.

The twelve-factor methodology can be applied to applications written in any  programming language, and which use any combination of backing services.

1. **Code base**: One code base tracked in revision control, many deploys.
2. **Dependencies**: Explicitly declare and isolate dependencies.
3. **Config**: Store config in the environment.
4. **Backing services**: Treat backing services as attached resources.
5. **Build, release, run**: Strictly separate build and run stages.
6. **Processes**: Execute the app as one or more stateless processes.
7. **Port binding**: Export services via port binding.
8. **Concurrency**: Scale out via the process model.
9. **Disposability**: Maximize robustness with fast startup and graceful shutdown.
10. **Dev/prod parity**: Keep development, staging, and production as similar as possible.
11. **Logs**: Treat logs as event streams.
12. **Admin processes**: Run admin/management tasks as one-off processes.

# Introducing Containers

Containers make development efficient and predictable, take away repetitive, mundane configuration tasks and are used throughout the development life-cycle for fast, easy and portable application development.

It works by using an open-source engine that automates the deployment of applications into containers that can be either podman or docker among the most known ones.

## Advantages

### Isolation & Security

Using containers developers can create predictable environments that are isolated from other applications. Regardless of where the application is deployed, everything remains consistent and this leads to massive productivity:  less time debugging, and more time launching fresh features and  functionality for users.

From a security  point of view, containers ensure that applications that are running are completely segregated and isolated from each other,  granting you complete control over traffic flow and management. None of the container can look into processes running inside another container. From an architectural point of view, each container gets its own set of resources ranging from processing to network stacks.

### Resource Utilization

When each process is put into a container, it can be shared with new applications and by allowing containers to share basic kernel functions, much of the  unnecessary OS overhead is removed. This can allow for up to four times more server application instances in the space a Virtual Machine would need. 

Containers are also quicker compared to a virtual machines because do not need to launch an complete Operative System.

### Manageability & Portability

Container images are free of environmental limitations, and that makes any deployment consistent, portable, and scalable. Containers have the added benefit of running anywhere. This speeds up the development process.  

### Scalability 

You can dictate how many resources `CPU, network, memory, etc.`each  container can use. Plus, the containers can be resized to meet the needs of your application as it grows. This allows an application to scale better than those on virtual machines, which are difficult to resize.    

## Architecture

![image-20210628124942462](images1/image-20210628124942462.png)

| Component     | Description                                                  |
| ------------- | ------------------------------------------------------------ |
| **Engine**    | Daemon + Client are refer to as the Engine or Master.        |
| **Client**    | It's the Command Line Interface or Command Line Interface (C. L. I.) that controls the Daemon. |
| **Daemon**    | Service responsible from running containers. "The server".   |
| **Images**    | They initial state of a container. "Template" that formats how each container will look like. |
| **Registry**  | It's a repository of all the images. Can be public (Docker Hub) or private. |
| **Container** | It's a instance of an image that is **running**!.            |

The Engine is everything… Basically when you say Docker you are in reality referring to the engine that acts as a client-server application with:

-  A server with a long-running daemon process `dockerd`
-  APIs which specify interfaces that programs can use to talk to and instruct the Docker daemon.
-  A command line interface (CLI) client `docker`.

The CLI uses Docker APIs to control or interact with the Docker daemon through scripting or direct CLI commands. Many other Docker applications use the underlying API and CLI. The daemon creates and manage Docker objects, such as images, containers, networks, and volumes/storage.

![image-20210621092032939](images1/image-20210621092032939.png)

When you execute a command in the `Client` the `daemon` interprets the command and acts accordingly either by connecting to the `Registry` to `pull` a new `image` or to `build` another image or maybe to `run` the image among other things such as `push` to the registry again. This process continues over and over for all your services. 

## Under the hood facts

-  Docker is written in the `GO programming language`.
-  Docker natively uses the `libcontainer` libraries.
-  Docker uses a technology called `namespaces` to provide the isolation of the container’s file-system, network and processes.
-  Resources are also isolated. Each container has allocated individual CPU and Memory using `cgroups` from the Linux Kernel.
-  Docker uses `Copy-on-Write` file-systems for fast and efficient storage. 
-  Docker sends all outputs from from any channel to `stdout` for easy recollection and analysis.
