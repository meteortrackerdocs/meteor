---
icon: square-v
---

# Даты и продолжительность задач

## Назначение дат начала и окончания

Чтобы изменить даты начала и окончания задачи, откройте задачу. Перейдите в раздел **Детали**, кликните по полю "**Дата**".

<figure><img src="../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

1. Переключатель **Ручное планирование** - позволяет вручную изменять даты начала, окончания и продолжительность задачи.
2. Переключатель **Только рабочие дни** - ограничивает даты только рабочими днями.
3. Поля для ввода даты начала, даты окончания и продолжительности задачи.
4. Календарь для выбора дат.
5. Кнопки "**Сохранить**" и "**Отмена**"

<figure><img src="../../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

Вы можете установить дату начала и окончания задачи двумя способами:

* С помощью поля для ввода дат. Введите дату начала и окончания задачи в формате ДД-ММ-ГГГГ.
* С помощью календаря. Выберите дату начала и окончания. Выбранные даты отобразятся в соответствующих полях, в календаре будут выделены темным цветом, а промежуточные — светлым.

Продолжительность задачи будет рассчитана автоматически и появится в поле для ввода - **продолжительность задачи**.

<figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

После выбора дат нажмите "**Сохранить**", чтобы зафиксировать изменения. Изменения дат будут зафиксированы в [Истории по задаче](istoriya-po-zadache.md).

Вы можете выбирать даты начала и окончания в любом порядке. Кликните по дате, а затем кликните по более ранней дате. Более ранняя дата будет использована в качестве начала задачи, более поздняя — в качестве окончания задачи.

### Однодневные мероприятия

Для задач, которые начинаются и заканчиваются в один день, дважды кликните по одной и той же дате в календаре. Некоторые задачи, например вехи, могут иметь только одну дату.

## Рабочие дни и продолжительность

### Рабочие дни

При включении переключателя "**Только рабочие дни**", система будет учитывать только рабочие дни (с понедельника по пятницу). Нерабочие дни (суббота и воскресенье) исключаются из расчета продолжительности, и их нельзя выбрать в качестве даты начала или окончания.

<figure><img src="../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

При выключении переключателя "**Только рабочие дни**" учитываются все дни.

{% hint style="info" %}
Для настройки рабочих дней обратитесь в тех.поддержку METEOR.
{% endhint %}

### Продолжительность

Продолжительность - количество дней между датами начала и окончания задачи (включительно).

<figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

Продолжительность может быть рассчитана автоматически или введена вручную. Чтобы задать продолжительность вручную, кликните по соответствующему полю и введите количество дней.

### Продолжительность при наличии дат начала и окончания

Когда вы устанавливаете дату начала и окончания, продолжительность определяется автоматически. Например, если дата начала установлена на _среду, 13 марта 2024 г._, а дата окончания - на _пятницу, 15 марта 2024 г._, получается продолжительность в 3 дня.

<figure><img src="../../.gitbook/assets/image (287).png" alt=""><figcaption></figcaption></figure>

Изменение продолжительности при уже установленных датах начала и окончания, приведет к изменению даты окончания. В нашем примере, если вы измените продолжительность на 4 дня, может произойти одно из двух:

* Если переключатель "**Только рабочие** **дни**" включен, дата окончания автоматически устанавливается на _понедельник, 18 марта 2024 года_ (поскольку суббота и воскресенье не являются рабочими днями)
* Если переключатель "**Только рабочие** **дни**" выключен, дата окончания автоматически устанавливается на _субботу, 16 марта 2024 г._ (поскольку включены все календарные дни)

### Продолжительность без дат начала и окончания

Возможно, что задача будет иметь только продолжительность без каких-либо установленных дат начала или окончания. Если даты не заданы, вы можете указать только продолжительность, что полезно, если точные даты еще не известны.

## Режим планирования

### Ручное планирование

Активация переключателя "**Ручное планирование**" включает [режим ручного планирования](../diagramma-ganta/rezhimy-avtomaticheskogo-i-ruchnogo-planirovaniya.md#rezhim-ruchnogo-planirovaniya) для задачи. При этом игнорируются отношения между задачами, так что вы можете выбрать любые даты начала и окончания, даже те, которые обычно были бы ограничены из-за [связи предшествует-следует](svyazi-i-ierarkhii-zadach.md).

Ручное планирование также разделяет даты начала и окончания родительских и дочерних задач. Это означает, что даты родительских задач больше не ограничены датами дочерних задач, и дочерние задачи могут быть запланированы за пределами диапазона родительских задач.

<figure><img src="../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

Ручное планирование может быть полезно, когда вам нужно привязать задачи к фиксированным датам, например, потому, что даты предыдущих или последующих задач еще не известны.

### Автоматическое планирование

При деактивации переключателя "**Ручное планирование**" включается режим [автоматического планирования](../diagramma-ganta/rezhimy-avtomaticheskogo-i-ruchnogo-planirovaniya.md#rezhim-avtomaticheskogo-planirovaniya).

<figure><img src="../../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

При этом даты задач выставляются автоматически:

* При связи _Предшествует-следует_: если дата окончания задачи-предшественника больше даты начала задачи-последователя, дата начала задачи-последователя будет скорректирована на дату окончания задачи-предшественника. Но это не работает в обратную сторону.

Например, если задача 1 завершается 5 октября, а задача 2 должна начаться 13 октября, и задача 1 задерживается на десять дней, установив дату окончания задачи 1 на 15 октября, дата начала задачи 2 автоматически перенесется на 16 октября.

* _Родительская задача-дочерняя задача_: дата начала родительской задачи соответствует самой ранней дате дочерней задачи, дата окончания родительской задачи соответствует самой поздней дате дочерней задачи.

Представим, что у нас есть задача по организации мероприятия (родительская задача), которая состоит из нескольких подзадач (дочерние задачи). Одной из дочерних задач является "Подготовить презентацию", которая начинается 1 сентября и заканчивается 10 сентября. Другой дочерней задачей является "Закупить материалы", которая начинается 25 августа и заканчивается 5 сентября.\
Начало родительской задачи (организация мероприятия) будет соответствовать самой ранней дате дочерней задачи (25 августа - начало "Закупить материалы"). А окончание родительской задачи будет соответствовать самой поздней дате дочерней задачи (10 сентября - окончание "Подготовить презентацию"). Таким образом, выполнение родительской задачи будет охватывать все дочерние задачи и их временные рамки.

* Нельзя изменить даты начала и окончания задачи, у которой есть дочерние задачи, **если она находится в режиме автоматического планирования**.

<figure><img src="../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

