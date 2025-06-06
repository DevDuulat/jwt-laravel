# JWT Аутентификация в Laravel 10+


## Установка

1. Клонируйте репозиторий:

```bash
git clone https://github.com/DevDuulat/jwt-laravel.git
cd laravel-jwt-auth
````

2. Установите зависимости:

```bash
composer install
```

3. Скопируйте `.env` и сгенерируйте ключ:

```bash
cp .env.example .env
php artisan key:generate
```

4. Установите секрет JWT:

```bash
php artisan jwt:secret
```

5. Установите время жизни токена в `.env`:

```env
JWT_TTL=30
```

6. Настройте подключение к базе данных в `.env`, затем выполните миграции:

```bash
php artisan migrate:fresh
```

---

## Запуск проекта

```bash
php artisan serve
```

Проект будет доступен по адресу:
[http://localhost:8000](http://localhost:8000)

---

## API Методы

### Login

```bash
curl -X POST http://localhost:8000/api/login \
-H "Content-Type: application/json" \
-d '{"email": "test@example.com", "password": "password123"}'
```

**Ответ:**

```json
{
  "access_token": "eyJ0eXAiOiJKV1Qi...",
  "token_type": "bearer",
  "expires_in": 1800
}
```

---

### Logout

```bash
curl -X POST http://localhost:8000/api/logout \
-H "Authorization: Bearer ваш_токен" \
-H "Content-Type: application/json"
```

**Ответ:**

```json
{
  "message": "Successfully logged out"
}
```

---

### Refresh

```bash
curl -X POST http://localhost:8000/api/refresh \
-H "Authorization: Bearer старый_токен" \
-H "Content-Type: application/json"
```

**Ответ:**

```json
{
  "access_token": "новый_токен",
  "token_type": "bearer",
  "expires_in": 1800
}
```

---


---

## Тестовые данные

```json
{
  "email": "test@example.com",
  "password": "password123"
}
```

---

## Полезные команды

```bash
# Очистить и пересоздать базу данных
php artisan migrate:fresh --seed

# Сброс кеша конфигурации
php artisan config:clear
php artisan cache:clear
```

```
