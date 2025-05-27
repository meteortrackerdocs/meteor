# Примеры изменения данных

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

## Создание задачи/подзадачи

```ruby
# 1. Создание подзадачи в этом же проекте и без отправки уведомления
subtask = WorkPackage.create_perform!(subject: "test create subtask #{DateTime.now}", project_id: self.project_id, parent_id: self.id, send_notifications: false)
# 2. Создание копии задачи и связи с исходной
copy_wp = ... # TODO
self.add_relation(to: copy_wp, relation_type: 'relates')  

```

## Назначить исполнителя задачи в зависимости от типа задачи

```ruby
# Если код типа задачи 'bug' - исполнитель задачи устанавливается 'developer@u-meteor.ru'
self.assigned_to = User.where(login: 'developer@u-meteor.ru').first if self.type_sym == :bug
```

## При назначении любого исполнителя для задачи - добавлять конкретный спринт, а при обнулении - убирать

```ruby
# Проверочное условие (condition_script)
self.assigned_to_changed?

# Действие
if self.assigned_to.present? then
 # если исполнитель указан
  self.verion = Version.find(123)
else
  self.version = nil  
end 
```

## Переоткрыть задачу если в ней добавился комментарий

```ruby
# Проверочное условие (condition_script)
# TODO

# Действие
self.status = Status.default
```

## Назначение тега при создании задачи

```ruby
# Поиск тега по названию
tag = Tag.where(name: 'My tag').first

# Добавление к задаче
self.tags.push(tag)

```

## Автоматическое заполнение данных в доп. полях

```ruby
# Получение значения заказчика по умолчанию из доп поля проекта задачи
customer_code = self.project.cf_customer_option.json['code']

# Установка поля заказчик значением по умолчанию
self.cf_customer = CustomOption.by_cf(:customer).where(symbol: customer_code).first

```
