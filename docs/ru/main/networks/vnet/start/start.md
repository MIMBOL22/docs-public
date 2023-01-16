Быстрый старт поможет начать работу с сервисом и познакомиться с его возможностями.

Пройдя все шаги быстрого старта, вы:

1. Настроите доступ в интернет.
1. Организуете базовую сетевую связность нескольких виртуальных машин.
1. Научитесь назначать группы правил файервола.

## Шаг 1. Создайте сеть и подсеть

1. Перейдите в [личный кабинет](https://mcs.mail.ru/app/) VK Cloud.
1. Перейдите в раздел **Виртуальные сети** → **Сети**.
1. Нажмите кнопку **Создать**.
1. Задайте имя сети, например, `test-network`.
1. Доступ в интернет: включен.
1. Маршрутизатор: Создать новый.
1. Нажмите **Добавить сеть**.

## Шаг 2. Создайте несколько виртуальных машин

Создайте виртуальную машину с выходом в интернет:

1. Перейдите в [личный кабинет](https://mcs.mail.ru/app/) VK Cloud.
1. Перейдите в раздел **Облачные вычисления** → **Виртуальные машины**.
1. Нажмите кнопку **Добавить**.
1. На шаге «Конфигурация»:

    1. Задайте имя виртуальной машине, например, `test-vm1`.
    1. Другие настройки задайте в зависимости от ваших требований или оставьте без изменений.

1. Нажмите **Следующий шаг**.
1. На шаге «Настройки сети»:

    1. Сети: Внешняя сеть (ext-net).
    1. Остальные настройки оставьте без изменений.

1. Нажмите **Следующий шаг**.
1. На шаге «Настройка резервного копирования» оставьте настройки без изменений.
1. Нажмите **Создать инстанс**.

Создание виртуальной машины может занять некоторое время, после чего она появится в списке.

Создайте вторую виртуальную машину:

1. Перейдите в [личный кабинет](https://mcs.mail.ru/app/) VK Cloud.
1. Перейдите в раздел **Облачные вычисления** → **Виртуальные машины**.
1. Нажмите кнопку **Добавить**.
1. На шаге «Конфигурация»:

    1. Задайте имя виртуальной машине, например, `test-vm2`.
    1. Другие настройки задайте в зависимости от ваших требований или оставьте без изменений.

1. На шаге «Настройки сети»:

    1. Сети: `test-network`.
    2. Ключ виртуальной машины: Создать новый ключ.
    3. Настройки Firewall: default, ssh.
    4. Назначить внешний IP-адрес: отключить.

2. Нажмите **Следующий шаг**.
3. На шаге «Настройка резервного копирования» оставьте настройки без изменений.
4. Нажмите **Создать инстанс**.

На ваш компьютер загрузится файл с ключ от виртуальной машины.

Создайте третью виртуальную машину:

1. Перейдите в [личный кабинет](https://mcs.mail.ru/app/) VK Cloud.
1. Перейдите в раздел **Облачные вычисления** → **Виртуальные машины**.
1. Нажмите кнопку **Добавить**.
1. На шаге «Конфигурация»:

    1. Задайте имя виртуальной машине, например, `test-vm3`.
    1. Другие настройки задайте в зависимости от ваших требований или оставьте без изменений.

1. На шаге «Настройки сети»:

    1. Сети: `test-network`.
    1. Ключ виртуальной машины: Создать новый ключ.
    1. Настройки Firewall: default, ssh.
    1. Назначить внешний IP-адрес: отключить.

1. Нажмите **Следующий шаг**.
1. На шаге «Настройка резервного копирования» оставьте настройки без изменений.
1. Нажмите **Создать инстанс**.

Дождитесь завершения создания виртуальной машины.

## Шаг 3. Создайте группу правил

1. Нажмите **Добавить**.
1. Задайте имя группы правил, например, `test-icmp`.
1. Нажмите **Создать группу**.
1. В блоке Входящий трафик создайте правила для управления трафиком:

    1. Нажмите **Добавить правило**.
    1. Тип: ICMP.
    1. Удаленный адрес: Все IP-адреса.

1. Нажмите кнопку **Сохранить правило**.
1. В блоке Исходящий трафик создайте правила для управления трафиком:

    1. Нажмите **Добавить правило**.
    1. Тип: ICMP.
    1. Удаленный адрес: Все IP-адреса.

1.  Нажмите кнопку **Сохранить правило**.

## Шаг 4. Назначьте группу правил

Чтобы передавать и принимать трафик, назначьте ВМ группу безопасности. Для ранее созданных ВМ примените следующие настройки:

1. Перейдите в [личный кабинет](https://mcs.mail.ru/app/) VK Cloud.
1. Перейдите в раздел **Облачные вычисления** → **Виртуальные машины**.
1. Нажмите на меню в строке виртуальной машины.
1. Выберите из списка меню **Настройки firewall**.
1. Найдите в списке группу правил, созданную на шаге 3.
1. Нажмите **Применить** в строке с группой правил.
1. Нажмите **Подтвердить**.

<info>

Успешное выполнение данного шага гарантирует наличие ICMP-связности между созданными ВМ. Сетевая связность будет работать, даже если у одной ВМ из назначенной группы правил отсутствует плавающий IP-адрес.

</info>

## Шаг 4. Подключитесь к ВМ по ssh

На прошлом шаге вы создали ключ от виртуальной машины, который был сохранен на ваш компьютер. Найдите файл в загрузках, он понадобится для подключения к ВМ.

1. Откройте терминал.
1. Перейдите в загрузки:

   ```
   cd ~/Downloads/
   ```

1. Сделайте ключ доступным только для текущего пользователя:

    ```
    chmod 400 <путь к ключу>
    ```

1. Подключитесь к инстансу по протоколу SSH:

    ```
    ssh -i <путь к ключу> centos@10.0.0.6
    ```

## Шаг 5. Проконтролируйте использование ресурсов

Если вам больше не нужны созданные вами ресурсы, то удалите их.