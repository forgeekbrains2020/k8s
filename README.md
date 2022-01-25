# Homework

1. In Minikube in namespace kube-system, there are many different pods running. Your task is to figure out who creates them, and who makes sure they are running (restores them after deletion).

2. Implement Canary deployment of an application via Ingress. Traffic to canary deployment should be redirected if you add "canary:always" in the header, otherwise it should go to regular deployment. Set to redirect a percentage of traffic to canary deployment.


![image](https://user-images.githubusercontent.com/72750543/150910753-895228e0-cc4d-4a54-953b-6d8478cca4be.png)
