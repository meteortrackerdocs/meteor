---
description: В этом документе вы получите первое представление о задачах.
---

# Задачи

## Что такое задача?

Задача — это атомарная единица работы, которую необходимо выполнить для достижения целей проекта. Она содержит всю информацию, необходимую для планирования, исполнения и контроля.

## Ключевые характеристики

1. **Основные атрибуты**
   * **ID** (он же номер задачи) - уникальный неизменяемый идентификатор. Нумерация задач сквозная для всех проектов.
   * **Название и описание** - краткий заголовок и детальное ТЗ, объясняющее суть задачи и что требуется сделать.
   * **Тип** - классификация по характеру работы (ошибка, улучшение, задача и др.).
   * **Приоритет** - важность относительно других задач.
   * **Сроки выполнения** - даты начала и завершения.
   * **Ответственные лица** - исполнитель, ответственный и наблюдатели.
   * **Статус** - текущая стадия выполнения.
2. **Дополнительные атрибуты**
   * **Связи** - 11 типов зависимостей между задачами.
   * **Подзадачи** - декомпозиция сложных работ (кроме вех).
   * **Комментарии** - обсуждения и уточнения.
   * **Вложения** - файлы, скриншоты, документы.
3. **Пользовательские поля** - возможность добавлять уникальные атрибуты под специфику проекта.&#x20;

## Типы задач

Назначение типизации:

* чёткое разделение работ (описание предварительно созданных типов задач приведено ниже);
* ускорение фильтрации и поиска;
* индивидуальные рабочие потоки (workflow);
* точная аналитика по видам деятельности;
* правильное распределение по командам;
* гибкая расширяемость через настройку собственных полей для каждого типа.

Предварительно настроенные типы задач в METEOR:

<table><thead><tr><th width="134">Название</th><th width="261">Значение</th><th width="259">Статусы по умолчанию</th><th>Доступны в шаблонах</th></tr></thead><tbody><tr><td>Эпик</td><td>Большой блок работ, которые можно разбить на более мелкие.</td><td>Новая, Описание требований, Требования сформированы, Проектирование, К разработке, В работе, Закрыто, В ожидании, Отклонено.</td><td>Scrum проект</td></tr><tr><td>История</td><td>Краткое изложение требований или запросов, составленное с точки зрения конечного пользователя.</td><td>Новая, Описание требований, Требования сформированы, Проектирование, К разработке, В работе, Закрыто, В ожидании, Отклонено.</td><td>Scrum проект</td></tr><tr><td>Задача</td><td>Задача для выполнения одним или несколькими исполнителями.</td><td>Новая, К разработке, В работе, Закрыто, В ожидании, Отклонено.</td><td>Scrum проект, Kanban проект, Waterfall проект</td></tr><tr><td>Ошибка</td><td>Ошибка в коде или системе, из-за которой что-то работает не корректно.</td><td>Новая, К разработке, В работе, Разработано, В тестировании, Протестировано, Тест не пройден, Закрыто, В ожидании, Отклонено.</td><td>Scrum проект, Kanban проект</td></tr><tr><td>Улучшение</td><td>Оптимизация существующей функциональности продукта</td><td>Новая, Описание требований, Требования сформированы, К разработке, В работе, Разработано, В тестировании, Протестировано, Тест не пройден, Закрыто, В ожидании, Отклонено.</td><td>Scrum проект</td></tr><tr><td>Фаза</td><td>Набор логически взаимосвязанных работ проекта, в процессе завершения которых достигается один из основных или существенных промежуточных результатов проекта</td><td>Новая, Планируется, Запланировано, В работе, Закрыто, В ожидании, Отклонено.</td><td>Waterfall проект</td></tr><tr><td>Веха</td><td>С помощью вех можно выделять события достижений значимого результата проекта.</td><td>Новая, Планируется, Запланировано, В работе, Закрыто, В ожидании, Отклонено.</td><td>Waterfall проект</td></tr></tbody></table>

Администратор вашего экземпляра METEOR может внести изменения в предустановленные типы или создать собственные. Подробнее можно прочесть в статье о [Типах задач](../rukovodstvo-administratora/zadachi/tipy-zadach.md).

## Связи

[Связи между задачами](../rukovodstvo-polzovatelya/zadachi/svyazi-i-ierarkhii-zadach.md) помогают отражать логические зависимости (например, последовательность выполнения или блокировки), что делает планирование прозрачным и предотвращает хаотичное выполнение работ. Они также автоматизируют контроль процессов — изменение статуса или сроков одной задачи автоматически влияет на связанные с ней задачи, экономя время на ручных корректировках.

## Подзадачи

Дробите сложные задачи на простые шаги - так легче оценивать, выполнять и контролировать работу. Распределяйте части задач между разными исполнителями, сохраняя общую структуру.  [Подзадачи](../rukovodstvo-polzovatelya/zadachi/svyazi-i-ierarkhii-zadach.md#ierarkhiya-zadach) отображаются отдельно от связей.

{% hint style="info" %}
Задача типа "Веха" не может иметь подзадачи.
{% endhint %}

## Статусы задач

Статусы позволяют отслеживать прогресс - видно на каком этапе находится задача (например, "В работе", "Тестирование", "Закрыто"). Так же помогают автоматизировать процессы - смена статуса может запускать уведомления, менять доступ или обновлять сроки.

Администратор вашего экземпляра METEOR может внести изменения в предустановленные статусы или создать собственные. Подробнее можно прочесть в статье о [Статусах](../rukovodstvo-administratora/zadachi/statusy.md).

Список предопределённых в METEOR статусов:

<table><thead><tr><th width="251">Название</th><th>Назначение</th></tr></thead><tbody><tr><td>Новая</td><td>Особый статус, который используется при создании задачи, настройка рабочих потоков начинается с этого статуса.</td></tr><tr><td>Описание требований</td><td>Осуществляется анализ и описание требований к продукту.</td></tr><tr><td>Требования сформированы</td><td>Буферный статус, на который задача переводится как только требования к продукту сформированы.</td></tr><tr><td>Согласовано</td><td>Задача принята к исполнению. Используйте как точку принятия обязательств.</td></tr><tr><td>Планируется</td><td>Задача готова к производственному планированию.</td></tr><tr><td>Запланировано</td><td>Работы по задаче запланированы (установлены даты начала /окончания или задача добавлена в версию/спринт).</td></tr><tr><td>Проектирование</td><td>Выполняется проектировочное решение.</td></tr><tr><td>К разработке</td><td>Задача готова к выполнению производственной работы.</td></tr><tr><td>В работе</td><td>Задача находится в работе.</td></tr><tr><td>Разработано</td><td>Задача готова к тестированию.</td></tr><tr><td>В тестировании</td><td>Задача находится в тестировании.</td></tr><tr><td>Протестировано</td><td>Тестирование успешно пройдено.</td></tr><tr><td>Тест не пройден</td><td>Тестирование не пройдено, имеются замечания.</td></tr><tr><td>Закрыто</td><td>Закрывающий статус. Все работы по задаче завершены, результаты работ проверены и приняты.</td></tr><tr><td>В ожидании</td><td>Выполнение задачи приостановлено. Рекомендуется добавлять комментарий при переводе задачи на данный статус и из него.</td></tr><tr><td>Отклонено</td><td>Задача не принята к исполнению.</td></tr></tbody></table>

## Дополнительные ссылки

1. [Просмотр задач](../rukovodstvo-polzovatelya/zadachi/prosmotr-zadach.md).\
   Как просматривать задачи: виды отображения, способы открытия задач; как просматривать историю по задаче.
2. [Создание задач](../rukovodstvo-polzovatelya/zadachi/sozdanie-zadach.md).\
   Как создавать задачи, какие поля необходимо заполнить в самом начале, из каких представлений можно создавать задачи.
3. [Редактирование задач](../rukovodstvo-polzovatelya/zadachi/redaktirovanie-zadach.md).\
   Как внести изменения в задачу, какие роли могут принимать пользователи в задаче, как посмотреть статус и рабочий поток, как добавить комментарий или приложить файл, как работать с наблюдателями в задаче.
4. [Копирование задач](../rukovodstvo-polzovatelya/zadachi/kopirovanie-zadach.md).\
   Как копировать задачи и какая информация будет скопирована.
5. [Даты и продолжительность задач](../rukovodstvo-polzovatelya/zadachi/daty-i-prodolzhitelnost-zadach.md).\
   Как назначить дату начала и окончания задачи, функция ручного планирования, планирование рабочих дней.
6. [Связи и иерархии задач](../rukovodstvo-polzovatelya/zadachi/svyazi-i-ierarkhii-zadach.md).\
   Где отображаются связи между задачами, какие типы связей допускаются, как удалить связи.
7. [Типы задач](../rukovodstvo-administratora/zadachi/tipy-zadach.md).\
   Как посмотреть доступные типы задач, настройка формы и рабочего потока для типа задачи (Раздел доступен администратору экземпляра METEOR).
8. [Статусы](../rukovodstvo-administratora/zadachi/statusy.md).\
   Если специфика вашей работы подразумевает другие статусы, то ознакомьтесь со статьей об администрировании статусов (Раздел доступен администратору экземпляра METEOR).
