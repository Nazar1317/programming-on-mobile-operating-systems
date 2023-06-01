
    Создал контейнер с веб-сервером nginx:

docker run -d -p 80:80 --name mynginx nginx

    Изменил стартовую страницу:

Перейти в контейнер и заменить файл index.html в директории /usr/share/nginx/html/ на нужный:

docker exec -it mynginx bash
cd /usr/share/nginx/html/
rm index.html
echo "Hello, World!" > index.html
exit

    Сделал проверку:

Открываю браузер и перехожу по адресу http://localhost. Должна открываться страница с текстом "Hello, World!".


    Создаю контейнер с веб-сервером Apache:

docker run -d -p 80:80 --name myapache httpd

    Изменяю стартовую страницу:

Перехожу в контейнер и заменяю файл index.html в директории /usr/local/apache2/htdocs/ на нужный:

docker exec -it myapache bash
cd /usr/local/apache2/htdocs/
rm index.html
echo "Hello, World!" > index.html
exit

    Выполняю проверку:

Открываю браузер и перехожу по адресу http://localhost. Должна будет открыться страница с текстом "Hello, World!".
