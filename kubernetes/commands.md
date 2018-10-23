```bash
# To spin up the kubeadm

kubeadm init --apiserver-advertise-address 0.0.0.0

# To initialise cluster networking
kubectl apply -n kube-system -f \
    "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 |tr -d '\n')"

# To create the pod
kubectl apply -f https://raw.githubusercontent.com/kubernetes/website/master/content/en/examples/application/nginx-app.yaml
```
