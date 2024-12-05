# Домашнее задание к занятию «Конфигурация приложений» Шарапат Виктор

### Цель задания

В тестовой среде Kubernetes необходимо создать конфигурацию и продемонстрировать работу приложения.

------

### Чеклист готовности к домашнему заданию

1. Установленное K8s-решение (например, MicroK8s).
2. Установленный локальный kubectl.
3. Редактор YAML-файлов с подключённым GitHub-репозиторием.

------

### Инструменты и дополнительные материалы, которые пригодятся для выполнения задания

1. [Описание](https://kubernetes.io/docs/concepts/configuration/secret/) Secret.
2. [Описание](https://kubernetes.io/docs/concepts/configuration/configmap/) ConfigMap.
3. [Описание](https://github.com/wbitt/Network-MultiTool) Multitool.

------

### Задание 1. Создать Deployment приложения и решить возникшую проблему с помощью ConfigMap. Добавить веб-страницу

1. Создать Deployment приложения, состоящего из контейнеров nginx и multitool.
2. Решить возникшую проблему с помощью ConfigMap.
3. Продемонстрировать, что pod стартовал и оба конейнера работают.
4. Сделать простую веб-страницу и подключить её к Nginx с помощью ConfigMap. Подключить Service и показать вывод curl или в браузере.
5. Предоставить манифесты, а также скриншоты или вывод необходимых команд.

------

### Задание 2. Создать приложение с вашей веб-страницей, доступной по HTTPS 

1. Создать Deployment приложения, состоящего из Nginx.
2. Создать собственную веб-страницу и подключить её как ConfigMap к приложению.
3. Выпустить самоподписной сертификат SSL. Создать Secret для использования сертификата.
4. Создать Ingress и необходимый Service, подключить к нему SSL в вид. Продемонстировать доступ к приложению по HTTPS. 
4. Предоставить манифесты, а также скриншоты или вывод необходимых команд.

------

### Правила приёма работы

1. Домашняя работа оформляется в своём GitHub-репозитории в файле README.md. Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.
2. Файл README.md должен содержать скриншоты вывода необходимых команд `kubectl`, а также скриншоты результатов.
3. Репозиторий должен содержать тексты манифестов или ссылки на них в файле README.md.

------

### Решение 1

* Создал Deployment манифест, состоящего из контейнеров nginx и multitool. Применил его.

Видно, что не запустился один из контейнеров.

![image](https://github.com/user-attachments/assets/2aebba95-4d49-4497-b274-6e820479693d)

* Смотрю логи контейнеров

![image](https://github.com/user-attachments/assets/dd972e01-1038-4bf6-bfd4-4c11f69867e2)

![image](https://github.com/user-attachments/assets/3a6936df-b639-474f-883f-efe618721471)


* Это контейнер  multitool, конфликт портов с nginx.

![image](https://github.com/user-attachments/assets/d695cf4d-b4bf-41eb-a0da-f013b7bb1607)


* Создаю и применяю манифест configmap-multitool.yaml для исправления ошибки.

* Так же правлю Deployment манифест, чтобы он использовал configmap. Применяю манифесты.

* Проверяю, что под запущен и два контейнера, так же работы service.

![image](https://github.com/user-attachments/assets/e7392a01-4d57-459c-b4bc-7529ee5ce395)

* Проверяю доступность страницы, вывод curl.

![image](https://github.com/user-attachments/assets/dd9e7e02-d046-42d0-a10c-af4dc56acf93)

---

### Решение 2

* Создал и применил манифест с nginx.

![image](https://github.com/user-attachments/assets/87dd05b3-6b66-44f6-9dad-522c7a6770ad)

* Создал web-страницу и подключил её как ConfigMap.

![image](https://github.com/user-attachments/assets/501abaea-58a8-487b-b029-a6d40eb50212)

* Выпустил самородписанные ssl сертификаты c SANs:

## openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout tls.key -out tls.crt -subj "/CN=nginx-example.com/O=nginx-example.com" -addext "subjectAltName=DNS:nginx-example.com"

* Создал secret для использования сертификатов.

## kubectl create secret tls nginx-tls --key tls.key --cert tls.crt -n dz8

* Создал и применил манифест service.

![image](https://github.com/user-attachments/assets/fff7d37b-d827-4619-a9c0-a042455bf4c2)

* Срздал и пременил ingress.yaml (важно прописать в хостах и связать доменное имя с контроллером ingress).

![image](https://github.com/user-attachments/assets/6c8f6d3b-4a8e-46a0-8bb0-4e645b5e37ee)


* Проверка

![image](https://github.com/user-attachments/assets/fee3e8a9-8e97-4db4-9e59-2f96e30be1a9)

![image](https://github.com/user-attachments/assets/6c84f18a-3349-416a-8f87-c36b8b439204)

![image](https://github.com/user-attachments/assets/71895771-784b-4389-9838-c24a284d181d)

![image](https://github.com/user-attachments/assets/fdb1bda8-4fad-4b8a-bf12-bbc8cdc71527)

![image](https://github.com/user-attachments/assets/45d1ccd2-a3aa-4f19-b028-98829005aa98)


  




---
























