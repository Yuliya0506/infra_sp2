# Проект infra_sp2
## Описание
Данный проект является проектом учебного курса Яндекс Практикум по специальности Python-разработчик.

Проект собирает отзывы (Review) пользователей на произведения (Titles). Произведения делятся на категории: «Книги», «Фильмы», «Музыка». Список категорий (Category) может быть расширен администратором (например, можно добавить категорию «Изобразительное искусство» или «Ювелирка»).
Сами произведения в YaMDb не хранятся, здесь нельзя посмотреть фильм или послушать музыку.
В каждой категории есть произведения: книги, фильмы или музыка. Например, в категории «Книги» могут быть произведения «Винни-Пух и все-все-все» и «Марсианские хроники», а в категории «Музыка» — песня «Давеча» группы «Насекомые» и вторая сюита Баха.
Произведению может быть присвоен жанр (Genre) из списка предустановленных (например, «Сказка», «Рок» или «Артхаус»). Новые жанры может создавать только администратор.
Благодарные или возмущённые пользователи оставляют к произведениям текстовые отзывы (Review) и ставят произведению оценку в диапазоне от одного до десяти (целое число); из пользовательских оценок формируется усреднённая оценка произведения — рейтинг (целое число). На одно произведение пользователь может оставить только один отзыв.
## Установка
Склонируйте проект по адресу https://github.com/Yuliya0506/api_yamdb-1.git

* Создайте файл infra_sp2/infra/.env
* Заполните его данными по образцу:

DB_ENGINE=django.db.backends.postgresql # указываем, что работаем с postgresql
DB_NAME=postgres # имя базы данных
POSTGRES_USER=postgres # логин для подключения к базе данных
POSTGRES_PASSWORD=postgres1 # пароль для подключения к БД (установите свой)
DB_HOST=db # название сервиса (контейнера)
DB_PORT=5432 # порт для подключения к БД
SECRET_KEY = 'p&l%385148kslhtyn^##a1)ilz@4zqj=rq&agdol^##zgl9(vs'

* Установите Docker, соответствующий вашей операционной системе
* Запустите Docker
* Откройте командную строку вашей операционной системы.
* Перейдите в директорию проекта infra_sp2/infra/

## В командной строке выполните команды:
* Команда для сборки образов и запуска контейнеров:
docker-compose up -d --build
* Выполнить миграции:
docker-compose exec web python manage.py migrate
* Копировать статические файлы в директорию static, медиа файлы в директорию media:
docker-compose exec web python manage.py collectstatic --no-input
* Создать суперпользователя:
docker-compose exec web python manage.py createsuperuser

## Загрузка тестовых данных
В репозитории, в директории /api_yamdb/static/data, находятся несколько файлов в формате csv с контентом для ресурсов Users, Titles, Categories, Genres, Review и Comments.
Залить данные из файлов csv в БД можно, импортировав данные командой: python manage.py import_csv

## Примеры
Пользователь аутентифицируется посредством сервиса Simple JWT.
* Получите код подтверждения регистрации.
* Отправьте POST запрос с именем пользователя и e-mail на эндпойнт:

http://127.0.0.1:8000/api/v1/auth/signup/

* Получите токен для доступа к функциям сервиса проекта. 
Отправьте POST запрос с именем пользователя и полученным по e-mail кодом подтвреждения на эндпойнт:

http://127.0.0.1:8000/api/v1/auth/token/

* Можно заполнить пустые поля в своем профайле, отправив PATCH запрос на эндпойнт:

http://127.0.0.1:8000/api/v1/users/me/

* Получение списка произведений GET запрос:

http://127.0.0.1:8000/api/v1/titles/

* Получение информации о произведении GET запрос:

http://127.0.0.1:8000/api/v1/titles/{titles_id}/

* Создать отзыв о произведении POST запрос:

http://127.0.0.1:8000/api/v1/titles/{title_id}/reviews/

### В проекте использованы технологии:
- Python
- Django
- Django REST Framework
- Simple JWT
- Docker
- Postgres
- Gunicorn
- Nginx

### Проект выполнила студентка 34 когорты Яндекс Практикума:
Юлия Галиева     https://github.com/Yuliya0506