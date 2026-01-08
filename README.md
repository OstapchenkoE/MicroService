# MicroService

## Запуск проекта

```bash
docker-compose up -d
```

## API Документация

### Интерактивная документация

Swagger UI: http://localhost:8000/api/docs

### Основные эндпоинты

#### Здоровье приложения

```
GET /health
```

Проверка статуса приложения.

**Ответ:**

```json
{ "status": "ok" }
```

#### Пользователи

**Регистрация**

```
POST /api/users/
```

Создание нового пользователя.

**Параметры:**

```json
{
  "email": "user@example.com",
  "username": "username",
  "password": "password123"
}
```

**Логин**

```
POST /api/users/login
```

Получение JWT токена.

**Параметры:**

```json
{
  "email": "user@example.com",
  "password": "password123"
}
```

**Ответ:**

```json
{
  "access_token": "eyJ0eXAiOiJKV1QiLCJhbGc...",
  "token_type": "bearer"
}
```

**Получить текущего пользователя**

```
GET /api/users/me
```

Требует аутентификацию (JWT токен в заголовке `Authorization: Bearer <token>`).

**Обновить профиль**

```
PUT /api/users/me
```

Обновление информации о текущем пользователе.

#### Статьи

**Создать статью**

```
POST /api/articles/
```

Требует аутентификацию.

**Параметры:**

```json
{
  "title": "Заголовок статьи",
  "description": "Описание",
  "body": "Содержание статьи"
}
```

**Получить все статьи**

```
GET /api/articles/?skip=0&limit=20
```

Публичный эндпоинт. Поддерживает пагинацию.

**Получить статью по slug**

```
GET /api/articles/{slug}
```

Получение конкретной статьи.

**Обновить статью**

```
PUT /api/articles/{slug}
```

Требует аутентификацию. Может обновлять только автор.

**Удалить статью**

```
DELETE /api/articles/{slug}
```

Требует аутентификацию. Может удалять только автор.

#### Комментарии

**Добавить комментарий**

```
POST /api/articles/{slug}/comments
```

Требует аутентификацию.

**Параметры:**

```json
{
  "body": "Текст комментария"
}
```

**Получить комментарии статьи**

```
GET /api/articles/{slug}/comments?skip=0&limit=20
```

Публичный эндпоинт. Поддерживает пагинацию.

**Удалить комментарий**

```
DELETE /api/articles/{slug}/comments/{comment_id}
```

Требует аутентификацию. Может удалять только автор комментария.
