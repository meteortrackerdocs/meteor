# Примеры валидаторов и условий переходов

## Запретить создавать эпики с одинаковым названием в рамках одного проекта

```ruby
# Проверочное условие (condition_script)
# если тема задачи зименилась и тип задачи Эпик
self.subject_changed? && self.type_sym == :epic

# Действие
dublicate_exists = Person.where(subject: self.subject, project_id: self.project_id)
.where.not(id: self.id)
.exists?

show_error "В проекте '#{self.project.name}' уже есть Эпик с темой #{self.subject}" if dublicate_exists

```

## Запретить редактирование эпиков пользователям, которые не состоят в группе

```ruby
# 1. Проверочное условие (condition_script)
# Если задача с типом Эпик и пользователь не имеет роли Администратора проекта
self.type_sym == :epic && !self.has_role_in_project(:project_admin, self.project_id )

# 2. Действие: вывод ошибки
show_error "Запрешено редактирование Эпика"

```
