# Dockered Django Template with Postgres, Gunicorn, and Nginx

### About

- Docker Compose 2.13.02
- Python 3.11.0
- Django 4.1.4
- Gunicorn 20.1.0
- PostgreSQL 15.1
- Nginx 1.23.0

## Development
1. Update the environment variables in the docker-compose.yml and .env.dev files.
2. Build the image: `~/docker_on_server`
    ```shell
    $ docker-compose up -d --build
    ```
3. Navigate to  [http://localhost:8000/]()

Commands to manage image:
`~/docker_on_server`
```shell
$ docker-compose exec web python manage.py flush --no-input
$ docker-compose exec web python manage.py migrate
```


## Production
#### Gunicorn + Nginx
1. Spin down the development containers:
   ```shell
   $ docker-compose down -v
   ```
2. Update the environment variables.
   - `.env.prod`
   - `.env.prod.db`
3. Build production images and spin up:
   ```shell
   $ docker-compose -f docker-compose.prod.yml up -d --build
   ```
4. Navigate to [http://localhost:1337/admin]()


Commands to manage image:
```shell
$ docker-compose -f docker-compose.prod.yml exec web python manage.py migrate --noinput
$ docker-compose -f docker-compose.prod.yml exec web python manage.py collectstatic --no-input --clear
```

