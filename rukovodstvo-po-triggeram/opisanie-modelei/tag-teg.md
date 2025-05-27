# Tag - Тег

## Поля

| Ключ         | Тип             | Название   | Описание |
| ------------ | --------------- | ---------- | -------- |
| id           | integer         | ID         |          |
| name         | string          | Название   |          |
| color\_id    | integer \| null | Цвет тега  |          |
| author\_id   | integer         | Автор      |          |
| external\_id | string \| null  | Внешний ID |          |

## Cвязи

* color: Color | null - Цвет тега
* author: User - Автор

## Фильтры/Сортировки

* sorted() - сортировка по названию
* for\_project(project: Project | Project\[]) - выбрать теги доступные в указанном проекте
