# Misconfiguration

Уязвимости в следствии некорректной настройки или недостаточно защищенного использования тех или иных технологий.

## CORS

Заголовки **CORS** поддерживают **wildcard**, соответственно ошибка в **wildcard** может привести к тому, что ресурс будет открыт для запросов извне, читай **CSRF**. Особенно опасно использовать `*` по понятным причинам.

### Защита

Использовать **whitelist** и не использовать **wildcard**.

## WebSocket

Спецификация **WebSocket** подразумевает открытие соединение путем **GET** запроса, соответственно **SOP** не запрещает, поэтому при авторизации только по **Cookie** атакующий может со своего сайта открыть соединение с атакуемым сайтом и ловить все сообщения из канала.  

### Защита

1. Открывая соединение передавать токен, полученный по безопасному каналу, аналогично **CSRF**-токену
2. Проверять **origin**, с которого открывается соединение
3. По возможности использовать **wss:**

## PostMessage

Вспоминаем, что при отправке **postMessage** указывается **origin** получателя, при этом доступно значение `*`. Плюс в объекте события `message` есть **origin** отправителя.

Соответственно, если сходу выполняются какие-то действия при получении сообщения, без проверки **origin** отправителя и с использованием данных из `message` - образуется уязвимость. Атакующий может вставить на свою страницу **iframe** передавая нужные данные через **postMessage**, причем хуже результат если внутри **iframe** критичные данные пользователя, загруженные благодаря его авторизованности на атакуемом ресурсе.

Аналогично уязвимость появляется, если ресурс отправляет широковещательные **postMessage** не указывая **origin** заменяя его значением `*`. Опять же атакующий может разместить у себя **iframe** перехватывая все сообщения.

### Защита

Строго определять отправителя и получателя по **whitelist**. Использовать заголовки или **CSP** определяя на каких **origin** может быть ресурс встроен в **iframe**.

[← Назад](../README.md)
