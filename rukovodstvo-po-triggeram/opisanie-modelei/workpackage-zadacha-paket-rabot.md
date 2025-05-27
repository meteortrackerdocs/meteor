# WorkPackage - Задача / Пакет работ

## Поля

| Ключ                       | Тип             | Название                                       |
| -------------------------- | --------------- | ---------------------------------------------- |
| id                         | integer         | ID                                             |
| created\_at                | DateTime        | Дата создания                                  |
| updated\_at                | DateTime        | Дата обновления                                |
| status\_updated\_at        | DateTime        | Дата обновления статуса задачи                 |
| subject                    | string          | Тема                                           |
| description                | string \| null  | Описание                                       |
| schedule\_manually         | boolean         | Ручное планирование                            |
| ignore\_non\_working\_days | boolean         | Игнорирование не рабочих дней при планировании |
| start\_date                | date \| null    | Дата начала задачи                             |
| due\_date                  | date \| null    | Дата завершения задачи                         |
| duration                   | integer \| null | Продолжительность задачи в днях                |
| done\_ratio                | integer         | % выполнения задачи                            |
| estimated\_hours           | float \| null   | Запланированное время выполнения               |
| remaining\_hours           | float \| null   | Оставшееся время                               |
| derived\_estimated\_hours  | float \| null   |                                                |
| derived\_remaining\_hours  | float \| null   |                                                |
| story\_points              | integer \| null | Оценка в SP                                    |
| external\_id               | string \| null  | Внешний ID                                     |
| type\_id                   | integer         | Тип задачи                                     |
| project\_id                | integer         | Проект                                         |
| status\_id                 | integer         | Статус                                         |
| status\_sym                | symbol          | Код статуса                                    |
| category\_id               | integer \| null | Категория                                      |
| priority\_id               | integer         | Приоритет                                      |
| version\_id                | integer \| null | Версия/Спринт                                  |
| author\_id                 | integer         | Автор                                          |
| assigned\_to\_id           | integer \| null | Исполнитель                                    |
| responsible\_id            | integer \| null | Ответственный                                  |
| parent\_id                 | integer \| null | Родительская задача                            |

## Связи

* type: Type - тип задачи
* type\_sym: Symbol - код типа задачи
* project: Project - проект
* status: Status - статус задачи
* status\_sym: Symbol - код типа задачи
* category: Category | null - категория задачи
* priority: IssuePriority - приоритет задачи
* version: Version | null - версия/Спринт задачи
* author: User - автор задачи
* assigned\_to: User | null - исполнитель задачи
* responsible: User | null - ответственный задачи
* parent: WorkPackage | null - родительская задача
* time\_entries: TimeEntry\[] - записи времени по задаче
* relations: Relation\[] - связи с задачами

## Дополнительные поля

Дополнительные поля настраиваются в рамках Типа задачи и поэтому требуется проверять наличие доп. поля в задаче во избежание ошибок:

```ruby
# Проверка что в задаче доступно допю поле
 respond_to?(:cf_my_field)
```

### **Примитивные доп. поля**

К ним относятся следующие типы:

* Целое число (integer)
* Текст (string)
* Длинный текст (string)
* Дробное число (float)
* Дата
* Дата/Время
* Логическое значение (boolean)

```ruby
# Обращение к доп полю по Symbol: cf_<symbol>
self.cf_string_field = 'test' # string_field - символьный код доп. поля
# Обращение к доп полю по ID: 
self.cf_99  = true         # 99 - это ID кастомного поля


```

### **Списочные доп. поля**

К ним относятся следующие типы:

* Пользователь (User)
* Версия/Спринт (Version)
* Список (CustomOption)

```ruby
# Получение списка доступных значений доп поля по коду доп поля
options = CustomOption.by_cf(:my_field) 
# Получение доступных значений доп поля по ID доп поля
options = CustomOption.by_cf(99) 
# Получение доступных значений доп поля по доп поля
cf = WorkPackageCustomField.find(:my_field)
options = CustomOption.by_cf(cf) 
options = cf.custom_options

# Присвоение конкретного значения доп поля по коду
self.cf_my_field = CustomOption.by_cf(:my_field).where(symbol: 'value_code').first

# Получение значения CustomOption для доп поля задачи
cf_value = self.cf_my_field_option # cf_value: CustomOption

# Работа с множественными полями
add_value =  CustomOption.by_cf(:my_field).where(symbol: 'value_code').first
# 1. Добавление значения
self.cf_array_field_add(add_value) 
# 2. Удаление значения
self.cf_array_field_remove(add_value)
# 3. Присвоение массива
self.cf_array_field = <array of CustomOption>

```

## Методы

* \<field>\_changed? - изменилось ли указанное поле
* closed? - задача находится на закрывающем статусе
* blocked? - задача заблокирована другой открытой задачей
* readonly\_status? - задача находится на readonly-статусе
*   overdue? - задача просрочена. \`\`\`ruby !due\_date.nil? && (due\_date < Time.zone.today) && !closed?

    ```
    ```
* milestone? / is\_milestone? - задача имеет тип milestone (Веха)
* duration\_in\_hours(): integer - продолжительность задачи в часах.
* visible?(user: User = User.current) - Доступна задача для данного/тек. пользователя
* visible\_relations(user: User) - Видимые связи для указанного пользователя
* add\_relation - создание связи
* ```ruby
    work_package.add_relation(to_id: 10, relation_type: 'relates', send_notifications: false, description: 'Description')
    work_package.add_relation(to: WorkPackage.find(10), relation_type: 'relates')
  ```

### Методы работы с иерархией задач

* parent: WorkPackage | null - Родительская задача
* children: WorkPackage\[] - подзадачи

## Фильтры

* visible(user: User = User.current) - выбрать задачи видимые для указанного/текущего пользователя
* in\_status(status: Status | integer ) - выбрать задачи находящиеся в указанном статусе
* for\_projects(projects: Project\[]) - выбрать задачи из указанных проектов
* changed\_since(since: DateTime) - выбрать задачи измененные после указанного момента
* with\_status\_open - выбрать задачи находящиеся на открытом статусе
* with\_status\_closed - выбрать задачи находящиеся на закрытом статусе
* with\_limit(limit: integer) - ограничение выборки
* on\_active\_project - выбрать задачи из активных проектов
* with\_author(author: User) - выбрать задачи, автор которых является указанный пользователь
* without\_version - задачи без версии/спринта

## Статические методы

* create\_perform - создание задачи

## Работа со связями между задачами

```ruby
# добавление
work_package.add_relation(to_id: 10, relation_type: 'relates', send_notifications: false, description: 'Description')
work_package.add_relation(to: WorkPackage.find(10), relation_type: 'relates')

# проверка ошибок
> relation = work_package.add_relation(...) 
> relations.errors.any?
> relations.errors.full_messages

# получение и обработка
work_package.relations.count
work_package.relations.visible.count
work_package.relations.blocks.count
work_package.relations.relates.each { ... }

# удаление
work_package.relations.select { |r| r.relation_type == 'blocks' }.each { |r| r.destroy }
```

TODO - не нашел в коде :

:ancestor\_hierarchies, :self\_and\_ancestors, :descendant\_hierarchies,\
:self\_and\_descendants, :root?, :child?, :leaf?, :root, :leaves, :depth, :level, :ancestors,\
:ancestor\_ids, :self\_and\_ancestors\_ids, :child\_ids, :descendants, :self\_and\_descendant\_ids,\
:descendant\_ids, :self\_and\_siblings, :siblings, :sibling\_ids, :parent\_of?, :root\_of?,\
:ancestor\_of?, :descendant\_of?, :child\_of?, :family\_of?, :add\_child
