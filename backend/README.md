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
    http://localhost:8000/api/