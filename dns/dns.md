# DNS test

kubectl apply -f https://k8s.io/examples/admin/dns/dnsutils.yaml

kubectl get pods dnsutils

kubectl exec -i -t dnsutils -- nslookup kubernetes.default

kubectl exec -ti dnsutils -- cat /etc/resolv.conf

k -n kube-system logs -f coredns-565d847f94-ss9ck

k get svc -A -o wide

k get endpoints -A -o wide