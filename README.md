Тестовое задание для Барс. Литвинцев Михаил.
Установка:
1. Скачать репозиторий:
2. В папке с проектом выполнить: docker compose build && docker compose up -d
3. Скопировать файл src/.env.example в src/.env
4. В контейнере php (docker compose exec php sh) выполнить команду: composer install. Можно снаружи запустить, находясь в папке src (если композер установлен глобально)ж
5. В контейнере php выполнить: 
    php artisan key:generate
    php artisan migrate
    php artisan optimize

После чего приложение готово к работе.


    
