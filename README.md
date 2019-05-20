Скрипт create_cluster.yml используется для развертывания кластера Kubernetes на Centos 7. В качестве менеджера виртуальной сети используется Weavenet. В качестве балансера Traefik Ingress контроллер.

Пример файла hosts:

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

Для развертывания на ноде балансера необходимо проставить необходимый тэг на ноде. Пример:

kubectl label node dev-k8s-balancer1 balancer=present

Для того, чтобы запретить разворачиванию на ноде других контейнеров, кроме балансера используйте следующую команду:

kubectl taint nodes dev-k8s-balancer1 type=balancer:NoSchedule

Отмена предыдущей команды:

kubectl taint nodes dev-k8s-balancer1 type:NoSchedule-

Для развертывания на ноде некоторых сервисов необходимо проставить необходимый тэг на ноде. Примеры тегов:

kubectl label node dev-k8s-balancer1 dashboard=present


Для LDAP авторизации необходимо сгенерировать сертификаты по инструкции:  

https://github.com/dexidp/dex/blob/master/Documentation/kubernetes.md

