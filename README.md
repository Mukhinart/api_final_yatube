# api_final
### _Описание_
API для проекта Yatube (Социальная сеть блогеров).
У неаутентифицированных пользователей доступ к API только на чтение (за исключением эндпоинта ```/follow/```).
Аутентифицированным пользователям разрешено изменение и удаление своего контента; в остальных случаях доступ предоставляется только для чтения.
### _Технологии_
![Python](https://img.shields.io/badge/python-3670A0?style=for-the-badge&logo=python&logoColor=ffdd54)
![DjangoREST](https://img.shields.io/badge/DJANGO-REST-ff1709?style=for-the-badge&logo=django&logoColor=white&color=ff1709&labelColor=gray)
![JWT](https://img.shields.io/badge/JWT-black?style=for-the-badge&logo=JSON%20web%20tokens)
### _Инструкция по запуску проекта:_
- Склонируйте проект из репозитория
- Установите и активируйте виртуальное окружение
```sh
python -m venv venv 
source venv/Scripts/activate
``` 
- Установите зависимости из файла requirements.txt
```sh
pip install -r requirements.txt
``` 
- Выполните миграции в папке с файлом manage.py:
```sh
python manage.py migrate
```
- В папке с файлом manage.py выполните команду:
```sh
python manage.py runserver
```
***
### Примеры использования:
Для доступа к API необходимо получить токен: 
- Нужно выполнить POST-запрос с полями 'username' и 'password'.
```
localhost:8000/api/v1/token/
```
API вернет JWT-токен
- Передав токен* можно будет обращаться к методам, например: 
```
/api/v1/posts/ (GET, POST, PUT, PATCH, DELETE)
```
*При отправке запроса передавайте токен в заголовке Authorization: Bearer <токен>
### Автор
Артём Мухин 
