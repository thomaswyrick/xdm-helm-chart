Install CRDS
kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v1.1.0/cert-manager.crds.yaml


Enable ingress on Minikube
'minikube addons enable ingress'

Install NGINX
--Nor sure if we need this. Just use the bottom one.
'helm install my-release oci://ghcr.io/nginxinc/charts/nginx-ingress --version 1.0.1'

helm upgrade --install ingress-nginx ingress-nginx \
  --repo https://kubernetes.github.io/ingress-nginx \
  --namespace ingress-nginx --create-namespacebre

helm plugin install https://github.com/jkroepke/helm-secrets --version v4.5.1

Get ingress ip
'kubectl get ingress'

start minikube mac m1
minikube start --driver qemu --network socket_vmnet --memory 8g   


TODO:
Add tls (done)
log out semarchy.log
Add secret management
-with or without ext
Add app online check -DONE
Add all env variables for simplicity
add namespacing
-AWS specific install
-AKS specific install
make db install simpler
add all env variables
package other helm charts