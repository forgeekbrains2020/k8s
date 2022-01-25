# Homework Task #2

_**1. In Minikube in namespace kube-system, there are many different pods running. Your task is to figure out who creates them, and who makes sure they are running (restores them after deletion).**_

За это отвечает kubelet. С помощью команды **kubectl describe pod -A** можно увидеть информацию о нужному поду:

![image](https://user-images.githubusercontent.com/72750543/150912571-0558b923-ea63-4951-8435-e2a508d85aa8.png)






_**2. Implement Canary deployment of an application via Ingress. Traffic to canary deployment should be redirected if you add "canary:always" in the header, otherwise it should go to regular deployment. Set to redirect a percentage of traffic to canary deployment.**_

Ниже на изображении представлена сначала конфигурация Ingress **ingress-v2.yaml** . В которой в секции **anatations** задаются настройки для редиректа при наличии загаловка:

    kubernetes.io/ingress.class: "nginx"
    
    nginx.ingress.kubernetes.io/canary: "true"
    
    nginx.ingress.kubernetes.io/canary-by-header: "canary"
    
    nginx.ingress.kubernetes.io/canary-by-header-value: "always"
    
Также идет привязка к сервису web-2,  который связан с новой версией приложения.
По запросу с заголовком curl **$(minikube ip) -H "(canary:always)"** отвечает новая версия приложения.  На запрос без заголвка отвечает старая версия.

![image](https://user-images.githubusercontent.com/72750543/150913593-796e90f9-e76f-4bf6-9bf7-f61ac4832308.png)



