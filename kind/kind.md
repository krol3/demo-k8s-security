# Creating a cluster with Kind

kind create cluster --name mycluster --config cluster.yaml

kind delete cluster --name mycluster

````
kind create cluster --name mycluster --config kind/cluster.yaml
Creating cluster "mycluster" ...
 â Ensuring node image (kindest/node:v1.25.3) đŧ 
 â Preparing nodes đĻ đĻ đĻ  
 â Writing configuration đ 
 â Starting control-plane đšī¸ 
 â Installing CNI đ 
 â Installing StorageClass đž 
 â Joining worker nodes đ 
Set kubectl context to "kind-mycluster"
You can now use your cluster with:

kubectl cluster-info --context kind-mycluster

Not sure what to do next? đ  Check out https://kind.sigs.k8s.io/docs/user/quick-start/
````

# Resources

https://kind.sigs.k8s.io/docs/user/ingress/

## add ingress

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml

