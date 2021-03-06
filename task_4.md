
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


- Set context for users:

```kubectl config set-context deploy_view --cluster=minikube --user=deploy_view```

```kubectl config set-context deploy_edit --cluster=minikube --user=deploy_edit```


- Create Role and RoleBinding  for deploy_view user:

![image](https://user-images.githubusercontent.com/72750543/152682280-635fe7f6-bf94-4749-b11b-91f95ba4352e.png)


- Create Role and RoleBinding  for deploy_edit user:

![image](https://user-images.githubusercontent.com/72750543/152682358-864a5f84-ab5f-49c3-8326-d1a4b6f91eb3.png)




### 2. Create namespace prod. Create users prod_admin, prod_view. Give the user prod_admin admin rights on ns prod, give the user prod_view only view rights on namespace prod.

- Create namespace prod:

```kubectl create ns prod```

- Create users prod_admin, prod_view. ???????????????????? ?????????????? ??????????????. ???????? ?????????????? ?????????? ???? ????????????????????.


- Create Role and RoleBinding  for users:

![image](https://user-images.githubusercontent.com/72750543/152685430-0a9303a8-df9e-4148-bea3-d76c66520f98.png)

- Switch to context "prod_admin" and create deployment:

![image](https://user-images.githubusercontent.com/72750543/152685526-a83fa280-4f0e-423a-862b-af428f74dd1d.png)

???????????????????? ?????????????? ????????????.

- Switch to context "prod_view" and try delete deployment.

![image](https://user-images.githubusercontent.com/72750543/152685610-687931c3-9cf1-4981-a6cd-8fb961907b7f.png)


?? prod_view  ???? ?????????????? ????????  ?????????????? deployment.

### 4. Create a serviceAccount sa-namespace-admin. Grant full rights to namespace default. Create context, authorize using the created sa, check accesses.

- Create a serviceAccount sa-namespace-admin. Get secret for serviceAccount sa-namespace-admin.

![image](https://user-images.githubusercontent.com/72750543/152686717-f972b886-c81a-4601-bc11-bd778a86fc04.png)


- ?????????????? ???????????????????? ???????????? ???? 4:
![image](https://user-images.githubusercontent.com/72750543/152687723-624e3548-c645-41fe-b130-0646686babb2.png)

- ???????????? ?????? ???????? pod:

![image](https://user-images.githubusercontent.com/72750543/152687789-cc6e8230-5b8c-4c16-9fc3-7948611a2898.png)


- Role Bindins  ?? ?????????????? admin:

![image](https://user-images.githubusercontent.com/72750543/152687894-031c9582-bb22-41be-8f19-24cbd9657a94.png)



