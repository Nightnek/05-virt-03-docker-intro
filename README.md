# Домашнее задание к занятию 4 «Оркестрация группой Docker контейнеров на примере Docker Compose»

## Задача 1

Сценарий выполнения задачи:

Установите docker и docker compose plugin на свою linux рабочую станцию или ВМ.
![image](https://github.com/user-attachments/assets/c6cd7a34-926f-4c12-9356-fbffc7044241)

Если dockerhub недоступен создайте файл /etc/docker/daemon.json с содержимым: {"registry-mirrors": ["https://mirror.gcr.io", "https://daocloud.io", "https://c.163.com/", "https://registry.docker-cn.com"]}
Зарегистрируйтесь и создайте публичный репозиторий с именем "custom-nginx" на https://hub.docker.com (ТОЛЬКО ЕСЛИ У ВАС ЕСТЬ ДОСТУП);
![image](https://github.com/user-attachments/assets/680b9293-58eb-471c-8671-35db0db2fa4f)

скачайте образ nginx:1.21.1;
![image](https://github.com/user-attachments/assets/445fc638-cda6-4ee9-a44e-c5c98b3d486b)

Создайте Dockerfile и реализуйте в нем замену дефолтной индекс-страницы(/usr/share/nginx/html/index.html), на файл index.html с содержимым:
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I will be DevOps Engineer!</h1>
</body>
</html>
![image](https://github.com/user-attachments/assets/55922d4d-58b2-4b7a-bea9-900df4af30cc)

Соберите и отправьте созданный образ в свой dockerhub-репозитории c tag 1.0.0 (ТОЛЬКО ЕСЛИ ЕСТЬ ДОСТУП).
![image](https://github.com/user-attachments/assets/05f8f4a3-0e91-4e8a-b264-aa4fbfd9175e)

Предоставьте ответ в виде ссылки на https://hub.docker.com/<username_repo>/custom-nginx/general .
https://hub.docker.com/repository/docker/nightnek/custom-nginx/general

## Задача 2
Запустите ваш образ custom-nginx:1.0.0 командой docker run в соответвии с требованиями:
имя контейнера "ФИО-custom-nginx-t2"
контейнер работает в фоне
контейнер опубликован на порту хост системы 127.0.0.1:8080
![image](https://github.com/user-attachments/assets/c140cb1e-b40a-4413-a387-9e1658ff0644)
![image](https://github.com/user-attachments/assets/3f7bf2a4-4d1f-4041-95d3-dd8a59aeacbb)

Не удаляя, переименуйте контейнер в "custom-nginx-t2"
![image](https://github.com/user-attachments/assets/16ee041e-1fe6-4f7e-83ab-3a6fc1bf77cb)

Выполните команду date +"%d-%m-%Y %T.%N %Z" ; sleep 0.150 ; docker ps ; ss -tlpn | grep 127.0.0.1:8080  ; docker logs custom-nginx-t2 -n1 ; docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html
Убедитесь с помощью curl или веб браузера, что индекс-страница доступна.
![image](https://github.com/user-attachments/assets/7f1eaf1e-b6c9-4ed7-b4f3-20538635918c)

## Задача 3

Воспользуйтесь docker help или google, чтобы узнать как подключиться к стандартному потоку ввода/вывода/ошибок контейнера "custom-nginx-t2".
Подключитесь к контейнеру и нажмите комбинацию Ctrl-C.
![image](https://github.com/user-attachments/assets/4136b19e-f378-440c-8470-5d8837839abe)

Выполните docker ps -a и объясните своими словами почему контейнер остановился.
![image](https://github.com/user-attachments/assets/e9867994-19ed-48d1-b414-ce707cf9510d)

---
Мы поключились к потоку ввода-вывода. Соответственно, нажав ctrl+c мы передали в контейнер команду остановки
---

Перезапустите контейнер
![image](https://github.com/user-attachments/assets/3d06c9c4-10e6-44f3-9870-c29b55100338)

Зайдите в интерактивный терминал контейнера "custom-nginx-t2" с оболочкой bash.
![image](https://github.com/user-attachments/assets/83234898-d3ed-4d9b-b3f4-ba232e8e7204)

Установите любимый текстовый редактор(vim, nano итд) с помощью apt-get.
![image](https://github.com/user-attachments/assets/bc1fd040-d72a-4b1a-9081-e05c6c08eebc)

Отредактируйте файл "/etc/nginx/conf.d/default.conf", заменив порт "listen 80" на "listen 81".
![image](https://github.com/user-attachments/assets/29fdcbc0-98df-4ddf-935a-cb04bd9e3e36)

Запомните(!) и выполните команду nginx -s reload, а затем внутри контейнера curl http://127.0.0.1:80 ; curl http://127.0.0.1:81.
![image](https://github.com/user-attachments/assets/81a98c7b-c564-45eb-8bf0-ff7335c673f5)

Выйдите из контейнера, набрав в консоли exit или Ctrl-D.
Проверьте вывод команд: ss -tlpn | grep 127.0.0.1:8080 , docker port custom-nginx-t2, curl http://127.0.0.1:8080. Кратко объясните суть возникшей проблемы.
![image](https://github.com/user-attachments/assets/613a8903-d1ce-49fc-9024-ae49e51f6c83)

---
у нас прот 80 проброшен на 8080. Мы поменяли прорт, на котором слушает nginx на 81, а "стучимся" на 80.
---

Это дополнительное, необязательное задание. Попробуйте самостоятельно исправить конфигурацию контейнера, используя доступные источники в интернете. Не изменяйте конфигурацию nginx и не удаляйте контейнер. Останавливать контейнер можно. пример источника
![image](https://github.com/user-attachments/assets/5b454de6-1a4c-4165-9bf8-e57cc4ad82a0)
![image](https://github.com/user-attachments/assets/78d8a55f-1659-4818-89b8-df769acbc350)
![image](https://github.com/user-attachments/assets/4ea0b664-356f-4f79-98d4-ca5ddc17ded5)
![image](https://github.com/user-attachments/assets/b73d5f5a-1a8f-4753-bbec-0aa3fe13abfe)

Удалите запущенный контейнер "custom-nginx-t2", не останавливая его.(воспользуйтесь --help или google)

---
Изменилось название, суть осталась той же.
---
![image](https://github.com/user-attachments/assets/e73be354-12c8-4c46-a97c-80761994a291)

## Задача 4

- Запустите первый контейнер из образа centos c любым тегом в фоновом режиме, подключив папку текущий рабочий каталог '$(pwd)' на хостовой машине в /data контейнера, используя ключ -v.
  ![image](https://github.com/user-attachments/assets/86d5d9d5-b283-40c7-bb49-dc623608b657)

- Запустите второй контейнер из образа debian в фоновом режиме, подключив текущий рабочий каталог '$(pwd)' в /data контейнера.
  ![image](https://github.com/user-attachments/assets/b7c3b72c-d6bf-47a1-b4b5-4d75c8454896)
  ![image](https://github.com/user-attachments/assets/46f96a75-fa97-4511-ad0f-c5fe9ac048ba)

- Подключитесь к первому контейнеру с помощью docker exec и создайте текстовый файл любого содержания в /data.
  ![image](https://github.com/user-attachments/assets/3d0f8e75-28ad-486b-96b0-ba0920ee1024)

- Добавьте ещё один файл в текущий каталог $(pwd) на хостовой машине.
  ![image](https://github.com/user-attachments/assets/076adc33-5a6b-4d81-861d-442166e454ea)

- Подключитесь во второй контейнер и отобразите листинг и содержание файлов в /data контейнера.
  ![image](https://github.com/user-attachments/assets/d880ee31-283c-4354-8948-ccf4d65ee03d)

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

## Задача 5

1. Создайте отдельную директорию(например /tmp/netology/docker/task5) и 2 файла внутри него. "compose.yaml" с содержимым:

  "docker-compose.yaml" с содержимым
  И выполните команду "docker compose up -d". Какой из файлов был запущен и почему?

  
2. Отредактируйте файл compose.yaml так, чтобы были запущенны оба файла.

3. Выполните в консоли вашей хостовой ОС необходимые команды чтобы залить образ custom-nginx как custom-nginx:latest в запущенное вами, локальное registry.



4. Откройте страницу "https://127.0.0.1:9000" и произведите начальную настройку portainer.




5. Откройте страницу "http://127.0.0.1:9000/#!/home", выберите ваше local окружение. Перейдите на вкладку "stacks" и в "web editor" задеплойте следующий компоуз



6. Перейдите на страницу "http://127.0.0.1:9000/#!/2/docker/containers", выберите контейнер с nginx и нажмите на кнопку "inspect". В представлении <> Tree разверните поле "Config" и сделайте скриншот от поля "AppArmorProfile" до "Driver".



7. Удалите любой из манифестов компоуза(например compose.yaml). Выполните команду "docker compose up -d". Прочитайте warning, объясните суть предупреждения и выполните предложенное действие. Погасите compose-проект ОДНОЙ(обязательно!!) командой.
