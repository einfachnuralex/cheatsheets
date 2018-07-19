
# Get

https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-via-curl

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
```

# Create config

```
CA=ca.pem
USER=alex.pem
KEY=alex-key.pem

kubectl config set-cluster test.lan --server=https://192.168.2.1:6443 --certificate-authority=$CA
kubectl config set-credentials alex --certificate-authority=$CA --client-key=$KEY --client-certificate=$USER
kubectl config set-context default-system --cluster=test.lan --user=alex
kubectl config use-context default-system
```
