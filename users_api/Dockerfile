# Базовый образ Python 3.12 slim (минимальный размер)
FROM python:3.12-slim

# Рабочая директория внутри контейнера
WORKDIR /app

# Установка системных зависимостей
RUN apt-get update && apt-get install -y \
    gcc \                    
    postgresql-client \     
    git \                    
    curl \                  
    && rm -rf /var/lib/apt/lists/*

# Обновление pip и установочных утилит
RUN pip install --no-cache-dir --upgrade pip setuptools wheel

# Копирование зависимостей
COPY requirements.txt .

# Установка Python зависимостей
RUN pip install --no-cache-dir -r requirements.txt

# Копирование проекта
COPY . .

# Открытие порта 8000
EXPOSE 8000

# Команда запуска приложения
CMD ["sh", "-c", "alembic upgrade head && python -m src.main"]