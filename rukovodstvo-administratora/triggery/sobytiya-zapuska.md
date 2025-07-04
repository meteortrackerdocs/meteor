---
description: Как работают триггеры, настроенные на разные события запуска
icon: wrench
---

# События запуска

В этой главе детально описывается то, как работает каждый тип событий запуска триггеров в METEOR.

## При создании

Триггеры, настроенные на это событие, будут вызываться во время создания задачи или отметки времени.&#x20;

Вам доступны два момента времени, в которые вы можете выполнить код:

1. Перед сохранением новой задачи/отметки времени (**Код триггера перед**, или before):\
   Используйте этот блок для кода, который будет:
   1. запрещать (отменять) создание сущности
   2. изменять или добавлять данные на основе введенных пользователем данных
   3. добавлять шаблонные данные
2. После сохранения задачи/отметки времени (**Код триггера после**, или after)\
   Этот блок необходимо использовать для кода, который будет:
   1. Создавать дополнительные сущности (например, подзадачи)
   2. Заполнять подчиненные данные (например, комментарии, наблюдатели, связи, вложенные файлы). Подчиненные сущности можно создавать только тогда, когда родительская сущность уже создана.

Вы можете использовать одновременно обе секции. Но вы должны понимать, что код в них будет выполнять в разные моменты времени. Вот общая последовательность запуска триггеров:

1. Пользователь в интерфейсе заполнил форму создания сущности (задачи или отметки времени).
2. Создается врмеенная структура, содержащая данные, введенные пользователем.
3. Запускаются код секций **before** всех триггеров, подходящих под эту сущность.
4. Временная структура со всеми изменениями, сделанными  на шаге 3 сохраняется в базе данных. В этот момент производится проверка сущности внутренними механизмами системы (роли, права, отношения к проектам и так далее).
5. Запускаются код секций **after** всех триггеров, подходящих под эту сущность.

{% hint style="info" %}
Триггеры, настроенные на этот тип запуска будут выполняться **исключительно только при создании** новой задачи или отметки времени.
{% endhint %}

## При сохранении

Триггеры, настроенные на событие "При сохранении", будут выполнять как при создании объекта, так и при его обновлении.

Вам доступны два момента времени, в которые вы можете выполнить код:

1. Перед сохранением данных новой или измененной задачи/отметки времени (**Код триггера перед**, или before);
2. После сохранения задачи/отметки времени (**Код триггера после**, или after).

Вы можете использовать одновременно обе секции.&#x20;

{% hint style="info" %}
Триггеры, настроенные на этот тип запуска будут выполняться **и во время создания**, **и во время обновления** задачи или отметки времени.&#x20;
{% endhint %}

## При обновлении

Триггеры, настроенные на событие "При обновлении", будут выполнять во время обновления.

Вам доступны два момента времени, в которые вы можете выполнить код:

1. Перед сохранением данных измененной задачи/отметки времени (**Код триггера перед**, или before);
2. После сохранения задачи/отметки времени (**Код триггера после**, или after).

Вы можете использовать одновременно обе секции.&#x20;

{% hint style="info" %}
Триггеры, настроенные на этот тип запуска будут выполняться **только во время обновления** задачи или отметки времени.&#x20;
{% endhint %}

## При удалении

Триггеры, настроенные на событие "При удалении", будут выполнять во время удаления задачи или отметки времени.

Вам доступны два момента времени, в которые вы можете выполнить код:

1. Перед удалением задачи/отметки времени (**Код триггера перед**, или before):\
   В этом блоке вы можете:
   1. Приостановить / запретить удаление сущности,
   2. Произвести необходимые проверки возможности удаления,
   3. Создать копию или наследника объекта с обновлением данных.&#x20;
2. После удаления задачи/отметки времени (**Код триггера после**, или after):\
   В этом блоке можно выполнять:
   1. Удаление зависимых объектов,
   2. Очистку "ненужных" данных,
   3. Информирование об удалении.

Вы можете использовать одновременно обе секции.&#x20;

{% hint style="info" %}
Триггеры, настроенные на этот тип запуска будут выполняться **только во время удаления** задачи или отметки времени.&#x20;
{% endhint %}

## Вручную

Это виртуальный тип события, который полностью запрещает автоматическое выполнение триггеров.

Триггеры, настроенные на этот тип событий, смогут выполняться только путем нажатия кнопки "Выполнить" в списке триггеров.&#x20;

<figure><img src="../../.gitbook/assets/Снимок экрана 2024-10-10 в 00.39.57.png" alt=""><figcaption><p>Запуск триггера с типом события "Вручную"</p></figcaption></figure>

Право на выполнение триггеров с этим типом события запуска имеет только администратор.

Этот тип события запуска мы рекомендуем применять для выполнения запрограммированных обслуживающих процедур (скриптов), которые по мере необходимости будут выполняться вручную пользователем с правами администратора системы.

В качестве примера приведем такой сценарий:

Допустим, в задачах вы задействовали пользовательское поле "Ответственный за документацию" с типом "пользователь". В некоторых задачах это поле заполнено значением "Иванов Иван". У вас возникла потребность в переводе Ивана на другую должность, и вам необходимо заменить Ивана на Марию. В этом случае вы можете написать триггер, который во всех задачах указанного проекта произведет такую замену.

### Особенности запуска этого вида триггеров.

Триггеры данного типа выполняются c помощью фоновых заданий.&#x20;

Когда пользователь нажимает кнопку "Запустить", фактически происходит вызов метода API:

`/op/api/v3/triggers/{ID триггера}/run`

Этот метод создаст фоновое задание (background Job) на запуск триггера и ответит редиректом на ID этого процесса для проверки статуса:

`Location: /op/api/v3/job_statuses/a77cf1d4-18eb-4073-b4f5-15005e3c2bde`

Имея ID фонового задания, система ежесекундно проверяет статус его выполнения запросом:

```json
/op/api/v3/job_statuses/a77cf1d4-18eb-4073-b4f5-15005e3c2bde

Response:
{
    "_type": "JobStatus",
    "jobId": "a77cf1d4-18eb-4073-b4f5-15005e3c2bde",
    "status": "in_process",
    "message": null,
    "payload": null,
    "_links": {
        "self": {
            "href": "/op/api/v3/job_statuses/a77cf1d4-18eb-4073-b4f5-15005e3c2bde"
        }
    }
}
```

Это будет происходить до того момента, пока не будет получен **status**, отличный от "**in\_process**". Как только триггер завершит свою работу, следующий вызов метода проверки статуса вернет:

```json
/op/api/v3/job_statuses/a77cf1d4-18eb-4073-b4f5-15005e3c2bde

Response в случае успешного выполнения триггера:
{
    "_type": "JobStatus",
    "jobId": "a77cf1d4-18eb-4073-b4f5-15005e3c2bde",
    "status": "success",
    "message": null
    "payload": null,
    "_links": {
        "self": {
            "href": "/op/api/v3/job_statuses/a77cf1d4-18eb-4073-b4f5-15005e3c2bde"
        }
    }
}

Response в случае ошибки в триггере:
{
    "_type": "JobStatus",
    "jobId": "a77cf1d4-18eb-4073-b4f5-15005e3c2bde",
    "status": "failure",
    "message": "my error",
    "payload": null,
    "_links": {
        "self": {
            "href": "/op/api/v3/job_statuses/a77cf1d4-18eb-4073-b4f5-15005e3c2bde"
        }
    }
}
```



Все ошибки, генерируемые в коде триггера методом `show_error()`, будут отображаться в окне результата выполнения триггера, а не в во всплывающих сообщениях, как это происходит при выполнении других видов триггеров.

## По расписанию

Триггеры, настроенные на этот тип событий запуска, будут выполняться в соответствии с указанным расписанием запуска.

В настройках таких триггеров вы также можете указать для каких объектов должен выполняться триггер.\
\
Но самое важное здесь - это настройка расписания автоматического запуска.\
Расписание вводится в виде cron-выражения.

<figure><img src="../../.gitbook/assets/image (1158).png" alt=""><figcaption></figcaption></figure>

... материал дополняется
