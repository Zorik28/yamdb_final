# [yamdb_final](http://zorik.ddns.net/redoc/)
![КАРТИНКА](https://github.com/Zorik28/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)


### Описание:
Этот проект предназначен для реализации Continuous Integration
и Continuous Deployment для сервиса api_yamdb с помощью инструментов GitActions.
После успешного обновления и запуска вам поступают телеграм-уведомления.
В проекте используется контейнерезация Docker. Для управления взаимодействием 
нескольких контейнеров применяется утилита docker-compose.


### Технологии развёртывания.
- Python:3.7-slim
- Docker-compose 3.8
- Postgres:13.0-alpine
- Nginx:1.21.3-alpine
- Gunicorn==20.0.4


### Стек технологий api_yamdb.
- написан на Python с использованием Django REST Framework.
- библиотека Simple JWT - работа с JWT-токеном
- библиотека django-filter - фильтрация запросов


### Шаблон наполнения env-файла.
- ```DOCKER_USERNAME=<имя аккаунта на DockerHub>```
- ```DOCKER_PASSWORD=<пароль от аккаунта на DockerHub>```
- ```HOST=<адрес сервера>```
- ```USER=<имя пользователя на сервере>```
- ```SSH_KEY=<приватный ключ для доступа на сервер>```
- ```PASSPHRASE=<фраза-пароль для ключа>```
- ```TELEGRAM_TO=<id своего телеграм-аккаунта>```
- ```TELEGRAM_TOKEN=<токен телеграм-бота>```
- ```DB_ENGINE=django.db.backends.postgresql```
- ```DB_NAME=<имя базы данных>```
- ```POSTGRES_USER=<логин для подключения к базе данных>```
- ```POSTGRES_PASSWORD=<пароль для подключения к БД>```
- ```DB_HOST=db # название сервиса (контейнера)```
- ```DB_PORT=5432 # порт для подключения к БД```
- ```SECRET_KEY=<секретный ключ Django>```


### Описание некоторых команд на сервере после успешного развёртывания:
- Выполнить миграции
```sudo docker compose exec web python manage.py migrate```
- Создать суперпользователя
```sudo docker compose exec web python manage.py createsuperuser```
- Подгрузить статику
```sudo docker compose exec web python manage.py collectstatic --no-input```
- Заполнение базы данными
```sudo docker-compose exec web python manage.py loaddata fixtures.json```



### Примеры запросов
**1. Пример GET-запроса: получить список всех категорий.**
_GET .../api/v1/categories/_

**Пример ответа:**
```
[
  {
    "count": 0,
    "next": "string",
    "previous": "string",
    "results": [
      {
        "name": "string",
        "slug": "string"
      }
    ]
  }
]
```

**2. Пример POST-запроса с токеном: добавление произведения.**
_POST .../api/v1/titles/_
```
{
    "name": "string",
    "year": 0,
    "description": "string",
    "genre": [
        "string"
    ],
    "category": "string"
}
```
**Пример ответа:**
```
{
    "id": 0,
    "name": "string",
    "year": 0,
    "rating": 0,
    "description": "string",
    "genre": [
        {
            "name": "string",
            "slug": "string"
        }
    ],
    "category": {
        "name": "string",
        "slug": "string"
    }
}
```

**3. Пример PATCH-запроса с токеном: частичное обновление отзыва по id.**
_PATCH .../api/v1/titles/{title_id}/reviews/{review_id}/_
```
{
    "text": "string",
    "score": 1
}
```
**Пример ответа:**
```
{
    "id": 0,
    "text": "string",
    "author": "string",
    "score": 1,
    "pub_date": "2019-08-24T14:15:22Z"
}
```


#### Автор
Карапетян Зорик  
РФ, Санкт-Петербург, Купчино.