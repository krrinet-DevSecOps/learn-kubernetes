# Docker
Docker-Basic
https://roadmap.sh/projects/basic-dockerfile

learn-docker
Challenges with servers
Each and every applicaition is highly dependent on the Underlying OS.
One VM cannot share the under-utilized resources with the neighbour VM's.
Configuration Management [ If app-a works on VM-a, there is no guarantee that app-a works on VM-b ]
Container : This a package with your Application + Pre-requisties + Libraries. This package is the container or our artifact. If this works on your linux machine, that should any where.

To run container, what should I install ?

1) You need to have a linux machine.
2) Install Container Run Time.  ( $ dnf install docker -y  ; this install PodMan Docker )
3) You're good to run your containers.
Container vs Docker
* Container is a package of your application.
* Docker is a container run-time to run the containers on linux machine. 
Docker is a container run time.
    Docker gives us high-level runtime as it uses CONTAINERD as its run-time.
    But PodMan uses containerd with the the same as dockr 

        $ dnf install docker       ( podMan docker ; We will be using it )
        $ dnf install docker-ce    ( Docker Runtime ; actual containerRun time from docker )
What is a container ?
    Container is a package of software that contains all the required elements to run your applicaition in any environment
What is Run Time ?
To run containers, you need to have a run time and among all, DOCKER was highly used
Containers are not OS dependent, but are CPU Architecture dependent: that means, if you buld a container keeping the x86 as base, then it works only on the top of the x86 architecture. if you buld a container keeping the ARM as base, then it works only on the top of the ARM architecture.

To solve this, just 2 years, docker introduced : multi-platform docker builds.

How can I run a container ?
To run a container you need a container image + container run time.
Where can I get the container images ?
We get the base images like python, node , nginx, angularjs, go from docker-registry / ecr.io / gcr.io / acr.io 
How can I build custom images so that I can run my applicaiton as containerized ?
We will use these base images as reference and on the top of it, we will add / modify as ndded and then we wll be build these images and then save them on our contaner registry.
What is container registry ?
This is a repo to hold container images ( Judt like github for code version control system )
$ docker images This shows the list of container images that are available on your system

How a container image naming looks like ?
docker.io/userName/imageName:version
( registry)

How to pull an image from container registry ? If it's public repo, you can pull it with # docker pull image ( if you just give a generic image name, by default it pulls the image from docker registry )

If it's private repo, we need to authenticate and then download
    # docker login ( userName & password )
    # docker pull image 
accelerators:

AI:
    Ngidia: GPU 
    Google: TPU
How containers do their job ?
Keep in mind, containers are not VM's that run all the time which has SSH to allow only the authenticated users.
    
    Containers ---> START The Container ---> Container Executes The Job ---> Exits ( Completed )
Contaners are designed to manage multiple jobs that execute parallely rather as a single unit.
Containers execute one process at a time and it won't have any SSH or login based mechanism.
Containers are immutable ( which cannot be changed )

There is no concept of stop and start the container.

Start the container means ( create the container with the supplied image ) ---> Executes the job ----> Exits ( Container terminates )
VM networking & Container networking are 2 different networks. Then how VM network can talk to the container network ? Run Time bridges it using "Bridge Mode Network Adaptor"

Why port forwarding is not working with podMan docker ? -P: publishes a random port -p: We can publish a port of our choice ( Doable only on docker's docker, not on podMan docker )

Running Containers directly on vm's is not practical! Why?
1) If a container runtime machine fails, it impacts all the containers running on it indefinitely.
2) If a container fails or stops, you need to fix it manually!
3) If the number of container runtime machines grow, then adminstration would be challenge
4) You'll never have the aggregated view of the container footPrint on the container runTime machines.
5) With this, we cannot enable the communication between the containers on the other container runtime machines.
So, what's the solution ?
1) Where can I get a centralised view of all the containers running across different machines
2) If a container fails, I want the platform to manage/start or action it automatically.
3) I want seemLess network communication between the containers
4) I want to have seemless shared storage for my containers.

All of the above 4 points, can be solved by using "Container Orchestration" In this space: 1) Kubernetes ( k8s ): CNCF Product which was donated by google.

What is a Cloud Native Product ? Kubernetes is a Cloud Native Offering !!!!
    A Product which is designed keeping cloud in mind is referred as Cloud Native.
    But that does'nt mean that it's going work only on cloud.

    All the features of the Cloud Native Product can be gained only if we are on Cloud.

Kubernetes is an Open Source Container Orchestrator.
    1) Kubernetes can run both on Cloud and On-Prem  ( OpenSource )

    2) OpenShift ( RedHat ) is a Container Orchestration Platform for On-Prem

    3) On-Prem Editions For Kubernetes : Rancher, VMWare Tanzua , Openshift
Redhat ----> CNCF kubernetes  -----> OpenShift ( Pay ) 
If I want to use kubernetes what should I do ?
You can set up kubernets cluster in 2 ways : 

    1) Hardway  ( If you're on-prem )

        1) You create servers 
        2) Install container run-time on all the servers 
        3) Then install kubelet on all the servers 
        4) Install CNI Solution and install k8 and mark one of the node as Master 
    
    2) Managed Solution ( If you're cloud )

        1) All you do is use the PaS ( AWS : EKS  ,  GCP : GKE )
Kubernetes Basics and intro will be in "learn-kubernetes" repo
