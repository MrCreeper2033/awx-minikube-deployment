# deploy-awx-minicube-inviroment

This project contains the code to deploy AWX inviroments on minikube with nginx Reverse Proxy.
I will build this to an ansible role in future.  

After deployment AWX will be available at "YOUR-IP":443  
Please note, if you have an active firewall on your system you may have to add a rule for port 443. 

Requirement: CentOS7 / REHL  
Tested on CentOS 7.9

ATTENTION: Please change the default PW in deploy minikube for user minikube or define an other user!

1. run deploy-minikube.yml
After this, run 2. and 3. Playbook as the user defined in deploy-minikube.yml. For default it is "minikube".

2. run deploy-awx-operator.yml
3. run deploy-awx.yml
4. run deploy-nginx-rproxy-awx.yml

# Playbooks in Detail
## deploy-awx-operator.yml
- installes git, yum-utils, docker-ce
- creates user minikube
- enable and start docker
- add user minikube to group docker
- add user minikube to sudoers
- grant ssh access for user minikube
- download and install minikube
- install systemd file for minikube
- enable and start minikube asa  service

## deploy-awx-operator.yml
- download latest awx-operator version from github
- git check out version/branch
- replace kubectl with "minikube kubectl --" in Makefile 
- deploy awx-operator and wait til it is up and runing 

## deploy-awx.yml
- copy awx deployment config
- deploy awx and wait 5 Minutes till it is available
- get admin secret

## deploy-nginx-rproxy-awx.yml
- install nginx
- enable and start nginx
- copy and modify config
- restart nginx
