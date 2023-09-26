*Understand the EKS with a live project*
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
--------------------------------------------------
go to AWS console and search EKS or click https://ap-south-1.console.aws.amazon.com/eks/home?region=ap-south-1#
{You must have an account on aws}
![image](https://github.com/ghoshraja9860/learning/assets/111753645/2ae1dcc5-29f5-48fe-aab3-f8ded75b2b3c)
Create new cluster

#Create an IAM role 'eks-cluster-role' with 1 policy attached: AmazonEKSClusterPolicy
Create another IAM role 'eks-node-grp-role' with 3 policies attached: 
(Allows EC2 instances to call AWS services on your behalf.)
    - AmazonEKSWorkerNodePolicy
    - AmazonEC2ContainerRegistryReadOnly
    - AmazonEKS_CNI_Policy
    
 FOLLOW THE STEPS FOR IAM ROLE
 ==============================
 Go to IAM section> roles > create role
 ![image](https://github.com/ghoshraja9860/learning/assets/111753645/500f5e84-f7ff-4c05-8377-705f72e08926)
 
select aws services and search by eks and finally click on eks-cluster
==============================
![image](https://github.com/ghoshraja9860/learning/assets/111753645/ef89467a-22f5-45d1-b353-403a4a5d9e14)

![image](https://github.com/ghoshraja9860/learning/assets/111753645/68b88996-719d-45b5-a6a6-6cea19f1debb)

next 

![image](https://github.com/ghoshraja9860/learning/assets/111753645/01bda664-f481-4924-86cb-30c1c5423924)

now create.

now again come to the role section for worker-node role creation
================================
![image](https://github.com/ghoshraja9860/learning/assets/111753645/48b997b7-4137-4c39-bd15-0451e32e962f)

here we will select:
               - AmazonEKSWorkerNodePolicy
               - AmazonEC2ContainerRegistryReadOnly
               - AmazonEKS_CNI_Policy
   and giving proper role name like below

   ![image](https://github.com/ghoshraja9860/learning/assets/111753645/b8e942c4-ded8-42a1-97bd-f6603764cd43)
   ![image](https://github.com/ghoshraja9860/learning/assets/111753645/47094aa5-c991-401f-af72-70eb615ad85f)

   Finally, we made two roles for our live project for EKS cluster.
   ==============
   ![image](https://github.com/ghoshraja9860/learning/assets/111753645/825e52d0-c9cb-420f-baca-d25ac7142a3d)
   
go back to the eks cluster page and follow the below
for cluster service role add recently created role:
   ![image](https://github.com/ghoshraja9860/learning/assets/111753645/e998fc99-aace-4242-840d-a516e74ecf9f)


 choose default VPC,
 =================
 Choose 2 or 3 subnets
Choose a security group that open the ports 22, 80, 8080
cluster endpoint access: public
so go to the EC2 section> search security group:
![image](https://github.com/ghoshraja9860/learning/assets/111753645/0aa779aa-353a-40ba-ac29-2644d26097cb)


provides name asper choise
![image](https://github.com/ghoshraja9860/learning/assets/111753645/1cb0679c-5fd0-4655-ad32-54427892d18e)
![image](https://github.com/ghoshraja9860/learning/assets/111753645/28140408-686e-419d-89e9-707f36a58367)

# For VPC CNI, CoreDNS and kube-proxy, choose the default versions, For CNI, the latest and default are 
# different. But go with the default.
go back to the eks cluster
---
![image](https://github.com/ghoshraja9860/learning/assets/111753645/8c2f073f-1d93-4bdc-ab66-8c618d98922b)
for the security group select which you have created.

rest option will be as it is or default and it will take 10 mins to start the cluster control plane.
![image](https://github.com/ghoshraja9860/learning/assets/111753645/4d0d0e05-9611-49aa-8aff-277b4f18f11d)


for the worker node, we have to go compute option
-----

![image](https://github.com/ghoshraja9860/learning/assets/111753645/b6a50a90-42f2-4ef5-bf38-1823f99864e9)


Follow the option for worker node creation


Click 'Create'. This process will take 10-12 minutes. Wait till your cluster shows up as Active. 


![image](https://github.com/ghoshraja9860/learning/assets/111753645/b4d972d4-c351-41fe-9e9a-b4997066b342)

![image](https://github.com/ghoshraja9860/learning/assets/111753645/e628f5e9-4d5a-43d1-8a23-aae9066c7075)

next keep default
and for the desired node will be 1
![image](https://github.com/ghoshraja9860/learning/assets/111753645/8e2652ad-2611-42b6-a7a6-dde81df008f7)

Node group creation may take 2-3 minutes
![image](https://github.com/ghoshraja9860/learning/assets/111753645/018f794c-6993-4676-946c-51377af3c476)


 Authenticate to this cluster
===================================
Reference:
https://docs.aws.amazon.com/eks/latest/userguide/create-kubeconfig.html
Open cloud shell

# Type on your AWS CLI window 
aws sts get-caller-identity
# Observe your account and user id details

![image](https://github.com/ghoshraja9860/learning/assets/111753645/a541a5be-8a57-4140-8ab1-e6898b5f129e)

# Create a  kubeconfig file where it stores the credentials for EKS:
# kubeconfig configuration allows you to connect to your cluster using the kubectl command line.
aws eks update-kubeconfig --region region-code --name my-cluster
ex: aws eks update-kubeconfig --region ap-south-1 --name project02 # Use the cluster name you just for my region: Mumbai and cluster: PROJECT02
![image](https://github.com/ghoshraja9860/learning/assets/111753645/9b07ef84-5807-4053-8bfc-9f90799ad040)

# see if you can get the nodes you created
kubectl get nodes
# Install nano editor in cloudshell. We will need this in the next task
sudo yum install nano -y
 
 Create a new POD in EKS for the 2048 game
 ---
 ![image](https://github.com/ghoshraja9860/learning/assets/111753645/5e704e61-0e5e-471b-8d0f-18ef07ea974b)
 ![image](https://github.com/ghoshraja9860/learning/assets/111753645/1dc30ff3-ed6f-429f-94df-3e8582343695)
 
 # view the newly created pod
kubectl get pods

![image](https://github.com/ghoshraja9860/learning/assets/111753645/fc89b79a-445b-4e1e-9e3a-542bae0d2c5a)

Setup Load Balancer Service
===================================
![image](https://github.com/ghoshraja9860/learning/assets/111753645/12547274-1bf0-452e-8e09-2205dd90b9e7)

![image](https://github.com/ghoshraja9860/learning/assets/111753645/81dedfac-2554-428e-8ae5-b07ccbe20886)

The application load balancer will help to the user to communicate with the apps as apps are running in the private subnet.
ALB helps to distribute the traffic on proper services.

# view details of the modified service
![image](https://github.com/ghoshraja9860/learning/assets/111753645/d289b815-6ec0-4ec3-afa5-9108cba73ea6)


# Go to EC2 console. get the DNS name of ELB and paste the DNS into the address bar of the browser
# It will show the 2048 game. You can play. (need to wait for 2-3 minutes for the 
# setup to be complete)

![image](https://github.com/ghoshraja9860/learning/assets/111753645/df5aabcc-01bb-4434-bda0-36f76ba2a686)

![image](https://github.com/ghoshraja9860/learning/assets/111753645/edd4dc27-67be-4fb6-9584-ca099ddf4fd4)
project completed!!!!!!

Task 3: Cleanup
---------------
# Clean up all the resources created in the task
kubectl get pods --all
kubectl delete svc --all
Delete worker node and cluster also.

============================================The End==================================










 































   
