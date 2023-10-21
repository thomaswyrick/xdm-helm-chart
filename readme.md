## Deploy the cert-manager

1. Add the Helm repository.
'helm repo add jetstack https://charts.jetstack.io
"jetstack" has been added to your repositories'

2. Upate the repository.
'helm repo update                                 
Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "jetstack" chart repository
Update Complete. ⎈Happy Helming!⎈'

3. Deploy cert-manager
'helm install cert-manager jetstack/cert-manager \
  --namespace cert-manager --create-namespace \
  --version v1.9.1  --set installCRDs=true'

4. Validate deployment
'kubectl get deployments --namespace cert-manager
NAME                      READY   UP-TO-DATE   AVAILABLE   AGE
cert-manager              1/1     1            1           76s
cert-manager-cainjector   1/1     1            1           76s
cert-manager-webhook      1/1     1            1           76s'


Enable ingress on Minikube
'minikube addons enable ingress'

Install NGINX
'helm install my-release oci://ghcr.io/nginxinc/charts/nginx-ingress --version 1.0.1'

Get ingress ip
'kubectl get ingress'

start minikube mac m1
minikube start --driver qemu --network socket_vmnet --memory 8g   


TODO:
Expose logs
Add app online check
Add tls
Add better logging
-job logs