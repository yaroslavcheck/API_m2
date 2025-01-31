# API платежной системы

## Базовый URL  
```
https://m2cerber.pythonanywhere.com/bot_api/
```

## 1. Создание платежа
**POST** `/new_payment/`

### Тело запроса:
```json
{
  "payment_id": "1234",
  "payment_sum": 200,
  "payment_link": "https://m10.com/...",
  "payment_recv": "05039201",
  "status": "pending",
  "callback_url": "https://webhook.com/...",
  "merch_id": "1",
  "user_email": "test@gmail.com",
  "create_time": "2024-09-28 14:30:00"
}
```

### Ответ:
```json
{
  "payment_id": "1234",
  "status": "pending"
}
```

## 2. Получение статуса платежа
**POST** `/get_status/`

### Тело запроса:
```json
{
  "payment_id": "1234",
  "status": "pending"
}
```

### Ответ:
```json
{
  "payment_id": "1234",
  "status": "pending"/"confirm"/"cancel"
}
```

## 3. Получение баланса
**GET** `/get_balance/`

### Параметры:
- `merch_id` (обязательный)
- `callback_url` (опционально)

### Ответ:
```json
{
  "canceled": 350,
  "confirm": 2000,
  "pending": 1500
}
```

## 4. Подпись запросов (Signature)
Для всех запросов, кроме `/get_balance/`:
```
Signature = payment_id + secret_key + status + payment_sum
```

Для `/get_balance/`:
```
Signature = payment_id + secret_key
```

## Ошибки и коды ответов
| Код | Описание |
|----|-----------|
| `200 OK` | Запрос выполнен успешно |
| `400 Bad Request` | Ошибка в переданных данных |
| `401 Unauthorized` | Ошибка подписи (Signature) |
| `404 Not Found` | Ресурс не найден |
| `500 Internal Server Error` | Ошибка сервера |

