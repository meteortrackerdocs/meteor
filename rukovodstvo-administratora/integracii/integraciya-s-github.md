---
description: >-
  METEOR предоставляет интеграцию с Pull Requests из GitHub, что позволяет
  связать процесс разработки с планированием задач
---

# Интеграция с GitHub

Интеграция позволяет создавать ветки GitHub прямо из интерфейса METEOR.

## Отображение в задаче

1. Вкладка "**GitHub**" - будет отображать следующие данные из gitHub:

* Все связанные Pull Requests с их статусами (Открыт, Объединен, Закрыт, Черновик);

<figure><img src="../../.gitbook/assets/image (1136).png" alt=""><figcaption></figcaption></figure>

* Статус GitHub Actions (success, queued, in\_progress, action\_required, failure, neutral, skipped, cancelled, timed\_out);

<figure><img src="../../.gitbook/assets/Снимок экрана 2025-04-22 в 19.55.09.png" alt=""><figcaption><p>GitHub Actions</p></figcaption></figure>

* Связь между задачами и Pull Requests (отношение n:m, задача может быть связана с несколькими Pull Requests, а Pull Requests — с несколькими задачами).

2. Вкладка "**История**" - будет отображать изменения по PR (обновления статусов, изменение описания PR):

<figure><img src="../../.gitbook/assets/image (1137).png" alt=""><figcaption></figcaption></figure>

## Настройка интеграции

### METEOR

1.  Создайте специальную [роль](../polzovateli-zapolniteli-i-gruppy/roli-i-prava/roli.md), в которой будут как минимум два права:

    * "Просмотр задач";
    * "Добавление комментариев".

    &#x20;_(Администрирование -> Пользователи и права -> Роли -> Конкретная роль -> раздел "Задачи")_

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXd4uZjGBCeGuhv46OW2favKAy07FMOPAY62xKLC5514b2UPS-XTvGldAygZkM8d-y8PTU6L752khHil22RWtnAWK_B-nB3Pzmjsx_RCkz6scq6FFoDx9Wq6hR7OInI1HBitx5-qLg?key=yvs9BW-M6yN5IDhNKDHndYGb" alt=""><figcaption></figcaption></figure>

2.  Создайте [пользователя](../polzovateli-zapolniteli-i-gruppy/polzovateli.md) для интеграции

    * &#x20;назначьте ему созданную роль;
    * добавьте этого пользователя во все проекты, где нужна интеграция с GitHub.

    _(Администрирование -> Пользователи и права -> Пользователи)_

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXcbQFQzgftMFkknliuIF9SjiDgb9wNjxB2YTNLpwnzAyrbgQlaIiv4ZKi8fSmTNLA0V405b3wzYoT0Lhxea7kq2SqftS498BIidLMTBX-FqAg-bpZVoTeDdbkHscGq6j8fb6mRngw?key=yvs9BW-M6yN5IDhNKDHndYGb" alt=""><figcaption></figcaption></figure>

3. Сгенерируйте API-токен для этого пользователя (он понадобится вам на стороне GitHub). Для генерации токена необходимо:
   * войдите в систему под учётной записью нового пользователя.
   * перейдите в **Профиль** (нажмите на аватарку в правом верхнем углу и выберите Профиль).
   * далее "**Токены доступа**".
   * нажмите на кнопку "+ Токен API".

{% hint style="info" %}
**Важно!** Обязательно скопируйте сгенерированный токен и надёжно сохраните его. Токен нельзя будет посмотреть позже!
{% endhint %}

4. Активируйте модуль GitHub в [настройках проекта](../../rukovodstvo-polzovatelya/proekty/nastroiki-proekta.md#moduli-proekta) (_Настройки проекта -> Модули)_.
5. Выдайте права на просмотр вкладки "**GitHub**" нужным [ролям](../polzovateli-zapolniteli-i-gruppy/roli-i-prava/):
   * "Показывать содержимое GitHub".

### Настройка GitHub

1. Создайте webhook для каждого репозитория:

* Content-Type: application/json
* URL: https://mycompany.u-meteor.ru/op/webhooks/github?key=ВАШ\_ТОКЕН
* События: "Send me everything"

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXduH99CBjL-eFBHjbxGISgAsBjXWLVmvliAp6LI7kSoAw-8a2yEVBCI-rky2Tfnah1f9z6-gCEfmWdHDjGC9WoY-0G2zA-f_9n0y2sTmQ95wEIbFJBMNd1MQYEWlLESWSCHsjd_?key=yvs9BW-M6yN5IDhNKDHndYGb" alt=""><figcaption></figcaption></figure>

Интеграция готова к использованию!

## Использование интеграции с GitHub

### Создание ветки

1. Откройте вкладку GitHub в карточке задачи;
2. Нажмите "Git-сниппеты";
3. Скопируйте имя ветки:

<figure><img src="../../.gitbook/assets/image (1153).png" alt=""><figcaption></figcaption></figure>

4. В Git-клиенте создайте ветку с этим именем:

<figure><img src="../../.gitbook/assets/tg_image_846903961.png" alt=""><figcaption></figcaption></figure>



### Создание коммита

1. METEOR предлагает шаблон сообщения коммита на основе задачи:

<figure><img src="../../.gitbook/assets/image (1154).png" alt=""><figcaption></figcaption></figure>

2. В GitHub создайте коммит с этим описанием (Extended description):

<figure><img src="../../.gitbook/assets/image (1155).png" alt="" width="563"><figcaption></figcaption></figure>

### Cоздание Pull Request

Для того, чтобы связать Pull Request с задачей METEOR, в описании Pull Request должна быть:

* ссылка на задачу,  ранее скопированная из METEOR (при условии, что коммит только один);
* или укажите «МТ#ID», где ID - это идентификатор задачи METEOR, в описании. Например, MT#2197. Данные о PR подтянутся в METEOR и будут отображаться на вкладке "**GitHub**".

{% hint style="info" %}
**Обратите внимание**, что «МТ#ID» чувствителен к регистру. «мт#ID» - не будет работать.
{% endhint %}

<figure><img src="../../.gitbook/assets/tg_image_2662194258.png" alt=""><figcaption></figcaption></figure>

Если коммит не один, то при создании Pull Request необходимо в описание вручную указать данные из METEOR (MT#ID или ссылка на задачу, ранее скопированная из METEOR).

Статусы Pull Request на вкладке "**GitHub**" в METEOR обновляются автоматически.

### Создать ветку с пустым коммитом

Из-за ограничения в один коммит или если есть необходимость создавать ветку как можно раньше, в меню «**Git-сниппеты**» можно создать пустой коммит. По кнопке «**Создать ветку с пустым коммитом**», который создаст ветку и добавит в неё пустой коммит с помощью одной команды.

<figure><img src="../../.gitbook/assets/image (1157).png" alt=""><figcaption></figcaption></figure>

