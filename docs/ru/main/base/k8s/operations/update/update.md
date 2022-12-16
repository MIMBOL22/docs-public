Если кластер использует не самую актуальную версию Kubernetes из [поддерживаемых](../../concepts/versions/version-support/), то его можно обновить до более новой версии Kubernetes.

<warn>

- При обновлении нельзя понизить версию Kubernetes.
- Обновить кластеры версий 1.16 и ниже можно только путем переноса резервной копии данных в новый кластер нужной версии, например, [с помощью Velero](../../use-cases/velero-backup).

</warn>

## Перед обновлением

1. Изучите [устройство процедуры обновления](../../concepts/update/).
1. Выполните резервное копирование кластера, который планируете обновить, например, с помощью Velero.
1. Разверните из резервной копии такой же кластер, как и тот, который планируется обновить. Проверьте с его помощью, что процедура обновления проходит без проблем: все данные и приложения кластера остаются доступны, приложения ведут себя так, как ожидается.
1. [Настройте порог](../manage-node-group#nastroit-parametry-obnovleniya) количества недоступных worker-узлов в группах.

## Выполните обновление

<tabs>
<tablist>
<tab>Личный кабинет</tab>
</tablist>
<tabpanel>

1. Перейдите в [личный кабинет](https://mcs.mail.ru/app/) VK Cloud.
1. Выберите проект и регион, где находится нужный кластер.
1. Перейдите в раздел **Контейнеры** → **Кластеры Kubernetes**.
1. Раскройте меню нужного кластера и выберите пункт **Обновить версию**.
1. В появившемся окне выберите нужную версию.
1. Ознакомьтесь с изменениями в версии.
1. Нажмите кнопку **Изменить версию**.

</tabpanel>
</tabs>