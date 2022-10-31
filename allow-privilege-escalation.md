# Allow privilege escalation

k create -f kubernetes/security/allow-privilege-escalation01.yaml

## Security context

k explain pod.spec.securityContext --recursive

k explain pod.spec.containers.securityContext --recursive

## Practice

minikube ssh

mkdir /tmp/host-fs

df

mount /dev/vda1 /tmp/host-fs/

## Resources
https://www.cncf.io/blog/2020/10/16/hack-my-mis-configured-kubernetes-privileged-pods/