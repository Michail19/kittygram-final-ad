# Базовый образ
FROM python:3.11-slim

# Переменные среды
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Рабочая директория
WORKDIR /app

# Системные зависимости (нужны для psycopg2 и сборки пакетов)
RUN apt-get update && apt-get install -y \
    gcc \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*

# Копируем зависимости
COPY requirements.txt .

# Устанавливаем зависимости
RUN pip install --upgrade pip && \
    pip install -r requirements.txt

# Копируем проект
COPY . .

# Команда запуска (для production через gunicorn)
CMD ["gunicorn", "kittygram_backend.wsgi:application", "--bind", "0.0.0.0:8000"]
