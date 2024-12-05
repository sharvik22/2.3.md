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

* Создать Deployment приложения, состоящего из контейнеров nginx и multitool.

![image](https://github.com/user-attachments/assets/2511c466-9a14-4c3c-9b5a-5f4c8dcaf528)

* создал веб страницу index.html (Hello, Kubernetes!) и configmap-nginx.yaml для конфигурации Nginx.
* создал файл service.yaml для Service.

![image](https://github.com/user-attachments/assets/58943829-592b-45a7-ad7b-fa85caf8f4aa)

* Проверка

![image](https://github.com/user-attachments/assets/9d23b542-606e-41c8-acbb-0b9cb481a7ca)

![image](https://github.com/user-attachments/assets/a8bf355a-64f5-4393-9d4d-520d7a74ce1e)



---

### Решение 2

---


### Решение 1

* Создал Deployment манифест, состоящего из контейнеров nginx и multitool. Применил его.

Видно, что не запустился один из контейнеров.

![image](https://github.com/user-attachments/assets/2aebba95-4d49-4497-b274-6e820479693d)

* Смотрю логи контейнеров

![image](https://github.com/user-attachments/assets/dd972e01-1038-4bf6-bfd4-4c11f69867e2)

![image](https://github.com/user-attachments/assets/d695cf4d-b4bf-41eb-a0da-f013b7bb1607)

* Это контейнер  multitool, конфликт портов с nginx.

![image](https://github.com/user-attachments/assets/3a6936df-b639-474f-883f-efe618721471)

* Создаю и применяю манифест onfigmap-multitool.yaml для исправления ошибки.

* Так же правлю Deployment манифест, чтобы он использовал configmap. Применяю манифесты.

* Проверка

![image](https://github.com/user-attachments/assets/52067ff9-eddc-445d-8ad5-66e9e28fc31d)

























