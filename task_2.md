# Homework Task #2

_**1. In Minikube in namespace kube-system, there are many different pods running. Your task is to figure out who creates them, and who makes sure they are running (restores them after deletion).**_

За это отвечает kubelet. С помощью команды **kubectl describe pod -A** можно увидеть информацию о нужному поду:

![image](https://user-images.githubusercontent.com/72750543/150912571-0558b923-ea63-4951-8435-e2a508d85aa8.png)






_**2. Implement Canary deployment of an application via Ingress. Traffic to canary deployment should be redirected if you add "canary:always" in the header, otherwise it should go to regular deployment. Set to redirect a percentage of traffic to canary deployment.**_

_**2.1**_ "canary:always" in the header

Ниже на изображении представлена сначала конфигурация Ingress **ingress-v2.yaml** . В которой в секции **anatations** задаются настройки для редиректа при наличии загаловка:

    kubernetes.io/ingress.class: "nginx"
    
    nginx.ingress.kubernetes.io/canary: "true"
    
    nginx.ingress.kubernetes.io/canary-by-header: "canary"
    
    nginx.ingress.kubernetes.io/canary-by-header-value: "always"
    
Также идет привязка к сервису web-2,  который связан с новой версией приложения.
По запросу с заголовком curl **$(minikube ip) -H "(canary:always)"** отвечает новая версия приложения.  

![image](https://user-images.githubusercontent.com/72750543/150913593-796e90f9-e76f-4bf6-9bf7-f61ac4832308.png)

На запрос без заголвка отвечает старая версия:

![image](https://user-images.githubusercontent.com/72750543/150915036-048b5213-b401-4424-b504-e9912638132d.png)




_**2.2**_  percentage of traffic to canary deployment

Изменяем файл **ingress-v2.yaml**, в нем определили 25 % значение для редирект на новую версию:

![image](https://user-images.githubusercontent.com/72750543/150915468-56f7c562-f28c-40be-b085-848bb70ba218.png)

Применил конфигурацию:

![image](https://user-images.githubusercontent.com/72750543/150916121-5ac987bb-9085-4e2b-a448-7aedbcae10eb.png)

Выполняю запросы. Видно, что из 5 запросов, только один пришелся на новую версию приложения:

![image](https://user-images.githubusercontent.com/72750543/150916200-a2beb6e9-2bcb-43a5-ace9-6fa2c3b41127.png)


