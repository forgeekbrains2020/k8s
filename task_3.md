# Homework Task #3

_**1. We published minio "outside" using nodePort. Do the same but using ingress.**_

Под minio-575d987896-7wsvl уже был запущен в кластере (deployment.yaml), его не трогаю:

![image](https://user-images.githubusercontent.com/72750543/151145463-0ac754ce-b67e-4f24-9497-cc982729948b.png)


Создал манифест для  Service-а и для Ingress-а:

![image](https://user-images.githubusercontent.com/72750543/151145890-7b25bbd5-ca8a-4c36-ac07-fbdf039ff6a6.png)


Разворачиваю созданные объекты в кластере:

![image](https://user-images.githubusercontent.com/72750543/151146338-df21a7f0-491f-4417-b3d5-6e90c3af6ab9.png)


Проверяю доступность:
![image](https://user-images.githubusercontent.com/72750543/151146431-35b81902-8a51-40f6-99ee-657e9b71de26.png)

![image](https://user-images.githubusercontent.com/72750543/151146576-519c3f21-7c01-479b-b07b-5bc90ef5f5e9.png)


_**3. Create deploy with emptyDir save data to mountPoint emptyDir, delete pods, check data.**_

Запустил pod dnsutils c emptyDir. Создал в каталоге /cache (mountPath) файл test. Удалил pod, проверил, что при создании pod-а в случае с emptyDir данных не сохранилось. 

![image](https://user-images.githubusercontent.com/72750543/151161188-caf781ec-552f-4da5-a685-af044a99bb2f.png)
