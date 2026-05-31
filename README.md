# kubernetis-dz04
Сетевое взаимодействие в Kubernetes

Задание 1: Настройка Service (ClusterIP и NodePort)
Задача
Развернуть приложение из двух контейнеров (nginx и multitool) и обеспечить доступ к ним:

Внутри кластера через ClusterIP.


Снаружи через NodePort.


Шаги выполнения
Создать Deployment с двумя контейнерами:
nginx (порт 80).
multitool (порт 8080).

![alt text](image.png)


Количество реплик: 3.

![alt text](image-1.png)

Создать Service типа ClusterIP, который:
Открывает nginx на порту 9001.
Открывает multitool на порту 9002.

![alt text](image-2.png)

![alt text](image-3.png)

Проверить доступность изнутри кластера:
 kubectl run test-pod --image=wbitt/network-multitool --rm -it -- sh
 curl <service-name>:9001 # Проверить nginx

![alt text](image-4.png)

 curl <service-name>:9002 # Проверить multitool

![alt text](image-5.png)

Создать Service типа NodePort для доступа к nginx снаружи.

![alt text](image-6.png)

Проверить доступ с локального компьютера:
 curl <node-ip>:<node-port>

![alt text](image-7.png)

![alt text](image-8.png)

или через браузер.

![alt text](image-9.png)



Задание 2: Настройка Ingress
Задача  "Развернуть два приложения (frontend и backend) и обеспечить доступ к ним через Ingress по разным путям."

Шаги выполнения:
Развернуть два Deployment:
frontend (образ nginx).
backend (образ wbitt/network-multitool).

![alt text](image-10.png)

Создать Service для каждого приложения.

Включить Ingress-контроллер:
 microk8s enable ingress

![alt text](image-11.png)

Создать Ingress, который:
Открывает frontend по пути /.
 ![alt text](image-12.png)

![alt text](image-14.png)


Открывает backend по пути /api.
![alt text](image-13.png)

![alt text](image-15.png)

Тестируем создание
![alt text](image-16.png)


Проверить доступность:
 curl <host>/
 curl <host>/api
или через браузер.

Создадим ingress с нужными путями
[text](ingress.yaml)
![alt text](image-17.png)

![alt text](image-18.png)

![alt text](image-19.png)

Работает!

![alt text](image-20.png)

![alt text](image-21.png)

![alt text](image-22.png)

