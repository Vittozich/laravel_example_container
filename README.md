My docker example for the local laravel + react (or other frontend library) projects.

### `OCTOBER 2020`

### `difficulty level: 2 of 10`

# Components: 

- [php:7.4-fpm-alpine](https://registry.hub.docker.com/_/php) (build)
- [mysql:8](https://registry.hub.docker.com/_/mysql) (image)
- [nginx:stable-alpine](https://hub.docker.com/_/nginx) (image)
- [phpmyadmin/phpmyadmin](https://registry.hub.docker.com/r/phpmyadmin/phpmyadmin) (image)
- [composer:latest](https://registry.hub.docker.com/_/composer) (image)
- [library/node](https://registry.hub.docker.com/_/node) (image, npm)

# `EN`:

# commands:


<hr/>

# notes:


<hr/>


# `RU`:


# Команды:

- `docker-compose build && docker-compose up -d` - создание контейнера 
(его запуск и по этой команде можно пересоздавать(после изменений))

- `docker-compose up -d --build` - другая версия той же команды 
- `docker-compose down` - удаляет контейнеры

<hr/>

# Пометки:

## Установки после клонирования репозитория:

 - копировать `.env.example` в `.env`
 - Если папки не создались - создать папки `mysql` и `src`
 - Проверить работоспособность контейнера можно создав файл по пути `src/public/index.php` (написать там что-то) и запустив в браузере `localhost/`
 - Для использования данной сборки контейнеров на боевом сервере её нужно немного переконфигурировать

## По работе проекта:

- Возможности общего шаблона будут дополнены после проверки его на всех моих проектах (дополнительные либы для php и дополнительные контейнеры (типо phpmyadmin))
- Данный контейнер собирается, как группа контейнеров, которые описаны в `docker-compose.yml`
- Код фреймворка (Laravel) находится в папке `src` и `.gitignore` игнорирует то, 
что внутри, так как внутри данной папки - репозиторий `git` фреймворка (как проекта)
- В данной сборке используется `nginx`, но можно использовать и настроить `apache` -
механизм не будет отличаться, при обновлении файлов внутри `src` не нужно перезапускать контейнеры.

## Конфигурация образа в отдельном файле:

- Вместо `image` в `docker-compose.yml` используется синтаксис `build` и внутри `build:` 
2 переменные `context` - где этот файл искать (`./php`) и `dockerfile` - название докерфайла. (лучше это сделать в отдельной папке)

## Конфигурация nginx:

- Создается отдельный файл конфигурации в папке `./nginx` с названием `default.conf`  -
 данные об этом указываются в настройке контейнера в `docker-compose.yml` в настройках nginx в `volumes`

## Работа с composer контейнером:

- После билда этот контейнер в состоянии отключенного.
- Выполнять команды для composer нужно с префиксом `--rm` - так как composer создает команду, по выполнении которой - команда должна быть удалена. 
Иначе будет создан ещё один контейнер. Пример - узнать версию `docker-compose run --rm composer -V`

## Работа с npm контейнером:

- Так же с префиксом `--rm` выполнять команды

## Работа с artisan контейнером:

- Так же с префиксом `--rm` выполнять команды
- Условие - проект должен лежать в папке src (без laravel проекта контейнер будет создан, но не будет работать, будет выдавать ошибку)
- пример узнать версию `docker-compose run --rm artisan -V` 

<hr/>