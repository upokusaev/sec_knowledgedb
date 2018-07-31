# Insecure direct object reference

Уязвимость, при которой персональные данные пользователей доступны по прямому запросу, без разграничения доступа.  

## Пример

В некой облачной многопользовательской системе пользователь1 может залить файл в свое персональное пространство, не подразумевая его шеринга. Открыть файл можно по уникальной ссылке.  

При этом пользователь2 по прямой ссылке может открыть тот же файл.  

> Не стоит недооценивать уязвимость, даже если прямые ссылки сложные и содержат высокоэнтропийные идентификаторы. В случае бага в кэше можно допустить утечку.  

## Обнаружение

1. Заводим два аккаунта
2. Заходим под первым и обходим все возможные пути, логируя свои походы
3. Заходим под вторым и повторяем путь по логам

[← Назад](../README.md)