## Introduction
The intent of this chart is to simplify Semarchy xDM installations. Currently, it will install xDM in high-availability configuration and provision TLS termination using [LetsEncrypt](https://letsencrypt.org/).

### Running on minikube

1. Start minikube on Mac M1
'minikube start --driver qemu --network socket_vmnet --memory 8g'

2. Enable ingress in Minikube
'minikube addons enable ingress'

3. Install NGINX Ingress
'helm upgrade --install ingress-nginx ingress-nginx \
  --repo https://kubernetes.github.io/ingress-nginx \
  --namespace ingress-nginx --create-namespace'

4. Install CRDS
'kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v1.1.0/cert-manager.crds.yaml'


5. Get IP address for K8 Ingress
'kubectl get ingress'

6. Add entries for active and passive hostnames in the hosts file pointing to ingress

7. Modify values.yaml accordingly

8. Launch
'helm install xdm-minikube .'

### Runnong on AKS
1. Set K8 Context
'az aks get-credentials --name ts-aks-test-2 --resource-group ts-tomwyrick-aks-test'

2. Install NGINX Ingress
'helm install ingress-nginx ingress-nginx/ingress-nginx \
  --create-namespace \
  --namespace ingress-nginx \
  --set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz'

3. Install CRDS
'kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v1.1.0/cert-manager.crds.yaml'


4. Get IP address for K8 Ingress
'kubectl get ingress'

5. Create DNS entries for acrtive and passive hostnames. I used Route 53.

6. Modify values.yaml accordingly

7. Launch
'helm install xdm-minikube .'





