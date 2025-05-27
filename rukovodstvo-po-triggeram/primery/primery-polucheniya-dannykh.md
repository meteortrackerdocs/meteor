# Примеры получения данных

## Получение текущего пользователя

```ruby
User.current
# Получение полного имени тек. пользователя
User.current.name
```

## Проверка что текущий пользователь находится в конкретной группе

in\_group?(group: Group | Symbol | string | integer) - проверка что пользователь состоит в группе group

```ruby
# 1. Проверка по id группы
user.in_group?(1)
# 2. Проверка по названию группы
user.in_group?("Group name")
# 3. Проверка по коду группы
user.in_group?(:group_123)
# 4. Проверка по объекту группы
user.in_group?(Group.find(123))
```

## Проверка что текущий пользователь является участником проекта с определенной ролью

has\_role\_in\_project?(role: Symbol | string | integer, project: Project | string | integer) - является ли пользователь участников проекта (project) с ролью (role)

```ruby
user.has_role_in_project?(:member, 'demo-project')
user.has_role_in_project?(2, 4)
user.has_role_in_project?('Member', Project.find('demo-project'))
```

## Получение подзадач

```ruby
# 1. Подзадачи первого уровня
# 1.1. Получение моделей подзадач
self.children
# 1.2. Получение IDs подзадач
self.child_ids

# 2. Получение всех подзадач 
# 2.1. Получение моделей
self.descendants
# 2.2. Получение IDs
self.descendant_ids


```

## Получение связей

```ruby
# получение и обработка
work_package.relations.count
work_package.relations.visible.count
work_package.relations.blocks.count
work_package.relations.relates.each { ... }
```

## Получение родителя / родителей

```ruby
# 1. Получение родительской задачи
self.parent
# 2. Получение всей цепочки родительских задач
self.ancestors
```

## Получить статус, в котором была задача до перехода в текущий статус

```ruby
# ID предыдущего статуса
old_status_id = self.status_id_was
# Предыдущий статус задачи
old_stutus = Status.find(self.status_id_was)
```

## Метод, которые преобразует объект в json формат

```ruby
# 1. Generate JSON 
json_object = JSON.generate({ current_user: User.current.name })
# 2. Parse JSON 
object = JSON.parse!(json_object)

```

## Получить список полей, которые изменились в момент выполнения триггера

```ruby
# Список измененных полей (Спистемных + доп. полей)
changed_fields = self.all_changes

```
