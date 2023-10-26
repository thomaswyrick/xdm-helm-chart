## Introduction
The intent of this chart is to simplify [Semarchy](https://semarchy.com) xDM installations. Currently, it will install xDM in a high-availability configuration and provision SSL/TLS certs using [LetsEncrypt](https://letsencrypt.org/).

### Installing on minikube

1. Enable ingress in Minikube
```
minikube addons enable ingress
```
3. Install cert-manager CRDS
```
kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v1.1.0/cert-manager.crds.yaml
```
4. Get IP address for ingress
```
kubectl get ingress
```
6. Add entries for active and passive hostnames in the hosts file pointing to ingress
7. Modify values.yaml accordingly
8. Launch
```
helm install xdm-minikube .
```
### Installing on AKS
1. Set K8 context
```
az aks get-credentials --name ts-aks-test-2 --resource-group ts-tomwyrick-aks-test
```
2. Install cert-manager CRDS
```
kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v1.1.0/cert-manager.crds.yaml
```
4. Get IP address for ingress
```
kubectl get ingress
```
6. Create DNS entries for active and passive hostnames. I used Route 53.
7. Modify values.yaml accordingly
8. Launch
```
helm install aks-xdm .
```




