## Introduction
The intent of this chart is to simplify [Semarchy](https://semarchy.com) xDM installations. Currently, it will install xDM in a high-availability configuration and provision SSL/TLS certs using [LetsEncrypt](https://letsencrypt.org/).

### Installation
#### General
```
helm install k8-xdm . \
--set active_host_name=xdma.yourdomain.com \
--set passive_host_name=xdm.yourdomain.com \
--set repository_driver: org.postgresql.Driver \
--set repository_url: jdbc:postgresql://<cluster-ip-address>:<cluster-port>/semarchy_repository \
--set xdm_repository_username: semarchy_repository \
--set xdm_repository_password: semarchy_repository \
--set xdm_repository_ro_username: semarchy_repository_ro \
--set xdm_repository_ro_password: semarchy_repository_ro
```

#### minikube

1. Enable ingress in Minikube
```
minikube addons enable ingress
```
2. Install cert-manager CRDS
```
kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v1.1.0/cert-manager.crds.yaml
```
3. Get IP address for ingress
```
kubectl get ingress
```
4. Add entries for active and passive hostnames in the hosts file pointing to the ingress IP
5. Launch
```
helm install k8-xdm . \
--set active_host_name=xdma.yourdomain.com \
--set passive_host_name=xdm.yourdomain.com \
--set repository_driver=org.postgresql.Driver \
--set repository_url=jdbc:postgresql://host.minikube.internal:5432/semarchy_repository \
--set xdm_repository_username=semarchy_repository \
--set xdm_repository_password=semarchy_repository \
--set xdm_repository_ro_username=semarchy_repository_ro \
--set xdm_repository_ro_password=semarchy_repository_ro \
--set ingress-nginx.enabled=false
```
