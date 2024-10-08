# Домашнее задание к занятию «Сетевое взаимодействие в K8S. Часть 1» - `Мурчин Артем`

### Цель задания

В тестовой среде Kubernetes необходимо обеспечить доступ к приложению, установленному в предыдущем ДЗ и состоящему из двух контейнеров, по разным портам в разные контейнеры как внутри кластера, так и снаружи.

------

### Чеклист готовности к домашнему заданию

1. Установленное k8s-решение (например, MicroK8S).
2. Установленный локальный kubectl.
3. Редактор YAML-файлов с подключённым Git-репозиторием.

------

### Инструменты и дополнительные материалы, которые пригодятся для выполнения задания

1. [Описание](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) Deployment и примеры манифестов.
2. [Описание](https://kubernetes.io/docs/concepts/services-networking/service/) Описание Service.
3. [Описание](https://github.com/wbitt/Network-MultiTool) Multitool.

------

### Задание 1. Создать Deployment и обеспечить доступ к контейнерам приложения по разным портам из другого Pod внутри кластера

1. Создать Deployment приложения, состоящего из двух контейнеров (nginx и multitool), с количеством реплик 3 шт.
2. Создать Service, который обеспечит доступ внутри кластера до контейнеров приложения из п.1 по порту 9001 — nginx 80, по 9002 — multitool 8080.
3. Создать отдельный Pod с приложением multitool и убедиться с помощью `curl`, что из пода есть доступ до приложения из п.1 по разным портам в разные контейнеры.
4. Продемонстрировать доступ с помощью `curl` по доменному имени сервиса.
5. Предоставить манифесты Deployment и Service в решении, а также скриншоты или вывод команды п.4.

### Решение 1

Создал Deployment приложения, состоящего из двух контейнеров (nginx и multitool), с количеством реплик 3 шт - https://github.com/artmur1/22-04-K8S/blob/main/files/deployment.yaml

![](https://github.com/artmur1/22-04-K8S/blob/main/img/22-04-01-01.png)

Создал Service, который обеспечит доступ внутри кластера до контейнеров приложения из п.1 по порту 9001 — nginx 80, по 9002 — multitool 8080 - https://github.com/artmur1/22-04-K8S/blob/main/files/svc-nginx-multitool.yaml

![](https://github.com/artmur1/22-04-K8S/blob/main/img/22-04-01-02.png)

Создал отдельный Pod с приложением multitool - https://github.com/artmur1/22-04-K8S/blob/main/files/pod-multitool.yaml

![](https://github.com/artmur1/22-04-K8S/blob/main/img/22-04-01-03.png)

Сервис работает: 

![](https://github.com/artmur1/22-04-K8S/blob/main/img/22-04-01-04.png)

Поды поднялись:

![](https://github.com/artmur1/22-04-K8S/blob/main/img/22-04-01-05.png)

Описание сервиса. Видно, что порты перенаправлены у каждого контейнера:

![](https://github.com/artmur1/22-04-K8S/blob/main/img/22-04-01-06.png)

Доступ с помощью curl по доменному имени сервиса на порт 9001:

![](https://github.com/artmur1/22-04-K8S/blob/main/img/22-04-01-07.png)

Доступ с помощью curl по доменному имени сервиса на порт 9002:

![](https://github.com/artmur1/22-04-K8S/blob/main/img/22-04-01-08.png)

------

### Задание 2. Создать Service и обеспечить доступ к приложениям снаружи кластера

1. Создать отдельный Service приложения из Задания 1 с возможностью доступа снаружи кластера к nginx, используя тип NodePort.
2. Продемонстрировать доступ с помощью браузера или `curl` с локального компьютера.
3. Предоставить манифест и Service в решении, а также скриншоты или вывод команды п.2.

### Решение 2

Создал отдельный Service приложения с возможностью доступа снаружи кластера к nginx, используя тип NodePort - https://github.com/artmur1/22-04-K8S/blob/main/files/svc-nginx-multitool-np.yaml

![](https://github.com/artmur1/22-04-K8S/blob/main/img/22-04-02-01.png)

Доступ с помощью браузера по внешнему IP адресу на порт 9001:

![](https://github.com/artmur1/22-04-K8S/blob/main/img/22-04-02-02.png)

Доступ с помощью браузера по внешнему IP адресу на порт 9002:

![](https://github.com/artmur1/22-04-K8S/blob/main/img/22-04-02-03.png)

------

### Правила приёма работы

1. Домашняя работа оформляется в своем Git-репозитории в файле README.md. Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.
2. Файл README.md должен содержать скриншоты вывода необходимых команд `kubectl` и скриншоты результатов.
3. Репозиторий должен содержать тексты манифестов или ссылки на них в файле README.md.

