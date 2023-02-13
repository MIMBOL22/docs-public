<!-- содержание этой статьи должно совпадать с быстрым стартом по личному кабинету; важно поддерживать актуальность обеих статей -->

## Регистрация в личном кабинете

1. Перейдите на [главную страницу VK Cloud](https://mcs.mail.ru) и нажмите кнопку **Регистрация** в правом верхнем углу.
1. В появившемся окне заполните поля:

    - **Корпоративный email**: укажите действующий адрес корпоративной почты.
    - **Пароль**: придумайте новый пароль.

    <warn>

    Минимальная длина пароля — 8 символов. Пароль должен содержать заглавные и строчные буквы латинского алфавита, а также цифры или символы: ``? ! ~ @ # $ % ^ & _ - + * = ; : , . / \ | ` [ ] { } ( )``

    </warn>

1. Нажмите кнопку **Создать аккаунт**.

Откроется главная страница личного кабинета VK Cloud. На указанную почту будет выслана ссылка для подтверждения учетной записи.

## Подтверждение учетной записи

Невозможно активировать сервисы и начать работу в личном кабинете без подтверждения учетной записи. Чтобы подтвердить свою учетную запись:

1. Откройте письмо от `noreply@mcs.mail.ru`.<!-- todo переделать шаг на "Откройте письмо с темой Тема письма.", когда выяснится тема письма-->

    <warn>

    Если письма нет во **Входящих**, проверьте папку **Спам**. Если письмо не пришло, запросите его повторно через личный кабинет.<!-- todo изменить на конкретный шаг при актуализации -->

    </warn>

1. Перейдите по ссылке из письма. Откроется личный кабинет VK Cloud с сообщением об успешном подтверждении учетной записи.

Отобразится структура сервисов личного кабинета.

## Активация сервисов

Чтобы сервисы в личном кабинете стали активны, привяжите к учетной записи номер телефона:

<!-- todo переписать инструкцию на реальные кнопки!!! -->

1. На [главной странице](https://mcs.mail.ru/app/main) личного кабинета введите номер телефона.

    <warn>

    Номер телефона может быть привязан только к одной учетной записи, использовать его повторно для другой учетной записи невозможно.

    </warn>

1. Введите код из СМС в одноименное поле.
1. Отправьте данные формы.

    В случае успешного подтверждения номера телефона появится сообщение о возможности активации сервисов.

1. Нажмите кнопку **Включить сервисы**.

## Активация доступа по API

Активируйте доступ по API, если будете работать с виртуальными ресурсами платформы не через личный кабинет (например, через OpenStackCLI или kubectl).

1. [Включите](/ru/base/account/account/security/2faon) двухфакторную авторизацию.
1. Нажмите на логин пользователя в правом верхнем углу [личного кабинета](https://mcs.mail.ru/app/) VK Cloud.
1. В выпадающем меню выберите **Настройки аккаунта**.
1. Перейдите на вкладку **Безопасность**.
1. В разделе **Доступ по API** нажмите кнопку **Активировать доступ по API**.

## Что дальше

- [Завершите](../corporate/) регистрацию ЮЛ.
- [Ознакомьтесь](../trial/) с пробным периодом использования платформы.
- [Посмотрите](/ru/base/account) возможности личного кабинета.