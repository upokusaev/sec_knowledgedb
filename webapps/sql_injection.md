# SQL injection

Атака, эксплуатирующая приложения с недостаточной фильтрацией пользовательского ввода, используемого в запросах к базе данных.

## Эксплуатация

Рассмотрим примитивный пример, когда пользовательский ввод используется при составлении **SQL**-запроса:  

    entity_id = request.args.get("id")
    response = connector.raw("SELECT * FROM myTable WHERE id=" + entity_id + ";")
    return response

Соответственно найдя уязвимый метод, атакующий может передать, к примеру, вместо ожидаемого `id` часть **SQL** запроса, изменяя исходный:

    GET /dbMethod?id=;%20UNION%20SELECT%20passwd%20FROM%20USERS;%20--%20 HTTP/1.1
    User-Agent: Mozilla/4.0 (compatible; MSIE5.01; Windows NT)
    Host: example.com
    Accept-Language: en-us
    Accept-Encoding: gzip, deflate
    Connection: Keep-Alive

В итоге значение `id` будет равно:  

    1; UNION SELECT * FROM USERS; --

и метод вернет также содержимое таблицы USERS, отбросив остаток запроса, тк он будет закомментирован.

> на самом деле чтобы это сработало нужно чтобы количество полей у обеих таблиц совпадало, но в рамках примера это неважно.

Помимо использования **raw**-запросов, то есть обычных строчных может использоваться **ORM** - программное **API**, представляющее объектный доступ к данным. То есть работа сводится к объектам, а не запросам.

`response = MyData.objects.get(id=user_id).order_by("dt")`

> Вопреки расхожему заблуждению использование ORM не гарантирует отсутствие SQL инъекций, тк может содержать внутри уязвимые инструкции

Для поиска используют перебор параметров в методах, значения **Cookie**, реферер и весь возможный пользовательский ввод, при этом отслеживается аномальное поведение методов:  

* Сообщения о ошибках
* Отсутствие данных в ответе

См [Страница на OWASP](https://www.owasp.org/index.php/SQL_Injection_Prevention_Cheat_Sheet)

## Защита

* Строгая валидация пользовательского ввода, с последующим санитайзингом
* При использовании **ORM** своевременное обновление

## NoSQL

Все аналогично **SQL**-инъекциям.

[← Назад](../README.md)
