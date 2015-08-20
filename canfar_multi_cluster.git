#CANFAR Multi Site Cluster Batch Processing

The CANFAR batch processing infrastructure is currently running on a single cluster orchestrated on one OpenStack cloud. With Nimbus, CANFAR used to run on 4 clusters at 3 different clouds, although with less total resources. Multi site clusters were handy for cloud bursting and giving users higher availability.  To achieve reliable, efficient and scalable multi-sites would probably require a new design work flow. We describe here how we would need to do multi site clusters batch processing with OpenStack in 

In order to achieve multi-site scheduling with the current CANFAR design, we need to deploy a batch scheduler server on each cluster, a central manager to collect job queues and schedules clusters, as well as a user portal hosting a job submission engine and a virtual machine management.

Below is a table of the rounded number of idle and running jobs and Virtual Machines since the beginning of 2015 and the  planned ones for multi-clusters. Although the main gain with multi-cluster is high availability, we are planning on gaining on efficiency as a side effect of over scheduling.


 Number of   | Average<br>Now | Peak<br>Now |  Average<br>Planned   |  Peak<br> Planned
-------| -------:|---------:| -------:|------:
Running Jobs| 150     | 1,100    |  300    | 2,000
Idle Jobs  | 100,000 | 300,000  | 100,000 | 300,000
VMs/day|  300    | 2,500 |   1500    |  3,000  |


The batch scheduler servers hosts the services launching batch jobs. Batch jobs in CANFAR consists of launching user submitted jobs on user launched Virtual Machines.

![Multi site cluster Architecture](http://www.canfar.phys.uvic.ca/data/pub/vospace/sfabbro/canfar_multi_cluster_architecture.png)

##Cluster Resources
CANFAR resource allocation define the resource quota in each cloud. Given the archive and VOSpace data location, we will share resources closer to the worker VMs to minimize traffic. Each cloud should have one CANFAR batch tenant with all the quota. In each cloud, only the storage replica slots are 

  
##Central Manager
The central manager gathers all user submission of jobs, collect job status and negotiate job requirements with available resources. Because user software stack in CANFAR is VM based, a VM instance manager monitors the job queue and launches or shutdowns VMs accordingly across clouds. To make sure the same VM image is used in all clouds, we used to have a common VM repository. With the current implementation the image repository is local to the cloud, so we need to synchronize them across clouds.

Central Manager  requirements: 

 - 16GB RAM, 8 cores, 1TB for data, 1 public IP
 - `HTCondor` setup for `COLLECTOR` and `NEGOTIATOR`
 - scheduler for VM instances between cloud: `cloudscheduler`
 - server to synchronize VM images between clouds: `glint-service`
 - cloud IaaS clients for instance and image managements:` OpenStack nova` and `glance`
 - contextualization for worker VMs with `cloud-init`  generated files for HTCondor and GlusterFS configuration

##POSIX Accessible VM Storage

To manage data inputs and outputs in batch jobs, most users transport their data on remote servers which are accessible with HTTP clients to the VOSpace storage. The current CANFAR VOSpace implementation is inefficient for small files,  requires reliable fail over procedures and network which are unavailable, and connect to a single point of failure in the CANFAR file database.  As a workaround to those reliability issues, we are also offering a shared file system for specific users accessible as read-only to their VMs. Not being linked to the identity framework of CANFAR, it has been so far tailored for critical users. It is not setup for intensive fast i/o such as HPC situations.

We also would like to carry on the capability of large POSIX shared file storage accessible for users. Many astronomy legacy software only work with POSIX access to file systems. Given the complexity of having user authorization across clusters and VMs and the scope of this proposal, we would restrict the file system as read-only and public.

Read-write master requirements:

 - 16GB RAM, 4 cores, 100TB of POSIX accessible storage, 1 public IP, 2x10GigE ethernet
 - SSH access for CANFAR users to setup their data
 - shared file server`GlusterFS` with geo replication setup as master
 - configuration management`puppet` agent to automate updates
 - collector agent`logstash`  to report the CANFAR monitoring and analytics
 - alert engine `nagios`or `prometheus` to quickly response issues

Read-only slave replica requirements:

 - 16GB RAM, 4 cores, 100TB of POSIX accessible storage, 1 public IP
 - same network as the worker instances
 - shared file server `GlusterFS`  with geo replication setup as slave
 
##User Job Management
Users develop code and test on VMs within their own resources not shared with batch services. To submit, manage and analyze jobs, CANFAR users can either use a batch web service for basic job management, or use command line clients on a dedicated server. User VMs need to be shared with a dedicated batch tenant. 

User job management dedicated server requirements:

 - 24GB RAM, 4 cores,  200GB of SSD for OS disk, 2TB of data disk (bare metal if number of running jobs > 5,000 to speed up disk i/o)
 - job scheduler`HTCondor` configured for the  `SCHEDD` daemon
 - OpenStack `glance` clients to share images between user tenants and batch tenant
 - CANFAR batch web service (tomcat based)
 - job submission command line CANFAR wrappers
 - configuration management`puppet` agent to automate updates
 - collector agent`logstash`  to report the CANFAR monitoring and analytics
 - engine alert system `nagios`or `prometheus` to quickly response issues
   
##Scalability

With the elasticity of current cloud IaaS, scaling up is only an issue of acquiring more resources either by increased allocation time on private clouds, or by credit card on public clouds. 
Each component of the user layer can be replicated and thus distribution is made easy. However the central manager is still one point of failure. In practice, replicating HTCondor collector is possible though not without difficulties. Other components of the central manager are not ready for automatic scalability with large increase of  either the number of users or number of tenants.

##Tasks

1. Resource deployment
VM and bare metal instances are launched according to the resource needs described above. The base OS is either Ubuntu Server or Centos.

2. Software installation
We want to manage all the servers automatically to be able to ease disaster recovery, so we will use a configuration management system to deploy all the software and updates to bare metal or VM servers described above. Monitoring and alerting are also needed on each configured servers to report back to the central monitoring service at CANFAR.  
We will therefore need the following extra software for each server:

- configuration management`puppet` agent to automate updates
- collector agent`logstash`  to report the CANFAR monitoring and analytics
- alert engine `nagios`or `prometheus` to quickly respond to failures

3. Deployment
With a few critical users, we will test and iterate from 
4. Release
Given successful deployment with alpha users, we will release the operational multi site cluster to CANFAR users.
