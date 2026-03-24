# API Tests: Wishlist Project

Тестовая коллекция для проверки API сервиса управления списками желаний.

## Инструменты
- Postman
- SOAP UI

## Быстрый старт

### 1. Импорт в Postman
1. Открыть Postman
2. Нажать Import - Выбрать файл `postman/Wishlist_API_Collection.json`
3. Импортировать окружение: `postman/Wishlist_API_Environment.json`
4. Выбрать импортированное окружение в правом верхнем углу

### 2. Запуск тестов
1. Открыть коллекцию Wishlist API Tests
2. Нажать Run collection
3. Выбрать окружение
4. Нажать Run Wishlist API Tests

## Результаты тестирования

### Пройденные тесты: 20/22 (90%)

Общая статистика:
- All tests: 22
- Passed: 20
- Failed: 2
- Errors: 0
- Duration: ~2.5s

### Пройденные сценарии:

#### Authentication (3/3)
- Register New User
- Login
- Login - Negative (Wrong Password)

#### WishLists CRUD (6/6)
- Create Wishlist
- Get All WishLists
- Get Wishlist by ID
- Update Wishlist
- Delete Wishlist
- Create Wishlist - No Auth (Negative)

#### Gifts (3/5)
- Get Gifts from Wishlist
- Reserve Gift
- Add Gift - Missing Name (Negative)
- Add Gift - Negative Price (Negative)
- Add Gift to Wishlist (401 Unauthorized)

### Найденные проблемы (2/22)

| Тест | Ожидаемый результат | Фактический | Статус |
|------|---------------------|-------------|--------|
| Add Gift to Wishlist | 200/201 Created | 401 Unauthorized | Failed |
| Response has gift data | Property 'id' exists | 401 error object | Failed |

### Анализ проблем:

Проблема: При добавлении подарка в список желаний API возвращает 401 Unauthorized, хотя:
- Токен успешно получен при авторизации
- Операции с Wishlist работают корректно
- Токен передаётся в заголовке Authorization

Возможные причины:
1. API endpoint `/api/gifts/wishlist/{id}` требует дополнительных прав
2. Токен истекает между запросами
3. Ошибка в конфигурации API

## Покрытие тестами

### Позитивные тесты:
- Регистрация и авторизация пользователя
- Получение JWT токена
- CRUD операции со списками желаний
- Получение подарков из списка

### Негативные тесты:
- Вход с неверным паролем (401/403)
- Создание списка без авторизации (401/403)
- Добавление подарка без обязательных полей (400/403)
- Добавление подарка с отрицательной ценой (400/403)
