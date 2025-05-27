---
description: >-
  METEOR предоставляет интеграцию с Merge Requests в GitLab, чтобы тесно связать
  разработку программного обеспечения с планированием и описанием задач проекта
---

# Интеграция с GitLab

## Отображение в задаче

1. Вкладка "**GitLab**" - будет отображать следующие данные из gitLab:

* **Issues** в которых была упомянута задача METEOR с соответствующим статусом (Открыто, Закрыто).&#x20;
* **Merge Requests (MR)**, связанные с задачей, включая их статусы (Открыт, Объединено, Закрыт). MR и задачи связаны в соотношении n:m, поэтому задача может быть связана с несколькими MR, а MR — с несколькими задачами;
* Текущее состояние выполнения **Pipline** для Merge Request (Created, Running, Waiting, Failed, Pending, Canceled, Skipped, Manual, Scheduled, Success).

<figure><img src="../../.gitbook/assets/image (1031).png" alt=""><figcaption></figcaption></figure>

2. Вкладка "**История**" - будет отображать изменения по MR и Issues (комментарии, обновления статусов):

<figure><img src="../../.gitbook/assets/image (1032).png" alt=""><figcaption></figcaption></figure>

## Настройка интеграции

Необходимо настроить METEOR и GitLab, чтобы интеграция заработала.

### METEOR

1.  Создайте специальную [роль](../polzovateli-zapolniteli-i-gruppy/roli-i-prava/roli.md), в которой будут как минимум два права:

    * "Просмотр задач";
    * "Добавление комментариев".

    &#x20;_(Администрирование -> Пользователи и права -> Роли -> Конкретная роль -> раздел "Задачи")_

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXd4uZjGBCeGuhv46OW2favKAy07FMOPAY62xKLC5514b2UPS-XTvGldAygZkM8d-y8PTU6L752khHil22RWtnAWK_B-nB3Pzmjsx_RCkz6scq6FFoDx9Wq6hR7OInI1HBitx5-qLg?key=yvs9BW-M6yN5IDhNKDHndYGb" alt=""><figcaption></figcaption></figure>

2.  Создайте [пользователя](../polzovateli-zapolniteli-i-gruppy/polzovateli.md) для интеграции

    * &#x20;назначьте ему созданную роль;
    * добавьте этого пользователя во все проекты, где нужна интеграция с GitLab.

    _(Администрирование -> Пользователи и права -> Пользователи)_

<figure><img src="https://lh7-rt.googleusercontent.com/docsz/AD_4nXcbQFQzgftMFkknliuIF9SjiDgb9wNjxB2YTNLpwnzAyrbgQlaIiv4ZKi8fSmTNLA0V405b3wzYoT0Lhxea7kq2SqftS498BIidLMTBX-FqAg-bpZVoTeDdbkHscGq6j8fb6mRngw?key=yvs9BW-M6yN5IDhNKDHndYGb" alt=""><figcaption></figcaption></figure>

3. Сгенерируйте API-токен для этого пользователя (он понадобится вам на стороне GitLab). Для генерации токена необходимо:
   * войдите в систему под учётной записью нового пользователя.
   * перейдите в **Профиль** (нажмите на аватарку в правом верхнем углу и выберите Профиль).
   * далее "**Токены доступа**".
   * нажмите на кнопку "+ Токен API".

{% hint style="info" %}
**Важно!** Обязательно скопируйте сгенерированный токен и надёжно сохраните его. Токен нельзя будет посмотреть позже!
{% endhint %}

4. Активируйте модуль GitLab в [настройках проекта](../../rukovodstvo-polzovatelya/proekty/nastroiki-proekta.md#moduli-proekta) (_Настройки проекта -> Модули)_.
5. Выдайте права на просмотр вкладки "**GitLab**" нужным [ролям](../polzovateli-zapolniteli-i-gruppy/roli-i-prava/):
   * "Показывать содержимое GitLab".

### GitLab

1.  Добавьте Webhook в каждом репозитории:

    * перейдите в Настройки -> Webhook;
    * нажмите "Добавить новый webhook".

    <figure><img src="../../.gitbook/assets/image (1156).png" alt="" width="563"><figcaption></figcaption></figure>

Нужно настроить URL-адрес, который указывает на конечную точку (Endpoint) webhook GitLab на вашем сервере METEOR (/op/webhooks/gitlab).

Вам понадобится Токен API, который ранее получили в METEOR. Добавьте его в URL в качестве простого параметра GET с именем key. В итоге URL должен выглядеть примерно так:

https://mycompany.u-meteor.ru/op/webhooks/gitlab?key=4221687468163843

2. **Примечание:** для событий, которые должны запускать webhook, выберите следующие:

* Push-события (все ветви);
* Комментарии;
* Issues;
* Merge Requests;
* Pipline.

{% hint style="info" %}
**Примечание:** если вы находитесь в локальной сети, вам может потребоваться разрешить запросы к локальной сети в вашем экземпляре GitLab.
{% endhint %}

3. Мы рекомендуем вам включить проверку SSL перед добавлением webhook.



Теперь интеграция настроена с обеих сторон, и вы можете её использовать!

## Использование интеграции с GitLab

### Создание Merge Requests (MR)

1.  Создайте ветку.

    * В задаче в METEOR во вкладке **GitLab** нажмите кнопку "**Git-сниппеты**", скопируйте имя ветки, нажав соответствующую кнопку:

    <figure><img src="../../.gitbook/assets/image (1035).png" alt=""><figcaption></figcaption></figure>

    * Откройте GitLab и создайте ветку, введя имя которое скопировали из задачи:

<figure><img src="../../.gitbook/assets/Снимок экрана 2025-05-05 в 22.00.01.png" alt=""><figcaption></figcaption></figure>

Таким образом, все ветки будут иметь общий шаблон, а поскольку в названии ветки указан идентификатор задачи, будет легко увидеть связь между MR и задачей, просмотрев список Merge Requests в GitLab.

2.  Добавьте коммит с автоматически сгенерированным описанием.

    * Используйте поле "**Описание коммита**" из меню «**Git-сниппеты**» на вкладке "**GitLab**":

    <figure><img src="../../.gitbook/assets/image (1036).png" alt=""><figcaption></figcaption></figure>

    * Создайте коммит в gitlab, вставив скопированное описание коммита:

    <figure><img src="../../.gitbook/assets/Снимок экрана 2025-05-05 в 22.24.56.png" alt=""><figcaption></figcaption></figure>

    * После внесения изменений вы можете создать MR. Заголовок и комментарий со ссылкой на соответствующую задачу METEOR будут заполнены автоматически, в случае если в ветке есть только один коммит:

<figure><img src="../../.gitbook/assets/Снимок экрана 2025-05-05 в 22.26.04.png" alt=""><figcaption></figcaption></figure>

3. Из-за ограничения в один коммит или если есть необходимость создавать ветку как можно раньше, в меню «**Git-сниппеты**» можно создать пустой коммит. По кнопке «**Создать ветку с пустым коммитом**», который создаст ветку и добавит в неё пустой коммит с помощью одной команды.

<figure><img src="../../.gitbook/assets/image (1037).png" alt=""><figcaption></figcaption></figure>

### Связь Merge Requests (MR) с задачами METEOR

Для того, чтобы связать MR с задачей METEOR, в описании MR или в комментарии должна быть:

* ссылка на задачу,  ранее скопированная из METEOR;
* или укажите «МТ#ID», где ID - это идентификатор задачи METEOR, в описании. Например, MT#50. Данные о MR подтянутся в METEOR и будут отображаться на вкладке "**GitLab**".

GitLab будет использовать сообщение первого коммита в качестве описания MR (при условии, что коммит только один)

{% hint style="info" %}
**Обратите внимание**, что «МТ#ID» чувствителен к регистру. «мт#ID» - не будет работать.
{% endhint %}

{% hint style="info" %}
Используйте в MR «РР#» вместо «МТ#», чтобы синхронизировать MR без комментариев.



Если вы хотите опубликовать только один комментарий из закрытого МР (имеет упоминание «РР#»), вы можете использовать «МТ#» непосредственно в этом комментарии. Таким образом, только этот конкретный комментарий будет опубликован в METEOR, а остальные комментарии останутся закрытыми.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (1038).png" alt=""><figcaption></figcaption></figure>

Описание ветки можно изменить до создания Merge Request, что позволяет дополнительно описать изменения. В описание Merge Request также можно включить ссылки на дополнительные задачи METEOR.

&#x20;В GitLab MR будет  выглядеть следующим образом.&#x20;

Нажмите на "Создать MR":

<figure><img src="../../.gitbook/assets/Снимок экрана 2025-05-05 в 22.31.01.png" alt=""><figcaption></figcaption></figure>

Если статус MR изменится, это соответствующим образом отразится в задаче METEOR. Пожалуйста, ознакомьтесь с примером ниже.

<figure><img src="../../.gitbook/assets/image (1040).png" alt=""><figcaption></figcaption></figure>

Текущее состояние выполнения Pipline для MR в METEOR отображается справа:

<figure><img src="../../.gitbook/assets/image (1135).png" alt=""><figcaption></figcaption></figure>

### Проблемы со ссылками

Интеграция METEOR с GitLab позволяет связывать задачи GitLab напрямую с задачами METEOR.

Изначально, если Issues и Merge Requests ещё не было, вы увидите следующее сообщение на вкладке GitLab.

<figure><img src="../../.gitbook/assets/image (1039).png" alt=""><figcaption></figcaption></figure>

Вы можете создать новую задачу в GitLab или отредактировать уже существующую, введя код МТ#ID в заголовок или описание задачи. После сохранения изменений или создания задачи в GitLab, она будет отображаться на вкладке "**GitLab**" в METEOR.
