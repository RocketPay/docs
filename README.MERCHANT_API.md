# CURL API Examples

**Формат запроса**

Все POST-запросы должны содержать json и content-type должен быть указан `application/json`

**Формат ответа**

Ответ содерржи несколько полей:

- `payload` - данные соответствующие запросу
- `status` - статус ответа, см. список статусов ответа

## Account

**`[POST] /api/v1/users` - User Registration**

Принимаемые параметры:

- `email`
- `password`
- `mobile_phone` - TODO

_Request_

```bash
curl 'http://merchant.rocketpay.ru/api/v1/users' \
    -X POST \
    -H 'Content-Type: application/json' \
    -d '{"email": "example@email.com", "password": "password"}'
```

_Response_

```json
{}
```

**`[POST] /api/v1/users/password_reset` - Password reset**

Отправка кода на email или sms

Принимаемые параметры:

- `email`
- `mobile_phone` - TODO

_Request_

```bash
curl 'http://merchant.rocketpay.ru/api/v1/users/password_reset' \
    -X POST \
    -H 'Content-Type: application/json' \
    -d '{"email": "example@email.com"}'
```

или

```bash
curl 'http://merchant.rocketpay.ru/api/v1/users/password_reset' \
    -X POST \
    -H 'Content-Type: application/json' \
    -d '{"mobile_phone": "79154747270"}'
```

_Response_

```json
{}
```

**`[PUT] /api/v1/users/password_reset`**

Если токена 

Принимаемые параметры:

- `code`
- `password`

```bash
curl 'http://merchant.rocketpay.ru/api/v1/users/password_reset' \
    -X PUT \
    -H 'Content-Type: application/json' \
    -d '{
        "code": "877739ce-d368-11e8-8b17-87c00c06382d",
        "password": "password"
    }'
```

_Response_

```json
{}
```

## Tokens

**`[POST] /api/v1/tokens` - Create new Token**

Принимаемые параметры:

- `email`
- `password`
- `mobile_phone` - TODO

```bash
curl 'http://merchant.rocketpay.ru/api/v1/tokens' \
    -X POST \
    -H 'Content-Type: application/json' \
    -d '{"email": "example@email.com", "password": "password"}'
```

_Response_

```json
{}
```

## Merchants

**`[GET] /api/v1/merchants` - Get Merchants**

_Request_

```bash
curl 'http://merchant.rocketpay.ru/api/v1/merchants' \
    -X GET \
    -H 'X-Token: ...'
```

_Response_

```json
{}
```

**`[POST] /api/v1/merchants` - Create merchant**
    
_Request_

```bash
curl 'http://merchant.rocketpay.ru/api/v1/merchants' \
    -X POST \
    -H 'Content-Type: application/json' \
    -H 'X-Token: ...' \
    -d '{"email": "example@email.com", "password": "password"}'
```

_Response_

```json
{}
```

**`[PUT] /api/v1/merchants/{int:merchant_id}` - Update merchant details**

_Request_

```bash
curl 'http://merchant.rocketpay.ru/api/v1/merchants/1' \
    -X PUT \
    -H 'X-Token: ...' \
    -H 'Content-Type: application/json' \
    -d '{"url_website": "https://gocloud.ru"}'
```

_Response_

```json
{}
```

## Reports

Настройка отчетов.
Механизм отправки реестров платежей для проведения сверки.

**`[GET] /api/v1/merchants/{int:merchant_id}/reports`**

Вывод текущих настроек отправки реестров платежей.

*Описание полей ответа*

- `enable`: `integer`. **1** - включено, **0** - выключено.
- `email`: `string`. адрес электронной почты.
- `frequency`: `enum`. **day**, **week**, **month**
- `format`: `enum`. **xml**, **cvs**

_Request_

```bash
curl 'http://merchant.rocketpay.ru/api/v1/merchants/1/reports' \
    -X GET \
    -H 'X-Token: ...'
```

_Response_

```json
{
    "payload": {
        "email": "test@rocketpay.ru",
        "frequency": "day",
        "format": "xml"
    },
    ...
}
```

**`[PUT] /api/v1/merchants/{int:merchant_id}/reports`**

_Request_

```bash
curl 'http://merchant.rocketpay.ru/api/v1/merchants/1/reports' \
    -X PUT \
    -H 'X-Token: ...' \
    -H 'Content-Type: application/json' \
    -d '{"enable": 1}'
```

_Response_

```json
{}
```
