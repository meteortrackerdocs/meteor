# Project - Проект

## Поля

| Ключ         | Тип                                                                                       | Название                   | Описание |
| ------------ | ----------------------------------------------------------------------------------------- | -------------------------- | -------- |
| id           | integer                                                                                   | ID                         |          |
| name         | string                                                                                    | Наименование               |          |
| description  | string                                                                                    | Описание проекта           |          |
| active       | boolean                                                                                   | Активный/Архивный проект   |          |
| public       | boolean                                                                                   | Публичный/Приватный проект |          |
| templated    | boolean                                                                                   | Шаблонный проект           |          |
| identifier   | string                                                                                    | Строковый идентификатор    |          |
| status\_code | enum {on\_track: 0,at\_risk: 1,off\_track: 2,not\_started: 3,finished: 4,discontinued: 5} | Код статуса проекта        |          |

## Cвязи

* parent: Project | null - родительский проект
