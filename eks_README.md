Why EKS?
=========
So I want to say in simple words that below are some points;
In classic Kubernetes, we are responsible for managing the control plane, 
like we have to monitor whether the server certificate is expired or not,
resources are working properly or not, faulty resource need to replace by ownself etc ..
it will take more time and costly and more manageable process.
So to reduce those problems we can use Amazon Elastic Kubernetes Service (Amazon EKS).
Utilizing Amazon EKS allows businesses to fully benefit from the AWS platform’s dependability, availability, performance,
and scale, which depends on integrations with its networking and security services.
![image](https://github.com/ghoshraja9860/learning/assets/111753645/ed2e8e4d-aeb1-4e41-af72-0e458e3689d4)
Normally time-consuming tasks, such as constructing the Kubernetes master cluster and setting service discovery, Kubernetes primitives, 
and networking, are handled by AWS EKS. Existing tools will almost certainly work through EKS with minimal if any, modifications.
1. Managed Control Plane:
   High availability, the unhealthy master will be identified and replaced during k8s running by AWS.
2. Managed Worker Nodes:
   A single command can establish, update, or terminate worker nodes.
3. Load Balancing:
   EkS supports all 3 types of load balancers,
           Application load balancers (ALB)
           Network load balancers (NLB)
           Classic load balancers (CLB)
4. Amazon EKS Logging:
   Users and cluster interaction activities are recorded in CloudTrail and this is an additional feature.

   ![image](https://github.com/ghoshraja9860/learning/assets/111753645/4beb3d44-fcaf-4e0a-8a6c-cbd72d3f033c)
   Kubernetes works on master-slave design architecture. The master is also called the control plane.
   If the master fails, then the entire cluster is down. Therefore, it is an important requirement to ensure the high availability of the master,
   Ensuring the high availability of the master and simultaneously managing all the worker nodes is a cumbersome task managed by AWS.  


   Amazon EKS components:
   ======================

   NODE: A node is a physical or virtual machine.
         In EKS both Master Node and Worker Node are managed by EKS.
         Master Nodes: A Master Node is a collection of components like Storage, Controller, Scheduler, and API server that make up the control plan of Kubernetes.
         The EKS itself creates the Master Node and manages it.
         API Servers: It controls the API servers whether it is kubctl (Kubernetes CLI) or rest API, every time components interact with API.
         ETCD: It is a highly available key-value store that is distributed among the Kubernetes cluster to store configuration data.Secure TLS.
         Controller Manager: It makes sure the actual state of the cluster matches to desired state. It is used to manage the VMs, storage, databases,
         and other resources associated with the Kubernetes cluster.
         It makes sure that you are using as much as the container needed at a point in time. It keeps a count of containers used and also records the state.
         Scheduler: It validates what and when the work needs to be done. It integrates with the Controller manager and API servers. The scheduler is an action taker.

   ![image](https://github.com/ghoshraja9860/learning/assets/111753645/2386c7d8-1ecc-469c-a63d-5462bf8349b6)
   
Worker Nodes: The worker nodes in a cluster are the machines or physical servers that run on applications. The user is responsible for creating and managing worker nodes.
kublet: It is an agent, that controls the flow to and  from the API. It makes sure containers are running in the pod. Provides success/fail report to master.
kubproxy: It includes networking rules and access control. Assigning ip to each pod.
Pods: A group of containers is called pods. The smallest unit of Kubernetes. NOTE: Kubernetes only knows pods not containers.

AWS EKS: How It Works: 
![image](https://github.com/ghoshraja9860/learning/assets/111753645/9031af3d-dce7-4e30-a7f4-3e498fcd1913)

With EKS, AWS also built an open-source CNI plugin for Kubernetes clusters running on AWS. The CNI plugin allows organizations
to use Amazon VPC networking natively with Kubernetes pods
or
Organizations can granularly control access permissions to Kubernetes masters by assigning RBAC roles directly to IAM entities.
By doing this, you can easily manage Kubernetes clusters through standard tools like kubectl.
![image](https://github.com/ghoshraja9860/learning/assets/111753645/0d7471f6-dedc-446e-bcae-76f465ab6a89)


EKS Pricing:
===============
 
As a standard, we have to pay 0.10$ /hour for each Amazon EKS cluster and we can deploy multiple applications on each EKS cluster.
We can run EKS using either EC2 or AWS Fargate, and on-premises using AWS outposts.

Now we will create a project to understand how eks works practically:
=======================================================================

The first step is we have to create an EKS cluster:
------------------------------------------------

   
