# Telegram-уведомления

Документация к Telegram доступна в ресурсе:

[https://core.telegram.org/bots/api#authorizing-your-bot](https://core.telegram.org/bots/api#authorizing-your-bot)

Проверочная ссылка на валидность токена и идентификатора чата telegram:

https://api.telegram.org/\<bot\_token>/channels.getMessages?channel=\<channel\_id>

Проверочная ссылка на валидность токена:

https://api.telegram.org/\<bot\_token>/getme

## Отправка сообщения в telegram-канал при создании задачи

* событие запуска: **При создании**
* Выполнить асинхронный скрипт:

```ruby
bot_token = 'bot<telegram bot token>'
chat_id = <Chat Id>

escape_telegram_md = ->(s) { s.gsub( /([_*\[\]()~`>#+\-=|{}\.!])/, '\\\\\1') } 
task_link = "https://#{Setting.host_name}/tasks/#{id}" 

task_data = [
	{ field: 'Проект',  new_value: project.name },
	{ field: 'Статус', new_value: status.name },
	{ field: 'Исполнитель', new_value: (assigned_to.present? ? assigned_to.name : '-') },
	{ field: 'Приоритет', new_value: priority.name },
	{ field: 'Дата окончания', new_value: due_date.present? ? due_date.strftime("%d.%m.%Y") : '-' },	
]

msg_md = "Пользователь *#{escape_telegram_md.call(User.current.name)}* создал задачу:\n"
msg_md += "[__*#{escape_telegram_md.call(type.name)} \\##{id} #{escape_telegram_md.call(subject)}*__](#{task_link})\n"
task_data.each do |e|
   msg_md +=  "#{e[:field]}: *#{escape_telegram_md.call(e[:new_value])}*\n"
end
msg_md += "[__Открыть задачу__](#{task_link})"

begin  
    RestClient.post("https://api.telegram.org/#{bot_token}/sendMessage", 
		{
			"chat_id": chat_id,
			"parse_mode": "MarkdownV2",
			"text": msg_md
		})   
rescue    
end 


```

## Отправка сообщения в telegram-канал при обновлении задачи

* событие запуска: **При обновлении**
* Выполнить скрипт **перед**:

```ruby
bot_token = 'bot<telegram bot token>'
chat_id = <Chat Id>

escape_telegram_md = ->(s) { s.gsub( /([_*\[\]()~`>#+\-=|{}\.!])/, '\\\\\1') } 
date_format = ->(date) { date.present? ? date.strftime("%d.%m.%Y") : '-' }
task_link = "https://#{Setting.host_name}/tasks/#{id}" 

status_was = Status.find(status_id_was)
project_was = Project.find(project_id_was)  
assigned_to_was = assigned_to_id_was.present? ? User.where(id: assigned_to_id_was).take || PlaceholderUser.where(id: assigned_to_id_was).take : nil
priority_was = IssuePriority.find(priority_id_was) 

task_data = [
	{ field: 'Проект', changed: project_id_changed?, old_value: project_was.name, new_value: project.name },
	{ field: 'Статус', changed: status_id_changed?, old_value: status_was.name, new_value: status.name },
	{ field: 'Исполнитель', changed: assigned_to_id_changed?, old_value: (assigned_to_was.present? ? assigned_to_was.name : '-'), new_value: (assigned_to.present? ? assigned_to.name : '-') },
	{ field: 'Приоритет', changed: priority_id_changed?, old_value: priority_was.name, new_value: priority.name },
	{ field: 'Дата окончания', changed: due_date_changed?, old_value: date_format.call(due_date_was), new_value:date_format.call(due_date) },	
	{ field: 'Теги', changed: false, old_value: nil, new_value: tags.present? ? tags.map { |t| t.name }.join(', ') : '-' },
]

msg_md = "Пользователь *#{escape_telegram_md.call(User.current.name)}* обновил задачу:\n"
msg_md += "[__*#{escape_telegram_md.call(type.name)} \\##{id} #{escape_telegram_md.call(subject)}*__](#{task_link})\n"
task_data.each do |e|
   msg_md += e[:field] +  (e[:changed] ? " изменен: *#{escape_telegram_md.call(e[:old_value])}*  ➡️" : ":") + " *#{escape_telegram_md.call(e[:new_value])}*\n"
end

if all_changes.include?(:cf_checklists) && cf_checklists.present? then
  checklists =  JSON.parse(cf_checklists)
  checklists_md = "*Чеклисты*\n" + checklists.map{|l| 
    "*#{escape_telegram_md.call l['name']}*\n" + l['checkboxes'].map{|item| "#{item['check'] ? '✅' : '⬜️'} #{escape_telegram_md.call item['name_checkbox']}"}.join("\n") 
  }.join("\n")
  msg_md += checklists_md + "\n"
end

msg_md += "[__Открыть задачу__](#{task_link})"

#show_error msg_md

# see docs - https://github.com/rest-client/rest-client
begin  
    RestClient.post("https://api.telegram.org/#{bot_token}/sendMessage", 
		{
			"chat_id": chat_id,
			"parse_mode": "MarkdownV2",
			"text": msg_md
		})   
rescue    
end 

```

## Отправка сообщения в telegram-канал при комментировании  задачи

* событие запуска: **При обновлении**
* Условие запуска триггера: `journal_notes.present?`
* Выполнить скрипт перед:

````ruby
bot_token = 'bot<telegram bot token>'
chat_id = <Chat Id>

escape_telegram_md = ->(s) { s.gsub( /([_*\[\]()~`>#+\-=|{}\.!])/, '\\\\\1') } 
task_link = "https://#{Setting.host_name}/tasks/#{id}" 

#show_error "sdf#123".gsub(escape_regex, escape_subst)

status_was = Status.find(status_id_was)
project_was = Project.find(project_id_was)  
assigned_to_was = assigned_to_id_was.present? ? User.find(assigned_to_id_was) : nil 
priority_was = IssuePriority.find(priority_id_was) 

task_data = [
	{ field: 'Проект',  new_value: project.name },
	{ field: 'Статус', new_value: status.name },
	{ field: 'Исполнитель', new_value: (assigned_to.present? ? assigned_to.name : '-') },
	{ field: 'Приоритет', new_value: priority.name },
]

msg_md = "Пользователь *#{escape_telegram_md.call(User.current.name)}* прокомментировал задачу:\n"
msg_md += "[__*#{escape_telegram_md.call(type.name)} \\##{id} #{escape_telegram_md.call(subject)}*__](#{task_link})"
msg_md += "``` #{journal_notes} ```"
task_data.each do |e|
   msg_md +=  "#{e[:field]}: *#{escape_telegram_md.call(e[:new_value])}*\n"
end
msg_md += "[__Открыть задачу__](#{task_link})"

#show_error msg_md

RestClient.post("https://api.telegram.org/#{bot_token}/sendMessage", 
	{
    "chat_id": chat_id,
    "parse_mode": "MarkdownV2",
    "text": msg_md
	})

````

## Отправка сообщения в telegram-канал при изменении статуса задачи

* событие запуска: **При обновлении**
* Поля задачи: **Статус**
* Выполнить скрипт перед:

```ruby
bot_token = 'bot<telegram bot token>'
chat_id = <Chat Id>

escape_telegram_md = ->(s) { s.gsub( /([_*\[\]()~`>#+\-=|{}\.!])/, '\\\\\1') } 
task_link = "https://#{Setting.host_name}/tasks/#{id}" 

status_was = Status.find(status_id_was)
old_status_name = escape_telegram_md.call(status_was.name)
new_status_name = escape_telegram_md.call(status.name)
msg_md = "Пользователь *#{escape_telegram_md.call(User.current.name)}* изменил статус с *#{old_status_name}* на *#{new_status_name}*:\n"
msg_md += "[__*#{escape_telegram_md.call(type.name)} \\##{id} #{escape_telegram_md.call(subject)}*__](#{task_link})"

begin  
    RestClient.post("https://api.telegram.org/#{bot_token}/sendMessage", 
		{
			"chat_id": chat_id,
			"parse_mode": "MarkdownV2",
			"text": msg_md
		})   
rescue    
end 



```



