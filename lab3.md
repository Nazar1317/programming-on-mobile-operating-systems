1.
Останавливаб все запущенные контейнеры, кроме portainer:

docker stop $(docker ps -a | grep -v "portainer" | awk '{print $1}')

Удаляю все контейнеры:

docker rm $(docker ps -a -q)

Удаляю все образы:

docker image prune -a

Так же удаляю все диски:

docker volume rm $(docker volume ls   -q)

Удаляю все остановленные  контейнеры и образы:

docker system prune -a


2.
Для установки Docker Registry от автора необходимо выполнить следующие шаги:

    Скачать файлом docker-compose.yml из официального репозитория автора:

curl -O https://raw.githubusercontent.com/docker/distribution/master/docker-compose.yml

    Запустить команду docker-compose up в директории с файлом docker-compose.yml:

docker-compose up -d

Теперь вы можете использовать Docker Registry от автора. По умолчанию он прослушивает порт 5000. Чтобы загрузить образы в реестр, используйте команду docker push и добавьте префикс с именем хоста и портом:

docker push localhost:5000/myimage:tag

Для получения образов из реестра используйте команду docker pull и указывайте тот же префикс:

docker pull localhost:5000/myimage:tag

 По умолчанию Docker Registry от автора не настроен для работы с защищенными (HTTPS) соединениями.
 3.
Shipyard - это инструмент для управления Docker-контейнерами и кластерами. Для установки Shipyard и подключения к API Docker необходимо выполнить следующие шаги:

    Установить Docker и Docker Compose 

    Скачать файл docker-compose.yml для Shipyard:

curl -L https://github.com/shipyard/shipyard/raw/master/docker-compose.yml > docker-compose.yml

    Запустить Filebeat 

curl -L https://github.com/elastic/beats/raw/master/deploy/docker/filebeat.docker.yml > filebeat.docker.yml
docker-compose -f filebeat.docker.yml up -d

    Запустить Shipyard и связать его с API Docker:

docker-compose up -d

    Открыть Shipyard в браузере на локальной машине по адресу http://localhost.

    В меню "Connection" добавить новое соединение, выбрать "Docker remote API" и ввести адрес хоста tcp://docker-ip:2375, где docker-ip - это IP-адрес хоста Docker.

    Сохранить настройки и подключиться к Docker API с помощью Shipyard.

Теперь вы можете управлять контейнерами и кластерами Docker с помощью Shipyard. Все операции будут выполняться через API Docker на хосте, на котором запущен Shipyard.
4.
Для установки лимита на использование ресурсов контейнера Apache в Docker, необходимо использовать параметры запуска --cpus и --memory. Например, чтобы установить ограничение на использование 1 CPU и 512Мб оперативной памяти, можно выполнить следующую команду:

docker run -d --name myapache --cpus=1 --memory=512m httpd

Параметр --cpus устанавливает количество доступных контейнеру CPU, а параметр --memory ограничивает объем доступной оперативной памяти. Оба параметра работают только с версией Docker Engine 1.13 и выше.

Также можно задать ограничение на использование оперативной памяти с помощью параметра --memory-reservation. Этот параметр задает минимальное значение оперативной памяти, которое будет доступно для контейнера. Например:

docker run -d --name myapache --cpus=1 --memory=512m --memory-reservation=256m httpd

Эта команда устанавливает лимит на использование 1 CPU, ограничивает доступную оперативную память на 512Мб и гарантирует, что контейнеру будет доступно не менее 256Мб оперативной памяти.
