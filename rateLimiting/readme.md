# Commands
## Helm command for this practice 

We are going to install the ingress nginx controller, for this we will use helm to install the official ingress
nginx chart

```sh
helm install  main nginx-stable/nginx-ingress --set controller.ingressClass=nginx --namespace nginx --create-namespace
```
Create separate ingress web
```sh
helm install web nginx-stable/nginx-ingress --set controller.ingressClass=nginx-web --namespace nginx-web --create-namespace
```
> We are going to execute this command after apply the firts Deployment

Create separate ingress api
```sh
helm install api nginx-stable/nginx-ingress --set controller.ingressClass=nginx-api --set controller.service.type=NodePort --set controller.service.httppPort.nodePort=30030  --set controller.enablePreviewPolicies=true --namespace nginx-api --create-namespace
```
> We are going to execute this command when we are going to separate the ingress from the api and frontend.

We are going to run a small pod inside kubernetes with an image busybox and we will try to reach these two different hosting
from within the cluster for ensure the communications works. So We going to use wget  command for example:

```sh
wget --header="Host: api.example.com" -qO- main-nginx-ingress.nginx
```
and

```sh 
wget --header="Host: api.example.com" --header="User-Agent: Mozilla" -qO- main-nginx-ingress.nginx
```

