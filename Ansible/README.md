Скрипт create_cluster.yml используется для развертывания кластера Kubernetes с тремя нодами master и неограниченным количеством нод worker. В качестве менеджера виртуальной сети используется Weavenet. В качестве балансера Traefik Ingress контроллер.

Пример файла hosts:

[init-master]  
172.16.0.54 ansible_user='administrator' ansible_sudo_pass='password'  
[master]  
172.16.0.55 ansible_user='administrator' ansible_sudo_pass='password'  
172.16.0.56 ansible_user='administrator' ansible_sudo_pass='password'  
[worker]  
172.16.0.53 ansible_user='administrator' ansible_sudo_pass='password'  
172.16.0.57 ansible_user='administrator' ansible_sudo_pass='password'  
172.16.0.58 ansible_user='administrator' ansible_sudo_pass='password'  
172.16.0.59 ansible_user='administrator' ansible_sudo_pass='password'  
[all:vars]  
api_address=172.16.0.53  
init_master=172.16.0.54  
first_master_ip=172.16.0.54  
second_master_ip=172.16.0.55  
third_master_ip=172.16.0.56  
first_master_hostname=dev-k8s-master1  
second_master_hostname=dev-k8s-master2  
third_master_hostname=dev-k8s-master3  

Для развертывания на ноде балансера необходимо проставить необходимый тэг на ноде. Пример:

kubectl label node dev-k8s-balancer1 balancer=present

Для того, чтобы запретить разворачиванию на ноде других контейнеров, кроме балансера используйте следующую команду:

kubectl taint nodes dev-k8s-balancer1 type=balancer:NoSchedule

Отмена предыдущей команды:

kubectl taint nodes dev-k8s-balancer1 type:NoSchedule-

Для развертывания на ноде некоторых сервисов необходимо проставить необходимый тэг на ноде. Примеры тегов:

kubectl label node dev-k8s-balancer1 dashboard=present
