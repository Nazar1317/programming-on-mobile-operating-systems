1.
Предположим, что в предыдущей работе были использованы технологии HTML, CSS и JavaScript для создания одностраничного сайта. Чтобы примонтировать volume, который будет содержать файлы сайта, мы можем создать новый Dockerfile и использовать его для создания контейнера, который будет примонтировать указанную папку в качестве volume.

Например, предположим, что можно примонтировать локальную папку "my-website" в качестве папки "/usr/share/nginx/html" в контейнере nginx. Для этого я использую следующий Dockerfile:

FROM nginx:latest

COPY nginx.conf /etc/nginx/nginx.conf
VOLUME /usr/share/nginx/html

В этом Dockerfile я скопировал файл "nginx.conf" в контейнер и указал, что папка "/usr/share/nginx/html" должна быть использована в качестве volume. Файл "nginx.conf" содержит конфигурацию Nginx, которая будет заставлять сервер обслуживать файлы из примонтированного volume.

После сборки Docker-образа, запускаю контейнер, примонтировав локальную папку в качестве volume. Длею это с помощью  команды:

docker run -d --name my-website -p 8080:80 -v /path/to/my-website:/usr/share/nginx/html nginx

В этой команде запускаю контейнер с именем "my-website" и привязываю порт 8080 хостовой системы к порту 80 контейнера. Ключ "-v" указывает, что нужно примонтировать локальную папку в качестве volume. Наконец, мы запускаем контейнер на основе образа nginx.

После того, как контейнер запущен, содержимое локальной папки будет отображаться на веб-сайте, который запущен на порту 8080. 
2.
Для начала создаю простую таблицу в PostgreSQL:

CREATE TABLE my_table (
	id serial primary key,
	name varchar(50),
	age int,
	email varchar(255)
);
Так же можно заполнить это некоторыми тестовыми данными:

INSERT INTO my_table (name, age, email)
VALUES
	('Alice', 25, 'alice@example.com'),
	('Bob', 30, 'bob@example.com'),
	('Charlie', 35, 'charlie@example.com');

Выполню запрос для выборки данных из таблицы:

SELECT * FROM my_table;

Результатом получил три строки с данными.
CREATE TABLE orders (
	order_id serial primary key,
	customer_name varchar(50),
	product_name varchar(50),
	price decimal(8, 2),
	quantity int,
	order_date date
);

В этой таблице есть несколько полей: order_id - целочисленный, автоматически генерируемый ключ, customer_name - строка, product_name - строка, price - число с фиксированной точкой, quantity - целое число и order_date - дата.

Добавляю несколько строк в эту таблицу, используя следующий запрос:

INSERT INTO orders (customer_name, product_name, price, quantity, order_date)
VALUES
	('Alice', 'iPhone', 800.00, 1, '2022-01-01'),
	('Bob', 'Samsung Galaxy', 700.00, 2, '2022-01-02'),
	('Charlie', 'Google Pixel', 600.00, 3, '2022-01-03');

Теперь, выполняю запрос на выборку данных из этой таблицы:

SELECT * FROM orders;

В результате получаю  три строки с данными, которые я только что вставил.
3.
Для того чтобы проинспектировать Docker контейнер на наличие volume,выполняю следующую команду, указав имя контейнера:

docker inspect <имя_контейнера> --format '{{ json .Mounts }}'

Например, если я хочу проинспектировать контейнер с именем my-website, буду выплнять следующую команду:

docker inspect my-website --format '{{ json .Mounts }}'

В результате выполнения команды получается список всех подключенных к контейнеру volume, а также их свойства.

Чтобы запустить контейнер, который примонтирует volume,  используется команда:

docker run -d --name my-website -p 8080:80 -v /path/to/my-website:/usr/share/nginx/html nginx

Здесь ключ "-v" указывает на примонтирование папки /path/to/my-website хостовой системы внутрь контейнера nginx в качестве volume. Конечно, для запуска контейнера я заменяю "/path/to/my-website" на реальный путь до папки с файлами сайта на машине.

Стоит обратить внимание, что при запуске этой команды Docker автоматически создаст новый volume, если он не существует.

После запуска контейнера, открывается браузер и для перехода на сайт, который будет запущен на порту 8080. Все файлы в папке /path/to/my-website будут отображаться на веб-сайте, а любые изменения, сделанные в локальной папке на хостовой системе, будут автоматически отображаться на веб-сайте внутри контейнера.
