
# Kubespray

https://github.com/kubernetes-incubator/kubespray/blob/master/docs/getting-started.md

## kubectl cheatsheet

https://kubernetes.io/docs/reference/kubectl/cheatsheet/

setup autocomplete in bash, bash-completion package should be installed first.

```
source <(kubectl completion bash)
```

### Access Control

https://github.com/kubernetes/dashboard/wiki/Access-control

### Access Dashboard

https://github.com/kubernetes/dashboard/wiki/Accessing-Dashboard---1.7.X-and-above

```
kubectl proxy
```

http://localhost:8001/api/v1/namespaces/kube-system/services/https:kubernetes-dashboard:/proxy/

# Authorization

https://github.com/oursky/kubernetes-github-authn

```
kubectl create namespace project1
kubectl create rolebinding johndoe-admin-binding --clusterrole=admin --user=johndoe --namespace=project1
```

```
kubectl create clusterrolebinding alex-admin-binding --clusterrole=cluster-admin --user=alex
```
