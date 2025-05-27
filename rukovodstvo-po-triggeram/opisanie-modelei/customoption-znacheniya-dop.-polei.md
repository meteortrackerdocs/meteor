# CustomOption - Значения доп. полей

## Поля

| Ключ              | Тип            | Название                            | Описание |
| ----------------- | -------------- | ----------------------------------- | -------- |
| id                | integer        | ID                                  |          |
| symbol            | string \| null | Код                                 |          |
| value             | string         | Значение                            |          |
| custom\_field\_id | integer        | ID доп. поля                        |          |
| default\_value    | boolean        | Значение по умолчанию для доп. поля |          |

## Методы

* json - JSON.parse(value)

## Фильтры

* by\_cf(custom\_field: CustomField | Symbol | integer) - Выбрать значения для указанного доп. поля
