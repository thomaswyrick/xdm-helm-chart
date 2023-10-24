az aks create -n myAKSCluster -g myResourceGroup --enable-addons azure-keyvault-secrets-provider --enable-oidc-issuer --enable-workload-identity


set context
az aks get-credentials --name ts-aks-test-2 --resource-group ts-tomwyrick-aks-test

add nginx
NAMESPACE=ingress-nginx

helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update

helm install ingress-nginx ingress-nginx/ingress-nginx \
  --create-namespace \
  --namespace $NAMESPACE \
  --set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz


Install CRDS
kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v1.1.0/cert-manager.crds.yaml



helm install aks-xdm .