# Kubernetes samples manifest

## Basic sample Docker

`docker run -d --name nginx01 -p 8088:80 nginx:1.23`

`curl  http://127.0.0.1:8088`

docker exec -ti nginx01 cat /etc/resolv.conf

## Basic sample kubernetes

kubectl run demo-nginx --image=nginx:1.23

kubectl create deployment my-nginx --image=nginx:1.23

k delete deploy my-nginx

k get pods --show-labels

kubectl expose deployment my-nginx --type=NodePort --port=8085 --target-port=80

kubectl expose deployment my-nginx --type=LoadBalancer --port=8085 --target-port=80

kubectl port-forward services/my-nginx :8085

## Kubectl networking

sudo lsof -i -n -P | grep TCP

k get svc -o wide

k get endpoints

k exec -ti my-nginx-6b6b5dcbd-9fqbn -- cat /etc/resolv.conf

## kubectl basic01

## kubectl allow-privilege-escalation