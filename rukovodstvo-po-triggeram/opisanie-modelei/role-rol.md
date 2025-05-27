# Role - Роль

## Поля

| Ключ        | Тип                    | Название           | Описание |
| ----------- | ---------------------- | ------------------ | -------- |
| id          | integer                | ID                 |          |
| symbol      | string \| null         | Код                |          |
| name        | string                 | Название           |          |
| builtin     | integer                | ID системных ролей |          |
| type        | 'Role' \| 'GlobalRole' | Тип роли           |          |
| permissions | string\[]              | Список прав роли   |          |

## Методы

* builtin? - проверка что роль системная
* member? - проверка что роль проектная (не системная)
* has\_permission?(permission) - роль имеет право permission
* allowed\_to?(action) - проверка что у роли есть право на действие action

## Статические методы

* non\_member: Role - возвращает системную роль "Non member"
* anonymous: Role - возвращает системную роль "Anonymous"
* in\_new\_project: Role - возвращает роль назначаемую пользователю при создании проекта из настроек системы
* by\_permission(permission): Role\[] - коллекция Ролей у которых есть право permission
* givable: Role\[] - коллекция назначаемых в проектах ролей
