# JSONP

**JSONP** - протокол обмена данными(JSON), созданый для обхода ограничений **SOP**. Используюет возможность тега `<script>` запрашивать данные кросс-доменно.  

## Механизм работы

При вызове передается в качестве параметра название коллбека, то есть функции, которая должна обработать возвращенный **JSON**.  
`http://example.com/user/123?jsonp=parseResponse`  
В итоге вернется не **JSON**, а **JS** вида:  
`parseResponse({"username": "test", "id": 123, ...})`

Соответственно на странице должен быть определен глобально обработчик `parseResponse`.

Опасность заключается в том, что атакующий может разместить у себя на странице вызов метода с передачей в свой обработчик, из-за чего у пользователя зашедшего на ресурс атакующего утекут данные. По сути поддержка **JSONP** открывает прямой путь к **XSSI**.  

## Защита

Не использовать **JSONP**. Совсем. **JSONP** был в до**CORS**овые времена и сейчас нет ни одной причины использовать его, а не **CORS**.

[← Назад](../README.md)
