
# Homework Task #4

### 1. Create users deploy_view and deploy_edit. Give the user deploy_view rights only to view deployments, pods. Give the user deploy_edit full rights to the objects deployments, pods.


- Create private key for users deploy_view, deploy_edit:

```openssl genrsa -out deploy_view.key 2048```

```openssl genrsa -out deploy_edit.key 2048```


- Create a certificate signing request:

```openssl req -new -key deploy_view.key -out deploy_view.csr --subj "/CN=deploy_view"```

```openssl req -new -key deploy_edit.key -out deploy_edit.csr --subj "/CN=deploy_edit"```

- Sign the CSR in the Kubernetes CA. We have to use the CA certificate and the key, which are usually in /etc/kubernetes/pki. But since we use minikube, the certificates will be on the host machine in ~/.minikube:

```openssl x509 -req -in deploy_edit.csr -CA ~/.minikube/ca.crt -CAkey ~/.minikube/ca.key -CAcreateserial -out deploy_edit.crt -days 500```

```openssl x509 -req -in deploy_view.csr -CA ~/.minikube/ca.crt -CAkey ~/.minikube/ca.key -CAcreateserial -out deploy_view.crt -days 500```


- Create users in kubernetes:

```kubectl config set-credentials deploy_view --client-certificate=deploy_view.crt --client-key=deploy_view.key```

```kubectl config set-credentials deploy_view --client-certificate=deploy_view.crt --client-key=deploy_view.key```


- Create Role and RoleBinding  for deploy_view user:

![image](https://user-images.githubusercontent.com/72750543/152682280-635fe7f6-bf94-4749-b11b-91f95ba4352e.png)


- Create Role and RoleBinding  for deploy_edit user:

![image](https://user-images.githubusercontent.com/72750543/152682358-864a5f84-ab5f-49c3-8326-d1a4b6f91eb3.png)


### Create namespace prod. Create users prod_admin, prod_view. Give the user prod_admin admin rights on ns prod, give the user prod_view only view rights on namespace prod.
