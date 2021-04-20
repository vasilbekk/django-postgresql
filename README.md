# django-postgresql
Инструкция по подключении базы данных PostgreSQL к веб-фреймворку Django.

## Установка необходимых утилит для Ubuntu

```
$ sudo apt-get install postgresql
```

## Запуск и настройка PostgreSQL

❗ В символы `<>` заключены значения, которые нужно вставить вместо данных символов.

Открываем консоль PostgreSQL
```
$ sudo -u postgres psql postgres
```
Задаем пароль администратора базы данных
```
\password postgres
```
Создаем и настраиваем пользователя при помощи которого Django будет соединяться с базой данных. Также укажем несколько полезных настроек. Временную зону можете указать свою, например `UTC`
```
create user <username> with password '<password>';
alter role <username> set client_encoding to 'utf8';
alter role <username> set default_transaction_isolation to 'read committed';
alter role <username> set timezone to 'Europe/Moscow';
```
Созаём базу данных нашего проекта
```
create database <project_db> owner <username>;
```
Можем выходить из консоли
```
\q
```

## Установка бэкэнда и настройка Django
Устанавливаем бэкэнд для работы Django с PostgreSQL 
```
pip install psycopg2
```
Настраиваем раздел `DATABASES` в файле настроек проекта `settings.py`
```
'ENGINE': 'django.db.backends.postgresql_psycopg2',
'NAME': '<project_db>',
'USER' : '<username>',
'PASSWORD' : '<password>',
'HOST' : '127.0.0.1',
'PORT' : 5432
```

