# Схема базы данных NoteHub

## Сущности

В MVP используются две таблицы:

- users — пользователи системы
- notes — заметки

## Связь

Один пользователь может создать много заметок.
Одна заметка принадлежит только одному пользователю.

```text
users 1 ──── * notes
```

## Таблица users

| Поле | Тип | Ограничения | Описание |
|---|---|---|---|
| id | INTEGER | PRIMARY KEY | Уникальный ID |
| username | VARCHAR(50) | UNIQUE, NOT NULL | Имя пользователя |
| email | VARCHAR(120) | UNIQUE, NOT NULL | Email |
| password_hash | VARCHAR(255) | NOT NULL | Хеш пароля |
| role | VARCHAR(10) | NOT NULL, DEFAULT user | user или admin |
| bio | TEXT | NULL | Описание профиля |
| created_at | DATETIME | NOT NULL | Дата регистрации |

## Таблица notes

| Поле | Тип | Ограничения | Описание |
|---|---|---|---|
| id | INTEGER | PRIMARY KEY | Уникальный ID |
| title | VARCHAR(150) | NOT NULL | Заголовок |
| content | TEXT | NOT NULL | Текст заметки |
| category | VARCHAR(50) | NULL | Категория |
| deadline | DATE | NULL | Дедлайн |
| is_public | BOOLEAN | NOT NULL, DEFAULT FALSE | Личная или публичная |
| author_id | INTEGER | NOT NULL, FK users.id | Автор |
| created_at | DATETIME | NOT NULL | Дата создания |
| updated_at | DATETIME | NOT NULL | Дата изменения |

## Бизнес-правила

1. Email должен быть уникальным.
2. Имя пользователя должно быть уникальным.
3. Пароль хранится только в хешированном виде.
4. Новый пользователь получает роль user.
5. Заметка всегда привязана к автору.
6. Личная заметка доступна только автору и администратору.
7. Публичная заметка доступна всем авторизованным пользователям.
8. При удалении пользователя его заметки также удаляются.