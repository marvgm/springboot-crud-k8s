# springboot-crud-k8s
Run &amp; Deploy Spring Boot CRUD Application With MySQL on K8S

video: <https://www.youtube.com/watch?v=I1OcFX6_09c>

# Comandos kubernetes

minikube start 

eval $(minikube docker-env)

docker images

## criar imagem da aplicação spring boot (ir na raiz com Dockerfile)

docker build -t spring-crud-k8s-example:1.0.0 .

## Deploy do config map

kubectl apply -f mysql-configMap.yaml

kubectl get configMap

## Deploy do Secrets

kubectl apply -f mysql-secrets.yaml

kubectl get secrets

## Deploy do Mysql

kubectl apply -f db-deployment.yaml

kubectl get deployments

## Entrar no pod do Mysql

kubectl get pods

kubectl logs mysql-78fd54f75f-rxxq8

kubectl exec -it mysql-78fd54f75f-rxxq8 /bin/bash

mysql -h mysql -u root -p
<informe a senha: root>

show databases;

use javatechie;

## Deploy do app no kubernates

kubectl apply -f app-deployment.yaml

kubectl get deployments

Atenção: na minha maquina a integração entre o docker e 
o minikube não funcinou. tive que subir o imagem do app
para o dockerHub(usei o intelij). 

O comando 'minikube dashboard' mostra o que aconteceu e 
pode-se deletar tudo por ele e começar novamente.

deletar deployments e service relacionado a aplicação

kubectl get pods

kubectl logs springboot-crud-deployment-6b4bdd848c-chsnk

## verificar o servico e acessar o app no kubernates

kubectl get svc

<na coluna ports, pegar a porta do svc>

ex: 8080:32225/TCP

minikube ip

192.168.49.2

então fica ip:port

--inserir pelo curl
curl -X POST -H "Content-Type: application/json" \
-d '{"name": "linuxize", "qty": 1 , "price": 200.00}' \
192.168.49.2:32225/orders

curl -X POST -H "Content-Type: application/json" \
-d '{"name": "linuxize2", "qty": 5 , "price": 201.00}' \
192.168.49.2:32225/orders

--recuperar
curl -X GET -H "Content-Type: application/json" \
192.168.49.2:32225/orders/2


minikube dashboard