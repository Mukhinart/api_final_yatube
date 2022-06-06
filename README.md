### _Описание_

API для проекта Yatube (Социальная сеть блогеров).
У неаутентифицированных пользователей доступ к API только на чтение (за исключением эндпоинта ```/follow/```).
Аутентифицированным пользователям разрешено изменение и удаление своего контента; в остальных случаях доступ предоставляется только для чтения.

Документация к API с доступными методами находится по адресу ```http://127.0.0.1:8000/redoc/```

### _Технологии_

![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![DjangoREST](https://img.shields.io/badge/DJANGO-REST-ff1709?style=for-the-badge&logo=django&logoColor=white&color=ff1709&labelColor=gray)
![JWT](https://img.shields.io/badge/JWT-black?style=for-the-badge&logo=JSON%20web%20tokens)

### _Инструкция по запуску проекта для Windows:_

- Склонируйте проект из репозитория:

```sh
$ git clone https://github.com/mukhinart/api_final_yatube.git
```

- Установите и активируйте виртуальное окружение:

```sh
python -m venv venv 
source venv/Scripts/activate
``` 

- Установите зависимости из файла requirements.txt:

```sh
pip install -r requirements.txt
``` 

- Выполните миграции в папке с файлом manage.py:

```sh
python manage.py migrate
```

- Запустите dev-сервер. В папке с файлом manage.py выполните команду:

```sh
python manage.py runserver
```

***

### Примеры использования API для любых пользователей:

- Для неавторизованных пользователей работа с API доступна в режиме чтения.

```sh
GET api/v1/posts/ - получить список всех постов.
При указании параметров 'limit' и 'offset' выдача работает с пагинацией:
GET /api/v1/posts/?limit=2&offset=4 - выдача 2-х постов, с пятого по шестой
```

```sh
GET api/v1/posts/{id}/ - получение поста по id
GET api/v1/groups/ - получение списка групп
GET api/v1/groups/{id}/ - получение информации о группе по id
GET api/v1/{post_id}/comments/ - получение всех комментариев к посту
GET api/v1/{post_id}/comments/{id}/ - Получение комментария к посту по id
```

### Примеры работы с API для авторизованных пользователей:

- Доступ к API авторизованным пользователям предоставляется только с JWT-токеном.

#### Получение токена

- Получение JWT-токена осуществляется через POST-запрос к эдпоинту:

```
POST api/v1/jwt/create/
```

В запросе необходимо передать поля:

1. ```username``` - имя пользователя;
2. ```password``` - пароль пользователя.

- API вернет JWT-токен в поле ```access```, данные из поля ```refresh``` понадобятся для обновления токена.

```
# Пример ответа
{
    "refresh": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTYyMDk0MTQ3NywianRpIjoiODUzYzE5MTg5NzMwNDQwNTk1ZjI3ZTBmOTAzZDcxZDEiLCJ1c2VyX2lkIjoxfQ.0vJBPIUZG4MjeU_Q-mhr5Gqjx7sFlO6AShlfeINK8nA",
    "access": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNjIwODU1Mzc3LCJqdGkiOiJkY2EwNmRiYTEzNWQ0ZjNiODdiZmQ3YzU2Y2ZjNGE0YiIsInVzZXJfaWQiOjF9.eZfkpeNVfKLzBY7U0h5gMdTwUnGP3LjRn5g8EIvWlVg"
} 
```

#### Запросы для обновления и проверки JWT-токена

- Обновить JWT-токен:

```POST /api/v1/jwt/refresh/```

- Проверить JWT-токен:

```POST /api/v1/jwt/verify/```

Если ваш токен утрачен, украден или каким-то иным образом скомпрометирован, вам понадобится отключить его и получить новый. Для этого отправьте POST-запрос на тот же адрес ```/api/v1/jwt/create/```, а в теле запроса в поле ```refresh``` передайте refresh-токен.

#### Передача токена в запросах к API

При отправке запроса токен необходимо передавать в заголовке ```Authorization```:```Bearer <токен>```.

#### Примеры запросов к API

- Создание поста:

```
POST /api/v1/posts/
```

в body
{
"text": "string",
"image": "string",
"group": 0
}

- Обновление поста:

```
PUT /api/v1/posts/{id}/
```

в body
{
"text": "string",
"image": "string",
"group": 0
}

- Частичное обновление поста:

```
PATCH /api/v1/posts/{id}/
```

в body
{
"text": "string",
"image": "string",
"group": 0
}

- Удаление поста:

```
DEL /api/v1/posts/{id}/
```

- Подписка пользователя от имени которого сделан запрос на пользователя, переданного в теле запроса:

```
GET /api/v1/follow/
```

***

### Автор

Артём Мухин 
