Тестовое задание для Барс. Литвинцев Михаил.
Установка:
1. Скачать репозиторий: git clone https://github.com/Mikhail-Litvintsev/bars-test testCase
2. В папке с проектом выполнить: docker compose build && docker compose up -d
3. Скопировать файл src/.env.example в src/.env
4. В контейнере php (docker compose exec php sh) выполнить команду: composer install. Можно снаружи запустить, находясь в папке src (если композер установлен глобально)ж
5. В контейнере php выполнить: 
    php artisan key:generate
    php artisan migrate
    php artisan optimize
6. При наличии установленного пакета npm, рекомендуется в папке src (снаружи контейнеров) выполнить команду 
    npm install && npm run watch. 
   Если такой возможности нет, то возможно запустить изнутри php контейнера.
7. Eсли у вас защищенные файловые системы (Linux), то выдйте пожалуйста разрешения на ппку с проектом (как минимум на src/storage)

Приложение готово к работе. По умолчанию http://localhost


    
