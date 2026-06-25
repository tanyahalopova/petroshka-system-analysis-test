# Задание 2. Проектирование API для экрана партнерских магазинов

## REST API

### Метод
```http
GET /api/v1/partners/stores
```

### Назначение
Возвращает список партнерских магазинов для отображения на экране мобильного приложения.

### Query-параметры

| Параметр | Тип | Обязательный | Описание |
|---|---|---:|---|
| latitude | number | Нет | Широта пользователя |
| longitude | number | Нет | Долгота пользователя |
| city_id | string | Нет | Идентификатор города |
| platform | string | Да | `ios` или `android` |
| app_version | string | Да | Версия приложения |

### Пример запроса
```http
GET /api/v1/partners/stores?city_id=msk&platform=ios&app_version=3.12.0 HTTP/1.1
Host: api.petrushka-zelenaya.ru
Authorization: Bearer <access_token>
Accept: application/json
```

## Пример ответа

```json
{
  "data": [
    {
      "id": "metro",
      "name": "METRO",
      "logo_url": "https://cdn.petrushka-zelenaya.ru/partners/metro/logo.png",
      "delivery": {
        "type": "scheduled",
        "title": "Ближайшая доставка",
        "description": "Сегодня 21:00–23:00",
        "next_delivery_at": "2026-06-24T21:00:00+03:00"
      },
      "external_link": {
        "url": "https://partner.example.com/metro",
        "open_mode": "external_browser"
      },
      "is_available": true,
      "sort_order": 1
    },
    {
      "id": "vkusvill",
      "name": "ВкусВилл",
      "logo_url": "https://cdn.petrushka-zelenaya.ru/partners/vkusvill/logo.png",
      "delivery": {
        "type": "express",
        "title": "Быстрая доставка",
        "description": "От 20 до 60 минут",
        "min_delivery_minutes": 20,
        "max_delivery_minutes": 60
      },
      "external_link": {
        "url": "https://partner.example.com/vkusvill",
        "open_mode": "external_browser"
      },
      "is_available": true,
      "sort_order": 2
    }
  ],
  "meta": {
    "city_id": "msk",
    "generated_at": "2026-06-24T10:00:00+03:00"
  }
}
```

## Описание ключевых полей

| Поле | Тип | Описание |
|---|---|---|
| data | array | Список партнерских магазинов |
| id | string | Уникальный идентификатор партнера |
| name | string | Название магазина |
| logo_url | string | URL логотипа |
| delivery | object | Информация о доставке |
| external_link.url | string | Внешняя ссылка для перехода по карточке |
| external_link.open_mode | string | Способ открытия ссылки |
| is_available | boolean | Доступность партнера пользователю |
| sort_order | integer | Порядок отображения |


## Вопросы к заказчику

1. Показывать ли недоступных в городе партнеров?
2. Скрывать ли партнера при отсутствии слотов доставки?
3. Открывать ссылку во встроенном WebView или внешнем браузере?
4. Нужны ли deeplink в приложение партнера?
5. Как часто обновлять данные о доставке?
6. Нужны ли кэширование и пагинация?
