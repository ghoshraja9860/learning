                     ===========================Docker swarm visualizer================================

#This is a basic project for larning purpose and we don't use this process in real world production deployment.
For production we must take all security precautions.#
visualizer project:
Here will see how docker services are running in docker container on a docker swarm diagram and it will be in visual format.
we will see every services in each container and how docker swarm will help to distribute task or sevices among the containers.

so to make this project easy I will explain step by step and it will very help full for beginer also.
so lets start:
Pre-req: 1. aws acc (free tier)
        2. basic knowledge on docker

First will launch 3 ec2 instances on t2.micro which is free and amazon-linux-2 

<img width="871" alt="image" src="https://github.com/ghoshraja9860/learning/assets/111753645/0f7a2845-587c-4bba-9632-e0aca962ee84">

<img width="865" alt="image" src="https://github.com/ghoshraja9860/learning/assets/111753645/ef25bb22-c724-445f-81b0-17ada18a31a7">

for network setting alltrafic allow must be enable

<img width="804" alt="image" src="https://github.com/ghoshraja9860/learning/assets/111753645/b0575881-730f-451d-8879-381eee02f977">
Finally it will show like this

<img width="760" alt="image" src="https://github.com/ghoshraja9860/learning/assets/111753645/b14f3356-5f91-48c3-b6b3-48b61d89e650">

======================go to aws cli and run below command on 3 instances===========================


	yum install docker* -y
	systemctl start docker
	systemctl enable docker

 now we are reaching to our project arena: 
 make one server as a manager and rest two will be act as workers
 
 <img width="959" alt="image" src="https://github.com/ghoshraja9860/learning/assets/111753645/87d9a217-4b0a-4d28-be18-d3a259796461">
docker swarm init (run this command to docker main server or manager )

please notice 'To add a worker to this swarm, run the following command:' this line as we have to paste below token details to other two nodes or worker instance so that
both can be attached with manager instance.
now paste token id to others instance and take ip adresses of all instances (private and public)

<img width="878" alt="image" src="https://github.com/ghoshraja9860/learning/assets/111753645/36a90089-2a08-4aa6-acc0-5aefdeb457c3">

docker service create --name=viz --publish=8080:8080/tcp --constraint=node.role==manager --mount=type=bind,src=/var/run/docker.sock,dst=/var/run/docker.sock dockersamples/visualizer

use above command in manager inst. if showing any error regarding port [If port 8080 is already in use on your host, you can specify e.g. -p [YOURPORT]:8080] can use 5000:8080 port details.

<img width="957" alt="image" src="https://github.com/ghoshraja9860/learning/assets/111753645/2b1521ad-e797-498e-9548-489a8a3febe8">

Remember aws not allow to use private ip to hit outsider so we will use public ip and same time wthat will we see?
copy manager's public ip and paste to browser like 

<img width="551" alt="image" src="https://github.com/ghoshraja9860/learning/assets/111753645/592fc6d6-53fb-40e7-a239-215bd376d5f9">

 so here we can see manager and workers are in running mode and manager holding this service.
 net we can create another service and let see what actually swarm will act

 
run 'docker service create --name webserver -p 8080 --replicas 3 nginx'

 <img width="551" alt="image" src="https://github.com/ghoshraja9860/learning/assets/111753645/4a01455c-0ed5-4f73-897d-e1808dbb63be">
 
 here 3 service is activaten can later more or scale up .
 
 <img width="551" alt="image" src="https://github.com/ghoshraja9860/learning/assets/111753645/70f56f22-73aa-4949-bf90-ff7791bb74f6">



 see the changes how swarm distributed the services among the nodes.
 So we can see like a picture where the service is going and where not.

 can do more experience like 

 <img width="618" alt="image" src="https://github.com/ghoshraja9860/learning/assets/111753645/4580688c-bf3c-4a9c-97a7-99833cfa303b">

<img width="834" alt="image" src="https://github.com/ghoshraja9860/learning/assets/111753645/ed6f94d9-1615-4ce2-a85f-e185147aec60">


what happend if one node is go down? 

<img width="271" alt="image" src="https://github.com/ghoshraja9860/learning/assets/111753645/f86f30c3-00e5-4343-ab7b-d7abd26e2f18">

and

<img width="861" alt="image" src="https://github.com/ghoshraja9860/learning/assets/111753645/670c01d6-4e61-48aa-b18e-a6e3aa342aef">

now see whaen we off the one worker node automatically services are distributed amonth manager and another worker node ..

I hope it is cleared how docker swarm works!!!!






