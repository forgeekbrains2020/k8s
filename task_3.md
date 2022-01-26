# Homework Task #3

_**1. We published minio "outside" using nodePort. Do the same but using ingress.**_

Под minio-575d987896-7wsvl уже был запущен в кластере (deployment.yaml), его не трогаю:

![image](https://user-images.githubusercontent.com/72750543/151145463-0ac754ce-b67e-4f24-9497-cc982729948b.png)

Создал манифест для  Servis-а и для Ingres:

![image](https://user-images.githubusercontent.com/72750543/151145890-7b25bbd5-ca8a-4c36-ac07-fbdf039ff6a6.png)




За это отвечает **kubelet**. С помощью команды **kubectl describe pod -A** можно увидеть информацию о нужному поду:
