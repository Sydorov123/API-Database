# Benchmarking SQL Queries API

Цей проєкт розроблений для оцінки продуктивності SQL-запитів до бази даних із різними обсягами даних (1 000, 10 000, 100 000, 1 000 000). Основною метою є аналіз швидкості виконання операцій SELECT, INSERT, UPDATE і DELETE у віддаленій базі даних.

## Системні вимоги

- Python 3.x  
- Бібліотеки `psycopg2` (для підключення до PostgreSQL) і `tabulate` (для виведення таблиць)  
- PostgreSQL-сервер (локальний або віддалений, наприклад, Railway.app)

## Установка

1. **Клонування репозиторію**  
   Завантажте репозиторій до вашої локальної системи:  
   ```bash
   git clone https://github.com/your-username/SQL-Benchmark-API.git
   cd SQL-Benchmark-API
   ```

2. **Встановлення залежностей**  
   Виконайте команду для інсталяції всіх необхідних бібліотек:  
   ```bash
   pip install -r requirements.txt
   ```

3. **Налаштування підключення**  
   Укажіть параметри доступу до вашої бази даних у файлі `config.py` або через змінні середовища.  

   **Приклад налаштувань**:  
   ```python
   DB_HOST = 'your-db-host'  # Наприклад, db1234.railway.app
   DB_PORT = '5432'  # Порт PostgreSQL за замовчуванням
   DB_NAME = 'your-db-name'
   DB_USER = 'your-db-user'
   DB_PASSWORD = 'your-db-password'
   ```

4. **Ініціалізація бази даних**  
   Виконайте SQL-скрипт для створення таблиці `items`:  
   ```sql
   CREATE TABLE items (
       id SERIAL PRIMARY KEY,
       name VARCHAR(100),
       description TEXT,
       price DECIMAL
   );
   ```

## Використання

### Запуск тестів

Виконайте скрипт для вимірювання часу виконання SQL-запитів:  
```bash
python -m app.query_benchmark
```

### Обсяги даних і тестові операції

Скрипт автоматично тестує виконання запитів із такими обсягами записів у таблиці:  
- 1 000  
- 10 000  
- 100 000  
- 1 000 000  

Для кожного обсягу даних виконуються:  
- **SELECT**: Вибірка 1 000 записів  
- **INSERT**: Додавання нових записів  
- **UPDATE**: Оновлення записів  
- **DELETE**: Видалення записів  

### Виведення результатів

Після виконання тестів результати відображаються у вигляді таблиці:  
```
+----------+--------------+--------------+--------------+--------------+
| Records  | Select Time  | Insert Time  | Update Time  | Delete Time  |
+----------+--------------+--------------+--------------+--------------+
| 1000     | 0.01s        | 0.05s        | 0.02s        | 0.04s        |
| 10000    | 0.12s        | 0.45s        | 0.20s        | 0.30s        |
| 100000   | 1.20s        | 5.00s        | 1.50s        | 3.00s        |
+----------+--------------+--------------+--------------+--------------+
```

## Особливості проєкту

- Для демонстрації базової ефективності запитів індекси не використовуються.  
- Паралельне виконання запитів для оптимізації операцій на великих наборах даних.  
- Підтримка підключення до будь-якого PostgreSQL-сервера.  

## Ресурси

Для тестування використовується база PostgreSQL, розгорнута на платформі Railway.app, однак ви можете налаштувати підключення до будь-якого іншого сервера.
