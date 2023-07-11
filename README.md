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

===================================================go to aws cli and run below command on 3 instances=========================================
	yum install docker* -y
	systemctl start docker
	systemctl enable docker
	docker swarm init







