FROM python:3.11-slim

WORKDIR /app

# Копируем requirements.txt первым делом (для кэширования)
COPY requirements.txt .

# Устанавливаем зависимости
RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir -r requirements.txt

# Копируем остальные файлы
COPY . .

# Создаём пользователя
RUN adduser --disabled-password --gecos '' appuser && \
    chown -R appuser:appuser /app
USER appuser

# Определяем открытый порт
EXPOSE 8000

# Запуск через Flask
CMD ["flask", "run", "--host=0.0.0.0", "--port=8000"]
