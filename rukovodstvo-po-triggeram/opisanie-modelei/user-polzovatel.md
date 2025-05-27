# User - Пользователь

## Поля

| Ключ      | Тип     | Название            | Описание                                 |
| --------- | ------- | ------------------- | ---------------------------------------- |
| id        | integer | ID                  |                                          |
| login     | string  | Логин               |                                          |
| firstname | string  | Имя                 |                                          |
| lastname  | string  | Фамилия             |                                          |
| mail      | string  | Почта               |                                          |
| name      | string  | Форматированное имя | Формат определяется в настройках системы |

## Методы

* pref - настройки пользователя
*   in\_group?(group: Group | Symbol | string | integer) - проверка что пользователь состоит в группе group. \`\`\`ruby user.in\_group?(1) user.in\_group?("Group name") user.in\_group?(:group\_123) user.in\_group?(Group.find(123))

    ```
    ```
*   has\_role\_in\_project?(role: Symbol | string | integer, project: Project | string | integer) - является ли пользователь участников проекта (project) с ролью (role) \`\`\`ruby user.has\_role\_in\_project?(:member, 'demo-project') user.has\_role\_in\_project?(2, 4) user.has\_role\_in\_project?('Member', Project.find('demo-project'))

    ```
    ```
* allowed\_to?(action, context, global: false) - проверка прав на действие action в контексте context (проект или глобальный)
* allowed\_to\_globally?(action) - проверка прав на глобальное действие
* allowed\_to\_in\_project?(action, project) - проверка прав на действие в рамках проекта

## Фильтры

* blocked - выбрать заблокированных пользователей
* not\_blocked - выбрать не заблокированных пользователей
* admin - выбрать администраторов
* like(query) - поиск по ФИО, login, email
* visible(user = ::User.current) - выбрать пользователей видимых для тек. пользователя или произвольного пользователя

## Статические методы

* current - текущий авторизованный пользователей
* system - системный пользователь
