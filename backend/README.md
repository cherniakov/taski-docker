# Запускаем бекэнд на локальной машине

## Создаем окружение: 

1. Перехододим в папку
    cd taski/backend/
2. Создаём виртуальное окружение с python 3.10
    python3 -m venv venv
3. Активируем виртуальное окружение
    source venv/bin/activate
4. Устанавливаем зависимости
    pip install -r requirements.txt

## Запускаем бекэнд:

1. Применяем миграции
    python3 manage.py migrate
2. Создаём суперпользователя
    python manage.py createsuperuser
3. Запустить проекты локально
    python manage.py runserver
4. Переходим по ссылкам:
    http://localhost:8000/admin/
    http://localhost:8000/api

## Собираем Docker-образ

1. Перехододим в папку
    cd taski/backend/

2. Создаём файл Dockerfile
    # Создать образ на основе базового слоя,
    # который содержит файлы ОС и интерпретатор Python 3.10.
    FROM python:3.10

    # Переходим в образе в директорию /app: в ней будем хранить код проекта.
    # Если директории с указанным именем нет, она будет создана. 
    # Название директории может быть любым.
    WORKDIR /app
    # Дальнейшие инструкции будут выполняться в директории /app

    # Скопировать с локального компьютера файл зависимостей
    # в текущую директорию (текущая директория — это /app).
    COPY requirements.txt .

    # Выполнить в текущей директории команду терминала
    # для установки зависимостей.
    RUN pip install -r requirements.txt --no-cache-dir

    # Скопировать всё необходимое содержимое 
    # той директории локального компьютера, где сохранён Dockerfile,
    # в текущую рабочую директорию образа — /app.
    COPY . .

    # При старте контейнера запустить сервер разработки.
    CMD ["python", "manage.py", "runserver", "0:8000"]

3. Создаём файл .dockerignore
    venv
    .git
    .env
    .vscode
    db.sqlite3

4. Выполните сборку образа
    docker build -t taski_backend .

5. Выведите список всех образов
    docker image ls

6. Запуск контейнера
    docker run --name taski_backend_container --rm -p 8000:8000 taski_backend

7. Откройте в браузере страницу http://localhost:8000/api/

8. Выполните миграции в контейнере taski_backend_container:
    docker exec taski_backend_container python manage.py migrate
