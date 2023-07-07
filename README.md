# pr0l_microservices

# ДЗ по Docker-4
В ходе выполнения ДЗ познакомились с сетями в докере, с утилитой docker-compose.

Основу имени проекта получаем из названия текущей директории. Поменять можно либо флагом --project-name / -p при запуске docker compose, либо задав переменную окружения COMPOSE_PROJECT_NAME

Описали проект в одном файле docker-compose.yml, установив переменные окружения. Запуск проекта осуществляется:
```
docker compose up -d
```
в директории где находится файл docker-compose.yml, для запуска проекта с другим название файла необходимо использовать флаг -f и указать путь и название файла.

Задания со ⭐
Создан docker-compose.override.yml для reddit проекта, который позволит:
    • Изменять код каждого из приложений, не выполняя сборку образа
    • Запускать puma для руби приложений в дебаг режиме с двумя воркерами (флаги --debug и -w 2)

# ДЗ по Docker-3
- Загружено приложение reddit-microservices;
- Реализовано через Dockerfile сборка и разворачивание трех приложений "comment" "post-py" "ui";
- Дополнительно оптимизирована сборка приложения post-py (обновлены версии компонентов и отключен лог так как мешало запуску, требуется привлечение разработчика для обновления кода) тем самым убраны при сканировании в 0 уязвимости приложения;
- Оптимизировано использование базовых образов тем самым уменьшены размеры докер образов в десятки раз;
- Дополнительно запускаем mongodb с подключением локального volme для хранения сообщений;

Задания со ⭐
 1. Запуск контейнеров с другими алиасами и передача данных с помощью переменных.
'''docker run -d --network=reddit --network-alias=post_db_01 --network-alias=comment_db_01 mongo:latest
docker run -d --network=reddit -e POST_DATABASE_HOST=post_db_01 -e POST_DATABASE=posts_01 --network-alias=post_01 pr0l/post:1.0
docker run -d --network=reddit -e COMMENT_DATABASE_HOST=comment_db_01 -e ENV COMMENT_DATABASE=comments_01 --network-alias=comment_01 pr0l/comment:1.0
docker run -d --network=reddit -e  POST_SERVICE_HOST=post_01 -e COMMENT_SERVICE_HOST=comment_01 -p 9292:9292 pr0l/ui:1.0'''

Образ на основе alpine Dockerfile.01.
'''FROM alpine
RUN apk update --no-cache \
    && apk add --no-cache ruby ruby-dev ruby-bundler build-base \
    && gem install bundler --no-rdoc --no-ri \
    && rm -rf /var/cache/apk/*'''
собираем:
'''docker build -t pr0l/ui:3.0 ./ui --file ui/Dockerfile.01'''


# ДЗ по Docker-2
В рамках данного ДЗ:
- Установил docker, docker-compose, docker machine
- Создал свой образ
- Создал docker host
- Зарегистрировался на Docker Hub и загрузил образ в публичное хранилище

Есть ошибки которые не смог понять.
Не весь контент прогружается.
