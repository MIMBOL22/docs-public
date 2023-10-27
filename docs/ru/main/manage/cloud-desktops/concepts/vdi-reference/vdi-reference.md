Основные понятия сервиса Cloud Desktop:

- **Рабочий стол** — виртуальное рабочее место с установленной на нем ПО. Рабочий стол создается в рамках пула рабочих столов и назначается администратором сервиса.
- **Пул рабочих столов** — объединение нескольких рабочих столов, которые используют общие вычислительные ресурсы. Через пул рабочих столов можно задавать общие настройки для рабочих столов. Рабочие столы в этом пуле могут быть созданы из разных шаблонов в зависимости от выполняемых задач.
- **Шаблон рабочего стола** — шаблон для создания ВМ и рабочих столов. Для ОС рабочего стола такого шаблона должен быть установлен и настроен компонент сервиса виртуализации.
- **Служба каталогов** — комплекс ПО, предназначенный для иерархического хранения, организации и предоставления доступа к информации. Взаимодействие с такими службами выполняется через протоколы, самый распространенный — LDAP. Сервис Cloud Desktop поддерживает интеграцию со службами каталогов Active Directory (AD) и OpenLDAP.