#Plan for CANFAR Multi Site Cluster Batch Processing

The CANFAR batch processing  services are currently running on a single cluster orchestrated on one OpenStack cloud with Compute Canada infrastructure. CANFAR batch services used to run on 4 clusters at 3 different clouds operated by Nimbus, although with a lesser amount of total resources. Multi site clusters were handy for cloud bursting, giving users higher availability and allowing specific hardware resources separation. Reliable, scalable, and usable multi-tenant and multi-sites batch processing services would require a new framework design. We describe here how we would need to run operational multi site clusters batch processing CANFAR services with the current OpenStack sites operated on Compute Canada infrastructure, with a minimal change of our services.

In order to achieve multi-site scheduling with the current CANFAR design, we need to deploy a batch scheduler server on each cluster, a central manager to collect job queues and schedules clusters, as well as a user portal hosting a job submission engine and virtual machine management.

Below is a table of the rounded number of idle and running jobs and virtual machines since the beginning of operational OpenStack migration in January 2015 and what we would like to achieve ones for multi-site clusters. Although the main gain with multi-site clusters is high availability, we are planning on gaining on efficiency as a side effect of over scheduling.


 Number of   | Average<br>Now | Peak<br>Now |  Average<br>Planned   |  Peak<br> Planned
-------| -------:|---------:| -------:|------:
Running Jobs| 150     | 1,100    |  300    | 2,000
Idle Jobs  | 100,000 | 300,000  | 100,000 | 300,000
VMs / day|  300    | 2,500 |   1500    |  3,000  |


The batch scheduler server hosts the services launching batch jobs. Batch jobs in CANFAR consists of running user submitted jobs on user launched Virtual Machines.

![Multi site cluster architecture](https://github.com/canfar/docs/blob/master/images/canfar_multi_cluster.png)

##Cluster Resources
The CANFAR resource allocation define the resource quota in each cloud. Given the archive and VOSpace data location, we will host storage resources closer to the worker VMs to minimize network traffic. Each cloud should have one CANFAR batch tenant with all the allocated quota for batch processing. In each cloud, only the storage replica is shared among Virtual Machines. 

  
##Central Manager
The central manager gathers all user job submissions, collect job status and negotiate job requirements with available resources. Because user software stack in CANFAR is VM based, a VM instance manager monitors the job queue and launches or shutdowns VMs according to the job requirements across clouds. To make sure the same VM image is used in all clouds, a common repository. With the current implementation of OpenStack, the image repository is local to the cloud, so we need to synchronize repositories across clouds.

Central Manager  requirements: 

 - 16GB RAM, 8 cores, 1TB for data, 1 public IP
 - `HTCondor` setup for  `COLLECTOR` and `NEGOTIATOR`
 - scheduler for VM instances between cloud: `cloudscheduler`
 - synchronization server side of VM images between clouds: `glint-service`
 - cloud clients for instance and image management: `OpenStack nova` and `glance`
 - contextualization for worker VMs with `cloud-init`  generated files for `HTCondor` and `GlusterFS` configuration

## Storage
To manage data inputs and outputs in batch jobs, most users transfer their data on remote servers which are accessible via HTTP clients to the CANFAR VOSpace storage service or the CANFAR data web service. To speed up transfers, we setup local cache HTTP storage. We also offer another layer of storage for users who need fast access POSIX storage.

### Cache Storage
The cache storage is described in more details in the "Mirroring Storage" document which we summarize here.  The cache storage is designed for fast writes of incoming data from processing VMs through the web services.  The cache instances consists of HTTP servers with local disk storage.  The cache storage keeps a file for a few hours at most.

Cache storage requirements:

 - 4 nodes 32GB RAM, 12 cores, 3TB fast access disk
 - CANFAR cache storage software stack


### POSIX Storage

The current CANFAR VOSpace storage implementation is  HTTP based. It is inefficient for small files, failover procedures are not scalable, and connect to a single point of failure at the CANFAR central services for multiple database queries.  We are also offering a shared file system for specific users accessible as read-only to their VMs. It is not linked to the CANFAR identity services, it has been so far tailored only for critical users with legacy software who need POSIX access to large storage. It is also not setup for intensive fast i/o such as HPC situations. It consists of a distributed shared file system with POSIX access on regular cloud managed block devices, with geographical replication.

We also would like to carry on the capability of large POSIX shared file storage accessible for users in the multi site case and other users. Many astronomy legacy software only work with POSIX access to file systems. Given the complexity of delegating single user authorization across clusters and VMs and the scope of this proposal, we would restrict the file system as read-only and public.

Read-write master requirements:

 - 16GB RAM, 4 cores, 100TB of POSIX accessible storage, 1 public IP, 2x10GigE ethernet
 - SSH access for CANFAR users to setup their data
 - shared file server`GlusterFS` with geo replication setup as master

Read-only slave replica requirements:

 - 16GB RAM, 4 cores, 100TB of POSIX accessible storage, 1 public IP
 - same network as the worker instances
 - shared file server `GlusterFS`  with geo replication setup as slave
 
##User Job Management
Users develop code and test on VMs within their own tenant resources not shared with batch services. To submit, manage and analyze jobs, CANFAR users can either use a batch web service for basic job management, or use command line clients on a dedicated server for more complex queries. User VMs need to be shared with a dedicated batch tenant to be accessible by the cloud scheduler.

User job management dedicated server requirements:

 - 24GB RAM, 4 cores,  200GB of SSD for OS disk, 2TB of data disk (bare metal if number of running jobs > 5,000 to speed up disk i/o)
 - job scheduler`HTCondor` configured for the `SCHEDD` daemon
 - OpenStack `glance` clients to share images between user tenants and batch tenant
 - CANFAR batch web service (tomcat based)
 - job submission command line CANFAR wrappers
   
##Scalability

With the elasticity of current cloud infrastructures, scaling up is only an issue of acquiring more resources either by an increased allocation time on private clouds, or by credit card on public clouds. 
Each component of the user layer can be replicated and thus distribution is made easy. However the central manager is still a single point of failure. With more available resources, more jobs will be running increasing the load on the central manager. In practice, replicating HTCondor collector is possible though not without obstacles. Other components of the central manager are not ready for automatic scalability with large increase of  either the number of users or number of tenants.

##Tasks

1. Resource deployment

	VM instances,  bare metal instances, and persistent volumes are launched according to the resource needs described above. Instances are booted from volumes. Only necessary ports (GlusterFS, HTCondor, cache servers, database, monitoring software) are open to specific machines to connect either clouds together, to the central manager, or to the central CADC services.

2. Software installation

	We want to manage all the servers automatically to be able to ease disaster recovery, so we will use a configuration management system to deploy all the software and updates to bare metal or VM servers described above. The base OS is either Ubuntu Server or CentOS. Monitoring and alerting are also needed on each configured servers to report back to the CANFAR central monitoring service.  We will therefore need the following extra software for each deployed server instance:
	* configuration management `puppet` agent to automate updates
	* collector agent `logstash` to report the CANFAR monitoring and analytics services
	* alert engine `nagios` or `prometheus` to quickly respond to failures.

3. Deployment

	We will test and iterate the automated deployment of the CANFAR batch VMs on the clouds. Critical alpha users will run a thousands of jobs while we monitor the proper scheduling of the job,  scalability of both the storage VOSpace and local access.

4. Release

	Given successful deployment with alpha users, we will release the operational multi site cluster to CANFAR users.
