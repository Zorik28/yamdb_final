# [yamdb_final](http://zorik.ddns.net/redoc/)
![КАРТИНКА](https://github.com/Zorik28/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)


### Description:
This project is designed to implement Continuous Integration
and Continuous Deployment for the api_yamdb service using the GitActions tools.
After a successful update and launch, you receive telegram notifications.
The project uses Docker containerization. To manage interaction
multiple containers, the docker-compose utility is used.


### Deployment technologies.
-Python:3.7-slim
- docker-compose 3.8
- Postgres:13.0-alpine
- Nginx:1.21.3-alpine
- Gunicorn==20.0.4


### api_yamdb technology stack.
- written in Python using Django REST Framework.
- Simple JWT library - work with JWT token
- django-filter library - request filtering


### Env-file template.
- ```DOCKER_USERNAME=<DockerHub account name>```
- ```DOCKER_PASSWORD=<DockerHub account password>```
- ```HOST=<server address>```
- ```USER=<server username>```
- ```SSH_KEY=<private key to access the server>```
- ```PASSPHRASE=<key passphrase>```
- ```TELEGRAM_TO=<id of your telegram account>```
- ```TELEGRAM_TOKEN=<telegram bot token>```
- ```DB_ENGINE=django.db.backends.postgresql```
- ```DB_NAME=<database name>```
- ```POSTGRES_USER=<database login>```
- ```POSTGRES_PASSWORD=<database password>```
- ```DB_HOST=db # service (container) name```
- ```DB_PORT=5432 # port to connect to the database```
- ```SECRET_KEY=<Django secret key>```


### Description of some commands on the server after successful deployment:
- Run migrations
```sudo docker compose exec web python manage.py migrate```
- Create superuser
```sudo docker compose exec web python manage.py createsuperuser```
- Upload statics
```sudo docker compose exec web python manage.py collectstatic --no-input```
- Filling the database
```sudo docker-compose exec web python manage.py loaddata fixtures.json```


### Request examples
**GET-request example: Get the list of all categories.**
_GET .../api/v1/categories/_

**Response example:**
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

**POST-request example with a token: adding the work.**
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
**Response example:**
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

**PATCH-request example with a token: partial update of the review by id.**  
_PATCH .../api/v1/titles/{title_id}/reviews/{review_id}/_
```
{
    "text": "string",
    "score": 1
}
```
**Response example:**
```
{
    "id": 0,
    "text": "string",
    "author": "string",
    "score": 1,
    "pub_date": "2019-08-24T14:15:22Z"
}
```


#### Author
Karapetyan Zorik  
Russian Federation, St. Petersburg, Kupchino.