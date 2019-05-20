create_cluster.yml playbook is used for deploying Kubernetes cluster to Centos 7. Weavenet network plugin is used. Traefik Ingress contoller.

hosts file example:

[masters]  
k8s-master-4-1 ansible_host=192.168.0.1  
k8s-master-4-2 ansible_host=192.168.0.2  
k8s-master-4-3 ansible_host=192.168.0.3  
[workers]  
k8s-worker-4-1 ansible_host=192.168.0.4  
k8s-worker-4-2 ansible_host=192.168.0.5  
k8s-worker-4-3 ansible_host=192.168.0.6  
[api_balancers]  
k8s-ingress-4-1 ansible_host=192.168.0.7  
k8s-ingress-4-2 ansible_host=192.168.0.8  
[all:vars]    
k8s_version=1.12.2-0  
docker_version=docker-ce-18.06.1.ce-3.el7  
api_address=192.168.0.10 

You need to label node for balancer deployng:

kubectl label node dev-k8s-balancer1 balancer=present

kubectl taint nodes dev-k8s-balancer1 type=balancer:NoSchedule

To cancel previous command:

kubectl taint nodes dev-k8s-balancer1 type:NoSchedule-

LDAP authorization:  

https://github.com/dexidp/dex/blob/master/Documentation/kubernetes.md

