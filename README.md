# openstack-cheat-sheet

To say it clear, this diagram is incomplete and at some points probably no fully true.
The idea is just to make the getting started simpler by providing a use case and showing the by this.

![overview] (https://raw.githubusercontent.com/michaelgruczel/openstack-cheat-sheet/master/openStackCheatSheet.png)
             
## components of open stack

all components are more or less independent and have rest APIs.
Each component potentially interacts with several other components.
Die diagram show one virtual use case from a logical point but not from 
the perspective of real technical interaction 

### Nova
offers and manages virtual machines, compute nodes, it's like AWS EC2

### Cinder
not replicated block storage for attaching and detaching external hard drives to your operating system.
The block storage can be used as normal disk storage (e.g. database), for your operating system files. 
Its like EBS (Elastic Block Store)

### Swift
replicated, scalabale Object Storage.
Storing multimedia content like videos, images, virtual machine images, backups, email storage, archives etc.
Can be used for storing static large data like backups, archives etc. It can be accessed with its own API, and is replicated cross datacenter. 
HTTP based APIs.
Swift can be compared to AWS S3

### Neutron
Networking, provide IP address both private and public

### Glance
This is used for maintaining a catalog for images and is kind of a repository for images,
like AMI (Amazon Machine Images). Stores and retrieve virtual machine disk images.

### Keystone
This component is responsible for managing authentication services for all components. 
Like credentials and authorization, and authentication for users

### Ceilometer
OpenStack Telemetry Service, statistics regarding the usage, billings

### Heat
This component manages multiple Cloud applications through an OpenStack-native REST API and a CloudFormation-compatible Query API.

### Trove
Database as a Service. Trove is Database as a Service for OpenStack. 
It's designed to run entirely on OpenStack, with the goal of allowing users to 
quickly and easily utilize the features of a relational database without the 
burden of handling complex administrative tasks. Cloud users and database 
administrators can provision and manage multiple database instances as needed. 
Initially, the service will focus on providing resource isolation at high performance 
while automating complex administrative tasks including deployment, configuration, 
patching, backups, restores, and monitoring.

### Marconi
Messaging as a Service. Marconi is a cloud messaging and notification service for 
developers building applications on top of OpenStack. The service features a 
web-friendly HTTP API, which developers can use to send messages between the 
various components of their SaaS and mobile applications, using a variety of 
communication patterns. Underlying the API is an efficient messaging engine designed 
with scalability and security in mind.

### Horizon
web-based portal to interact with all the underlying OpenStack services, 
such as NOVA, Neutron, etc.

## the use case

Let's assume we want to create a virtual machine by the Web-UI.
So we will login into Horizon. Then we want to create a virtual machine, which means 
the nova module is called for that. But we do not want to create a blank machine, 
instead we want to have an OS on it. The images are stored in Glance. 
Maybe the disk size is not big enough, so we will add a disk by using Cinder.
After the machine is created it should get an ip, there the neutron module comes in place.
The UI is doing all of them in one dialog, so we do not need do request 
the modules ourselves.
After the machine is created we will deploy a software. 
This software needs maybe a database or a broker. 
The modules Trove and Marconi can make your live easier 
(think about problems like vendor login here).
Maybe your application stores data which should be available in another datacenter.
Normally you have probably a database which runs shared on boot datacenters, 
but stuff like videos or archives should not be in a database. Here you can use Swift 
for scalable and reliable Object storeage by APIs.

## play with openstack by CLIs

openstack offer rest api, but there are command line tools as well, see

http://docs.rackspace.com/servers/api/v2/cs-gettingstarted/content/section_gs_install_nova.html

For an easy usage I prepared a vagrant box. 

    vagrant up
    vagrant ssh

Log in by vagrant ssh and then setup of environment

    export OS_AUTH_URL=...
    export OS_TENANT_ID=...
    export OS_TENANT_NAME=...
    export OS_PROJECT_NAME=...
    export OS_REGION_NAME=...
    export OS_USERNAME=...
    export OS_PASSWORD=...

create and delete a server

    # show images
    nova image-list

    # show flavors
    nova flavor-list

    # show running servers
    nova list

    #start a server (take image hash from image-list call)
    nova boot ...

    # check server with the id (see boot result) e.g. 
    nova show ....    
    
    # delete server again
    nova delete ...
    
see https://github.com/michaelgruczel/vagrant-nova-client for more details   
