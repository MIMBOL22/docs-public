После запуска кластера группы безопасности настроены согласно данным из таблицы ниже.

<table><tbody><tr><td>Исходящий трафик</td><td>Без ограничений</td></tr><tr><td>Входящий и исходящий трафик между узлами кластера в рамках внутренней сети</td><td>Без ограничений</td></tr><tr><td>Входящий трафик на TCP-порт 8080 головного узла</td><td>Без ограничений, используется для доступа в интерфейс ADCM (авторизация по логину и паролю)</td></tr><tr><td>Входящий трафик на TCP-порт 22 головного узла</td><td>Без ограничений, используется для доступа по SSH (авторизация по SSH-ключу).</td></tr><tr><td>Входящий ICMP-трафик на головной узел</td><td>Без ограничений</td></tr><tr><td>Остальной трафик</td><td>Запрещен</td></tr></tbody></table>

<warn>

Внешний доступ к кластеру возможен через веб-интерфейс ADCM и SSH-доступ к Head-узлу.

</warn>

## Настройка доступа к веб-интерфейсу ADCM

<tabs>
<tablist>
<tab>Личный кабинет</tab>
</tablist>
<tabpanel>

1. [Перейдите](https://msk.cloud.vk.com/app/) в личный кабинет VK Cloud.
1. Перейдите в раздел **Большие данные** → **Кластеры**.
1. На шаге «Настройка узлов» создания кластера выберите опцию **Назначить внешний IP на Head-узел**.
1. На шаге указания пароля компонентов укажите пароль для входа в ADCM UI.
1. Дождитесь завершения развертывания кластера.
1. Откройте страницу нужного кластера, нажав на его имя.
1. Перейдите по адресу, указанному в **ADCM UI**. Откроется консоль ADCM.
1. Введите имя пользователя `admin` и пароль, указанный при создании кластера.

</tabpanel>
</tabs>

## Подключение к Head-узлу по SSH

<tabs>
<tablist>
<tab>Личный кабинет</tab>
</tablist>
<tabpanel>

1. [Перейдите](https://msk.cloud.vk.com/app/) в личный кабинет VK Cloud.
1. Перейдите в раздел **Большие данные** → **Кластеры**.
1. На шаге «Настройка узлов» создания кластера выберите опцию **Назначить внешний IP на Head-узел**.
1. Дождитесь завершения развертывания кластера. Сохраните SSH-ключ, сгенерированный при создании кластера.
1. Откройте страницу нужного кластера, нажав на его имя.
1. [Подключитесь к Head-узлу](/ru/base/iaas/service-management/vm/vm-connect/vm-connect-nix) по IP-адресу, указанному в **ADCM UI** по SSH-ключу.

</tabpanel>
</tabs>

## Подключение к Edge-узлу по SSH

<tabs>
<tablist>
<tab>Личный кабинет</tab>
</tablist>
<tabpanel>

1. [Перейдите](https://msk.cloud.vk.com/app/) в личный кабинет VK Cloud.
1. Перейдите в раздел **Большие данные** → **Кластеры**.
1. На шаге «Настройка узлов» создания кластера выберите опцию **Подключить Edge-узел**.
1. Укажите нужные параметры узла и выберите опцию **Назначить внешний IP на Edge-узел**.
1. Дождитесь завершения развертывания кластера. Сохраните SSH-ключ, сгенерированный при создании кластера.
1. Откройте страницу нужного кластера, нажав на его имя.
1. [Подключитесь к Edge-узлу](/ru/base/iaas/service-management/vm/vm-connect/vm-connect-nix) по SSH-ключу.

</tabpanel>
</tabs>

## Настройка доступа к веб-интерфейсам компонентов кластера

Чтобы настроить доступ к веб-интерфейсам компонентов в сети, воспользуйтесь одним из способов:

<tabs>
<tablist>
<tab>Настройте VPN-доступа</tab>
<tab>Настройте группы безопасности</tab>
</tablist>
<tabpanel>

1. [Создайте](/ru/networks/vnet/operations/manage-net#sozdanie_seti) новую внутреннюю сеть и [маршрутизатор](/ru/networks/vnet/operations/manage-router#dobavlenie_marshrutizatora).
1. Создайте кластер, указав созданную сеть.
1. [Настройте VPN-подключение](/ru/networks/vnet/use-cases/vpn-tunnel) к сервисам VK Cloud.

</tabpanel>
<tabpanel>

[Настройте](/ru/networks/vnet/operations/secgroups) группы безопасности нужным для вас образом, подробнее в статье [Ограничение трафика](/ru/networks/vnet/concepts/traffic-limiting).

</tabpanel>
</tabs>