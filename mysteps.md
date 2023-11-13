


Date:11/13/2023
Received assessment email at: 10:12 
Duration:240 min




Step 1 - Install NGINX Ingress Controller using Helm

Fist verify your cluster is ready:
kubectl get nodes
 

To install an NGINX Ingress controller using Helm, add the nginx-stable repository to helm, then run helm repo update . After we have added the repository we can deploy using the chart nginx-stable/nginx-ingress.


helm repo add nginx-stable https://helm.nginx.com/stable
helm repo update
 
helm install infra-nginx-ingress-trial nginx-stable/nginx-ingress --set rbac.create=true
 

Step 2 - Validate that NGINX is Running


to verify it:

kubectl get all| grep nginx

 

kubectl get pods --all-namespaces

 

kubectl get services infra-nginx-ingress-trial-controller

 

Step 3 - Exposing Services using NGINX Ingress Controller with special annotation

Sample of a host-based service mapping through an ingress controller using the type “Ingress” with special annotation nginx-trial:
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: hello-world
  annotations:
        nginx-trial/default: "on"
spec:
  ingressClassName: nginx
  rules:
  - host: zizi
    http:
      paths:
      - pathType: Prefix
        path: "/"
        backend:
          service:
            name: hello-world
            port:
              number: 80



 






















































