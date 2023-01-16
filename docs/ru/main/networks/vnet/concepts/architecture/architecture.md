## Чем оперирует сервис

Сервис виртуальных сетей состоит из двух слоев:

1. [Программно-определяемая сеть](https://ru.wikipedia.org/wiki/Программно-определяемая_сеть) (software-defined network, SDN).
1. [Виртуализованные сетевые функции](https://ru.wikipedia.org/wiki/Виртуализация_сетевых_функций) (Network Function Virtualization, NFV).

На слое SDN сервис позволяет работать с базовыми сущностями:

- Сетями.
- Подсетями.
- Портами. Порт OpenStack эквивалентен комбинации:

  - Порта виртуального коммутатора (switch), подключенного к виртуальной сетевой карте.
  - IP-адреса из некоторой подсети, назначенного этой сетевой карте.

На слое NFV с помощью SDN реализуются следующие сущности:

- Маршрутизаторы для связи нескольких приватных сетей между собой и организации доступа в интернет.
- Балансировщики нагрузки для распределения входящего трафика по нескольким экземплярам сервисов платформы VK Cloud.
- Файервол с группами правил для ограничения трафика к определенным сервисам платформы. Группы правил назначаются на уровне отдельных портов.
- VPN для связи удаленной сетевой инфраструктуры с сетью, созданной в рамках платформы.

## Используемые SDN

Для работы со объектами SDN и NFV используется Openstack Neutron API. Расположенные на хостах агенты получают запросы через API и создают или изменяют объекты, нужные для работы SDN или NFV.

В качестве SDN платформа VK Cloud использует:

- Openstack Neutron.

  Он эффективен при работе в небольшой сети, но в сетях большого масштаба (тысячи и десятки тысяч портов) могут возникать проблемы:
  
  - C синхронизацией работы множества агентов, которые не хранят свое состояние.
  - С большим количеством событий из-за переусложненного уровня передачи данных (dataplane).
  - C потерей этих событий в очереди RabbitMQ из-за их большого количества. Эта очередь выполняет роль транспорта для передачи событий сервисов.

- Sprut, SDN собственной разработки VK Cloud, полностью совместимый с Openstack Neutron API.

  <info>

  Sprut находится на этапе beta-тестирования. Для получения доступа к новому сервису SDN обратитесь в [службу технической поддержки](../../../../../contacts).

  </info>

  Он лишен перечисленных недостатков Openstack Neutron. Sprut обеспечивает стабильную работу сетей и сетевых функций поверх этих сетей на больших масштабах. Его преимущества:

  - Вместо очереди сообщений используется HTTP REST API.
  - Все агенты хранят свое текущее состояние. Агенты получают от SDN-контроллера целевое состояние, в котором они должны быть, и приводят свое состояние к требуемому.
  - Выбрана многоуровневая архитектура, позволившая упростить уровень передачи данных и настраивать его более гибко.

  Подробнее о Sprut рассказано в докладе [Как выбрать SDN для высоких нагрузок](https://www.youtube.com/watch?v=iqSXRZ8b_bk).