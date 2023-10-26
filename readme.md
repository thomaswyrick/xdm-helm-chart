## Introduction
The intent of this chart is to simplify [Semarchy](https://semarchy.com) xDM installations. Currently, it will install xDM in a high-availability configuration and provision SSL/TLS certs using [LetsEncrypt](https://letsencrypt.org/).

### Running on minikube

1. Enable ingress in Minikube
'minikube addons enable ingress'

2. Install CRDS
'kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v1.1.0/cert-manager.crds.yaml'

3. Get IP address for K8 Ingress
'kubectl get ingress'

4. Add entries for active and passive hostnames in the hosts file pointing to ingress

5. Modify values.yaml accordingly

6. Launch
'helm install xdm-minikube .'

### Running on AKS
1. Set K8 Context
'az aks get-credentials --name ts-aks-test-2 --resource-group ts-tomwyrick-aks-test'

2. Install CRDS
'kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v1.1.0/cert-manager.crds.yaml'

3. Get IP address for K8 Ingress
'kubectl get ingress'

4. Create DNS entries for active and passive hostnames. I used Route 53.

5. Modify values.yaml accordingly

6. Launch
'helm install xdm-minikube .'





