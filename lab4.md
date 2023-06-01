Готовый js файл в html я беру из сети
Создал dockerfile в репозитории и в нем пишу код , который представлен ниже

FROM nginx

COPY js.html /usr/share/nginx/html

COPY style.css /usr/share/nginx/html

COPY script.js /usr/share/nginx/html

Теперь можно создать docker образы

build docker -t js

И пробовать приступать к запуску 

docker run -d -p 80;80 js

Для того чтобы воспроизвести запуск контейнера из этого Dockerfile, я выполняю следующий порядок команд:

docker build -t mywebsite .
docker run -d -p 8080:80 --restart always --name mycontainer mywebsite

Команда docker build создает Docker-образ с именем mywebsite.
Команда docker run запускает контейнер из этого образа, привязывает порт 80:80 из хостовой системы к порту 80 в контейнере, 
при завершении работы дает имя контейнеру mycontainer и дает указание контейнеру перезапуститься
После запуска контейнера, вы можно получить доступ к веб-сайту, перейдя по адресу http://localhost:8080/ в веб-браузере.
