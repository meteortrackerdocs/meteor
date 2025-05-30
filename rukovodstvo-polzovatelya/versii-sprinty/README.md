---
icon: square-v
---

# Версии / Спринты

Работа в гибких проектных командах становится все более востребованной. METEOR поддерживает работу с методологией Scrum, предлагая полезные функции для управления проектами. С его помощью вы можете расставлять приоритеты для задач в бэклоге спринтов и продукта, оценивать задачи, настраивать доски для наглядного планирования версий / спринтов.

Обратите внимание, что данное руководство не обучает методологии Scrum, а лишь объясняет как использовать возможности METEOR.

Ключевыми элементами успешной работы в Scrum являются поддерживаемый и приоритезированный бэклог продукта, а также создание спринтов. В METEOR можно легко создавать задачи с различными типами и объединять их в Версии / спринты.

{% hint style="info" %}
Для использования Спринтов необходимо активировать модуль "Планирование спринтов" [в настройках проекта](../proekty/nastroiki-proekta.md#moduli-proekta).

Версия - не имеет статуса и SP, и данный функционал доступен всегда.
{% endhint %}

## Просмотр версий / спринтов

Вы можете просмотреть версии / спринты следующими способами:

* на доске по версиям - здесь видны все существующие версии/спринты и задачи, которые к ним относятся. Чтобы узнать, как добавить колонки на доску, посетите страницу **"**[**Колонки на доске**](../doski/kolonki-na-doske.md)**".**
* в инструменте "**Управление версиями / спринтами**" (открывается через контекстное меню проекта) - раздел для администрирования версий / спринтов.

<figure><img src="../../.gitbook/assets/image (1060).png" alt="" width="409"><figcaption></figcaption></figure>

В инструменте "**Управление версиями / спринтами"** отображается список всех версий / спринтов проекта.

<figure><img src="../../.gitbook/assets/image (770).png" alt=""><figcaption></figcaption></figure>

## Создание версии / спринта

Вы можете создать версию / спринт двумя способами:

* в инструменте "Управление версиями / спринтами";
* на доске по версиям.

### Создание версии / спринта из раздела Управление версиями / спринтами

Для создания версии / спринта из раздела "**Управление версиями / спринтами"** нажмите кнопку "**Добавить**".

<figure><img src="../../.gitbook/assets/image (771).png" alt=""><figcaption></figcaption></figure>

Откроется окно создания версии / спринта. Необходимо заполнить поля:

* Имя - уникальное название версии / спринта для проекта (обязательное поле).
* Статус - выберите "открыт", "начат" или "закрыт".
* Дата начала и Дата окончания - сроки работы над версией / спринтом.
* Совместное использование - выберите подходящий вариант использования версии / спринта между проектами.
* Wiki - привяжите wiki-страницу к версии / спринту.
* Описание - добавьте цель или описание версии / спринта.

<figure><img src="../../.gitbook/assets/image (772).png" alt=""><figcaption></figcaption></figure>

Доступные варианты совместного использования версий / спринтов:

* Не используется другими (по умолчанию) - версия / спринт создается только в текущем проекте.
* Во всех проектах - версия / спринт будет создана во всех проектах вашего экземпляра METEOR, но задачи нужно будет добавить вручную.
* С подпроектами - версия / спринт создается также во всей иерархии подпроектов текущего проекта. Например, если создать спринт "с подпроектами" в проекте "Подпроект 1.2", то спринт будет дополнительно создан только в проекте "Подпроект 1.2.1.

<figure><img src="../../.gitbook/assets/image (773).png" alt="" width="353"><figcaption></figcaption></figure>

* С иерархией проектов - версия / спринт будет создана во всех родительских проектах и всех его подпроектах. Но не будет создан в соседних ветках подпроектов его родительского проекта. Например, если создать спринт "с иерархией проектов" в проекте "Подпроект 1.2", то спринт также будет создан в проектах "Подпроект 1" и "Тестовый". Но не будет создан в проектах "Подпроект 1.1", "Подпроект 2", "Подпроект" 2.1 и "Подпроект 2.2".

<figure><img src="../../.gitbook/assets/image (774).png" alt="" width="353"><figcaption></figcaption></figure>

* С деревом проектов - версия / спринт будет создана во всем дереве подпроектов всех его родительских проектов. Например, если создать спринт "с деревом проектов" в проекте "Подпроект 1.2", то спринт также будет создан во всем дереве подпроектов проекта "Тестовый".

<figure><img src="../../.gitbook/assets/image (775).png" alt="" width="353"><figcaption></figcaption></figure>

### Создание версии / спринта с доски

Для создания версии / спринта на доске необходимо заполнить те же поля, что и в в инструменте "Управление версиями / спринтами":

* Имя - уникальное название версии / спринта для проекта (обязательное поле).
* Статус - выберите "открыт", "начат" или "закрыт".
* Дата начала и Дата окончания - сроки работы над версией / спринтом.
* Совместное использование - выберите подходящий вариант использования версии / спринта между проектами.
* Wiki - привяжите wiki-страницу к версии / спринту.
* Описание - добавьте цель или описание версии / спринта.

<figure><img src="../../.gitbook/assets/image (776).png" alt=""><figcaption></figcaption></figure>

После создания версии / спринта появится на доске в виде колонки:

<figure><img src="../../.gitbook/assets/image (777).png" alt=""><figcaption></figcaption></figure>

## Редактирование версии / спринта

Редактируйте версию / спринт через контекстное меню колонки на доске:

<figure><img src="../../.gitbook/assets/image (778).png" alt=""><figcaption></figcaption></figure>

Или через инструмент "**Управление версиями / спринтами**":

<figure><img src="../../.gitbook/assets/image (779).png" alt=""><figcaption></figcaption></figure>

## Запуск версии / спринта

Функции запуска, приостановки и завершения доступны только при включенном модуле "Планирование спринтов".&#x20;

**Для запуска** версии / спринта необходимо изменить её статус, через контекстное меню колонки на доске по версиям /спринтам:

<figure><img src="../../.gitbook/assets/image (780).png" alt=""><figcaption></figcaption></figure>

Или изменить статус через соответствующую кнопку в шапке колонки на доске по версиям /спринтам:

<figure><img src="../../.gitbook/assets/image (781).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Задачи в запущенный спринт добавлять нельзя. Сперва приостановите спринт, добавьте или удалите задачи. Повторно запустите спринт.
{% endhint %}

## Завершение версии / спринта

Выберите версию / спринт и измените её статус на "**Завершить**".&#x20;

<figure><img src="../../.gitbook/assets/image (782).png" alt=""><figcaption></figcaption></figure>

## Удаление версии / спринта

### Удаление версии / спринта с доски

Чтобы удалить версию / спринт с доски воспользуйтесь кнопкой "**Удалить с доски**":

<figure><img src="../../.gitbook/assets/image (783).png" alt=""><figcaption></figcaption></figure>

Версия / спринт будет скрыта, но останется в системе и может быть возвращена на доску.

### Удаление версии / спринта из системы

Чтобы полностью удалить версию/спринт, перейдите в инструмент "**Управление версиями / спринтами**".

{% hint style="info" %}
Удалить можно только версию / спринт без задач. Перенести задачи в бэклог или другую версию / спринт перед удалением.
{% endhint %}

Используйте кнопку "**Удалить**" в контекстном меню версии / спринта:

<figure><img src="../../.gitbook/assets/image (784).png" alt=""><figcaption></figcaption></figure>

В открывшемся окне подтвердите удаление:

<figure><img src="../../.gitbook/assets/image (785).png" alt=""><figcaption></figcaption></figure>

