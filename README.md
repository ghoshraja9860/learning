# Ansible Roles - HAProxy on AWS  

<img src="https://gorillalogic.com/wp-content/uploads/2016/10/maxresdefault-1.jpg" height=100 width=170 alt="Ansible" /> <img src="https://www.metaltoad.com/sites/default/files/styles/large_personal_photo_870x500_/public/2020-05/aws-logo-blog-header.png?itok=t4o3meiH" height=100 width=170 alt="AWS" /> <img src="https://linuxglobe.com/wp-content/uploads/2019/12/haproxy-logo.png" height=100 width=170 alt="HAProxy" /> <img src="https://rhsumon.files.wordpress.com/2012/03/apache.jpg" height=100 width=170 alt="Apache Webserver" /> 

Ansible Roles to configure a Webserver on Instance Dynamically launched on AWS Cloud and then configure a LoadBalancer to balance load between them

### Ansible Roles -   

**Role Name** | **Role Description**
------------- | --------------------
**aws** | To create a AWS Infrastructure for HAProxy and Webservers
**loadbalancer** | To configure HAProxy Loadbalancer  
**webserver** | To configure Apache Webserver

## Prerequisites   
- Ansible should be installed and Configured
- AWS CLI Should be Installed and Configured  
- Other requirements of Roles are included in Readme file of particular Role

## How to Start 
- Clone or Download this Repository
- Create ansible vault named "aws-login.yml" and put your aws_access_id and aws_access_secret_key in that

- After that Copy my ansible folder in you /etc/ directory  
  OR  
  Copy my ansible configuration only and make a groups named "webserver" and "loadbalancer" in your own inventory and also update configration file accordingly  

- Finally, Run the ansible playbook using 'ansible-playbook aws-web.yml' command or 'ansible-playbook --ask-vault-pass aws-web.yml'accordingly

## Note  
- Ansible Config file should include previliage_escalation block to become root user in order to configure AWS Instances  

# Links

[Click here for Article having detailed description](https://amanjhagrolia.medium.com/ansible-configure-haproxy-for-webserver-on-ec2-4a150b693bdf?sk=ef825092b449f60d1270051cb71d5956)  
[Post Link](https://www.linkedin.com/posts/amanjhagrolia143_ansible-configure-haproxy-for-webserver-activity-6781066201947799552-Vbgk)
  
***Feel free to Contact if any issue!!***

<a href="https://www.linkedin.com/in/amanjhagrolia143" target="_blank"> <img src="https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white" /> </a> 
