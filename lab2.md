
    Создал контейнер с веб-сервером nginx:

docker run -d -p 80:80 --name mynginx nginx

    Изменил стартовую страницу:

Перейти в контейнер и заменить файл index.html в директории /usr/share/nginx/html/ на нужный:

docker exec -it mynginx bash
cd /usr/share/nginx/html/
rm index.html
echo "Hello, World!" > index.html
exit

    Проверка:

Открыть браузер и перейти по адресу http://localhost. Должна открываться страница с текстом "Hello, World!".
