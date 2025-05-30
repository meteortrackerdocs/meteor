---
icon: square-v
---

# Общие настройки

## Настройки аутентификации <a href="#authentication-settings" id="authentication-settings"></a>

Чтобы изменить системные настройки аутентификации, перейдите в раздел "**Администрирование**" в верхней части экрана:

<figure><img src="../../.gitbook/assets/image (979).png" alt=""><figcaption></figcaption></figure>

В разделе **Аутентификация** выберем пункт "**Общие**":

<figure><img src="../../.gitbook/assets/image (907).png" alt=""><figcaption></figcaption></figure>

Вы можете настроить следующее в настройках аутентификации:

### Общие настройки аутентификации

1. Разрешить доступ без авторизации. По умолчанию доступ к METEOR без авторизации отключен.&#x20;

{% hint style="info" %}
Если включить опцию «**Разрешить доступ без авторизации**», доступ к вашему экземпляру METEOR станет возможен без входа в систему. Доступность отдельных проектов зависит от параметра «Публичный» в [настройках проекта](../../rukovodstvo-polzovatelya/proekty/nastroiki-proekta.md). Права неавторизованных пользователей определяются ролью "[Аноним](../polzovateli-zapolniteli-i-gruppy/roli-i-prava/opisanie-predustanovlennykh-rolei.md#rol-anonim)".
{% endhint %}

2\. Самостоятельная регистрация пользователей. Выберите один из вариантов регистрации:

* **Активация по электронной почте** - требуется подтверждение от пользователя.
* **Активацией учетной записи администратором** - администратор вручную активирует новые учетные записи.
* **Автоматическая активация учётной записи** - учётная запись активная сразу после регистрации.

{% hint style="info" %}
Самостоятельная регистрация распространяется только на внутренних пользователей (с входом по имени пользователя и паролю). При интеграции с LDAP, SAML или OpenID Connect используйте их настройки для управления созданием учетных записей.
{% endhint %}

3. Использовать email как логин. Следует ли использовать адрес электронной почты в качестве логина для входа.
4. Задайте срок действия письма с кодом активации для новых пользователей.

<figure><img src="../../.gitbook/assets/image (908).png" alt=""><figcaption></figcaption></figure>

### Политика безопасности паролей

1. Задайте минимальную длину пароля.
2. Укажите требования к надежности пароля: необходимо включение классов символов (заглавные буквы, строчные буквы, спецсимволы, числовые символы).
3. Определите минимальное количество обязательных классов символов, оно не должно превышать количество отмеченных вами необходимых для включения классов символов (предыдущая настройка).\
   \
   Например, вы отметили, что в пароле должны быть все классы символов, но минимальное количество классов указали 2. Будут допустимы пароли, включающие **любые** 2 класса символов.&#x20;
4. Укажите срок, через который пароль должен быть обязательно изменен пользователем.
5. Укажите количество последних паролей, которые запрещено использовать пользователю повторно при установке нового пароля.
6. Включите или отключите функцию «Восстановить пароль» для восстановления пароля через электронную почту.

<figure><img src="../../.gitbook/assets/image (909).png" alt=""><figcaption></figcaption></figure>

### Автоматическая блокировка пользователя

1. Установите лимит неудачных попыток входа (некорректный логин и/или пароль), после которого пользователь будет временно заблокирован.&#x20;
2. Определите продолжительность блокировки после превышения лимита попыток.&#x20;

<figure><img src="../../.gitbook/assets/image (910).png" alt=""><figcaption></figcaption></figure>

### Авторизация

1. Включите опцию сохранения авторизации, чтобы пользователь оставался в системе даже после закрытия браузера. Когда эта функция активирована, на экране входа появится возможность «**Оставаться в системе**».&#x20;
2. Настройте срок действия сеанса при отсутствии активности.&#x20;

{% hint style="info" %}
При включении функция "**Сеанс истекает**", отменяется действие функции "**Сохранить авторизацию**".
{% endhint %}

<figure><img src="../../.gitbook/assets/image (911).png" alt=""><figcaption></figcaption></figure>

### Другие настройки аутентификации

Включите логирование запросов с указанием имени пользователя, логина и адреса электронной почты.

<figure><img src="../../.gitbook/assets/image (873).png" alt=""><figcaption></figcaption></figure>

**Сохраните** внесенные изменения.
