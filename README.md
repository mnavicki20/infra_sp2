# Проект YaMDb

## Описание

Проект yamdb позволяет пользователям оставлять отзывы на произведения разных категорий и жанров. Пользователи могут оценить призведение по 10-бальной шкале и узнать как в среднем оценили произведение другие пользователи. Если чей-то отзыв вызовет желание высказаться, пользователь может оставить к нему комментарий.


## Как запустить проект

#### Клонировать репозиторий и перейти в него в командной строке

```shell
git clone https://github.com/mnavicki20/infra_sp2
cd infra_sp2
cd api_yamdb
```

#### Cоздать и активировать виртуальное окружение

```shell
python3 -m venv venv
/venv/Scripts/activate - для Windows
python -m pip install --upgrade pip
```

#### Установить зависимости из файла requirements.txt

```shell
pip install -r requirements.txt
```

#### Переходим в папку с файлом docker-compose.yaml:

```shell
cd infra
```

#### Поднимаем контейнеры infra_db_1, infra_web_1, infra_nginx_1:

```shell
docker-compose up --build
```

#### Выполняем миграции внутри контейнера:

```shell
docker-compose exec web python manage.py makemigrations reviews
docker-compose exec web python manage.py migrate
```

#### Создаем суперпользователя:

```shell
docker-compose exec web python manage.py createsuperuser
```

#### Собираем статику:

```shell
docker-compose exec web python manage.py collectstatic --no-input
```

#### Создаем дамп базы данных (базы данных пока нет):

```shell
docker-compose exec web python manage.py dumpdata > dumpPostrgeSQL.json
```

#### Остановить контейнеры:

```shell
docker-compose down -v
```