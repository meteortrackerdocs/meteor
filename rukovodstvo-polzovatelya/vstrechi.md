# Встречи

METEOR автоматически записывает встречи через сервис [mymeet.ai](http://mymeet.ai), преобразуя их в структурированные задачи с исполнителями и сроками.

**Требования:**\
Для начала работы необходимо [настроить интеграцию](../rukovodstvo-administratora/integracii/integraciya-s-mymeet.ai.md) с [mymeet.ai.](https://mymeet.ai/)

## 1. Создание и запись встречи

**Шаги:**

1. Создайте встречу в поддерживаемом сервисе (Zoom, Google Meet, Яндекс.Телемост, Контур.Толк, SaluteJazz, TrueConf) и скопируйте ссылку
2.  В METEOR:

    * Нажмите на кнопку "Добавить встречу" в левом меню:

    <figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

    * Убедитесь, что активирован переключатель "**Записать встречу**";
    * Выберите сервис;
    * Вставьте ссылку на встречу;
    * Укажите название встречи (опционально);
    * Нажмите кнопку "**Записать встречу**".

    <figure><img src="../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Важно!**

* Бот mymeet подключается **сразу** после нажатия кнопки “Записать встречу”
* Для отложенных встреч добавляйте запись встречи в METEOR непосредственно перед началом встречи
{% endhint %}

## 2. Обработка и результаты

После завершения встречи (обычно в течение 1-2 часов) вы получите в сервисе mymeet:

* **Транскрипт** с разметкой по главам и спикерам&#x20;

<figure><img src="../.gitbook/assets/image (1119).png" alt="" width="563"><figcaption></figcaption></figure>

* **Отчет по встрече** (тип отчета "**Обычная встреча**") с кратким содержанием всей встречи и  итогами по темам

<figure><img src="../.gitbook/assets/image (1120).png" alt="" width="563"><figcaption></figcaption></figure>

* **Задачи** с исполнителями и дедлайнами

<figure><img src="../.gitbook/assets/image (1123).png" alt="" width="563"><figcaption></figcaption></figure>

## 3. Автоматическая синхронизация

**Как работает:**

* Каждые 5 минут METEOR проверяет новые встречи в сервисе [mymeet.ai](http://mymeet.ai) и создает в проекте [mymeet.ai](http://mymeet.ai):
  * Основную задачу (тип "MyMeet") с итогами встречи;
  * и если на встрече были поставлены задачи, то они создаются в виде подзадач (тип "Задача") к основной задаче с:
    * описанием и темой;
    * исполнителем (при точном совпадении имени и фамилии с пользователем METEOR);
    * датой окончания (если указана).

<figure><img src="../.gitbook/assets/image (1127).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (1129).png" alt="" width="563"><figcaption></figcaption></figure>

**Дополнительно:**

* Встречи, созданные напрямую в mymeet, также синхронизируются;
* Логи синхронизации хранятся в истории сервисной задачи "[mymeet.ai](http://mymeet.ai)" (проект "Интеграции"):

<figure><img src="../.gitbook/assets/image (1131).png" alt="" width="563"><figcaption></figcaption></figure>

{% hint style="info" %}
**Ограничение:**\
Поддерживается только тип отчета "Обычная встреча". Другие типы отчетов могут синхронизироваться некорректно.
{% endhint %}

## 4. Перенос задач в другой проект

Вы можете перенести задачи в другой проект, изменив поле **«Проект»** у основной задачи.

Подзадачи переместятся автоматически.

<figure><img src="../.gitbook/assets/image (1132).png" alt=""><figcaption></figcaption></figure>

## 5. Ручная синхронизация

Если требуется обновить данные без ожидания автоматической синхронизации:

1. Перейдите в проект "Интеграции";
2. Откройте сервисную задачу:
   * Название: "[mymeet.ai](http://mymeet.ai)";
   * Тип: "Интеграция".
3.  В меню действий выберите:\
    → **"Синхронизировать с mymeet"**



<figure><img src="../.gitbook/assets/image (1133).png" alt="" width="563"><figcaption></figcaption></figure>

**Что происходит:**

* Система сразу проверяет новые встречи в [mymeet.ai](http://mymeet.ai);
* Создаёт задачи по тому же принципу, что и при автоматической синхронизации;
* Результаты отображаются в истории задачи "[mymeet.ai](http://mymeet.ai)".

**Когда использовать:**

* После важных встреч, которые нужно обработать срочно;
* Если автоматическая синхронизация ещё не произошла;
* При подозрении на пропущенные встречи.

## 6. Загрузка файлов

Вы так же можете загрузить видео со встречи для обработки. Для этого в METEOR:

* Нажмите на кнопку "**Добавить встречу**" в левом меню:

<figure><img src="../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

* Выберите пункт "**Загрузить файл**";
* Выберите файл с компьютера или перетащите в область для загрузки;
* Укажите название встречи (опционально);
* Нажмите кнопку "**Загрузить файл**".

<figure><img src="../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>
