- Убедимся, что все таблицы Django по умолчанию были созданы

    `$ docker-compose exec db psql --username=app_main --dbname=app_main_dev` 

- проверить, что том (volume) был создан

    `$ docker volume inspect api-docker_postgres_data` 

- Пересоберем заново образы

    `$ docker-compose up -d --build`

- Остановить контейнер

    `$ docker-compose down -v`

- Приостановить контейнер

    `docker stop CONTAINER ID`

- Запустить ранее остановленный контейнер

    `docker start CONTAINER ID`

- Перегрузить контейнер

    `docker restart CONTAINER ID`

- Посмотреть работающие контейнеры

    `docker ps`
    `docker ps -a`

- Посмотреть список всех образов

    `docker images`

- Удалить образ

    `docker rmi CONTAINER ID`

- Логи
    `docker-compose logs -f`

- Создание нового образа и запуск контейнера

    `
    $ docker build -f ./api-fois/Dockerfile -t app_main:latest ./api-fois
    $ docker run -d \
        -p 8006:8000 \
        -e "SECRET_KEY=please_change_me" -e "DEBUG=1" -e "DJANGO_ALLOWED_HOSTS=*" \
        app_main python /usr/src/api-fois/manage.py runserver 0.0.0.0:8000
    `

- Активация среды

    `source api-fois/env/bin/activate`

- Запуск: 
  - dev

    - `$ docker-compose down -v`

    - `$ docker-compose up -d --build`

  - prod

    - `$ docker-compose -f docker-compose.prod.yml down -v`

    - `$ docker-compose -f docker-compose.prod.yml up -d --build`

    - `$ docker-compose -f docker-compose.prod.yml exec web python manage.py migrate --noinput`

    - `$ docker-compose -f docker-compose.prod.yml exec web python manage.py collectstatic --no-input --clear`