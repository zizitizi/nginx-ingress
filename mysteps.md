


Date:11/13/2023
Received assessment email at: 10:12 
Duration:240 min




# Step 1 - Install NGINX Ingress Controller using Helm

***Fist verify your cluster is ready:***


   kubectl get nodes

 ![image](https://github.com/zizitizi/nginx-ingress/assets/123273835/550855b1-77b2-4636-9d6b-a09c7fbf77d0)



To install an NGINX Ingress controller using Helm, add the nginx-stable repository to helm, then run helm repo update . After we have added the repository we can deploy using the chart nginx-stable/nginx-ingress.

   
   helm repo add nginx-stable https://helm.nginx.com/stable
   helm repo update




![image](https://github.com/zizitizi/nginx-ingress/assets/123273835/238548a7-1db1-4cb0-9c32-8f7d03bcb441)




   helm install infra-nginx-ingress-trial nginx-stable/nginx-ingress --set rbac.create=true
 

![image](https://github.com/zizitizi/nginx-ingress/assets/123273835/55bfd0b6-16e8-47c7-bcab-5e084fa21512)


# Step 2 - Validate that NGINX is Running


to verify it:


   kubectl get all| grep nginx



![image](https://github.com/zizitizi/nginx-ingress/assets/123273835/b439a1ec-59f6-4fcb-8a4a-91e82b6d9be3)

 

   kubectl get pods --all-namespaces



![image](https://github.com/zizitizi/nginx-ingress/assets/123273835/4c4233aa-f31b-4c90-b859-4a0c2318b96e)

 

   kubectl get services infra-nginx-ingress-trial-controller



![image](https://github.com/zizitizi/nginx-ingress/assets/123273835/b31079d5-50e1-4035-99f5-722c7b8ffbc7)


 

# Step 3 - Exposing Services using NGINX Ingress Controller with special annotation


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



 
![image](https://github.com/zizitizi/nginx-ingress/assets/123273835/5fe301b0-4532-4166-a6fb-8ec1c138dd7c)






















































