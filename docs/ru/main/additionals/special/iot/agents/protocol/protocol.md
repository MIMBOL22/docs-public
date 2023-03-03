Протокол общения агента с платформой состоит из следующего набора действий:

- получение конфигурации агентом из платформы;
- отправка агентом данных от устройств на платформу;
- выполнение полученных агентом команд из платформы;
- отправка агентом логов в платформу.

## Получение конфигурации

Конфигурация агента имеет уникальную версию, которая монотонно возрастает при изменении метаинформации агента, либо одного из подключенных к нему устройств.

При первом запуске агент автоматически получает последнюю версию конфигурации из шлюза платформы. В дальнейшем обновление конфигурации агента активируется с помощью команды.

Пример команды:
```bash
agent_tag/$state/$config/$version = new_version
```

После получения и применения конфигурации, агент рапортует в платформу текущую версию конфигурации и время обновления в специальные системные подтэги типа `state $state/$config/$version $state/$config/$updated_at`.

На основе разницы между версией конфигурации агента в метаинформации и версией, которую рапортует агент, платформа и пользователь могут понять, находится ли на агенте последняя конфигурация или требуется отправка команды на обновление.

## Отправка данных

Агент отправляет данные на платформу:

1. Маппинг показаний устройств на соответствующие тэги типа `event` и `state`.
2. Свой статус, а также о статусе всех подключенных устройств в тэги `$state/$status`.

Если связь с платформой оборвалась, агент буферизирует получаемые данные для отправки на платформу после восстановления связи.

## Выполнение команд

Агент должен поддерживать получение команд из платформы.

Команда может быть адресована:

- агенту;
- устройству подключенному к агенту.

Адресат команды вычисляется по переданным в команде тэгам, в чьем поддереве тэгов находятся переданные тэги. Одна команда может быть адресована только одному агенту или устройству.

Команда может содержать произвольный набор новых значений для любых тэгов типа `state` с полем
`properties.readonly = false` из поддерева тэгов целевого агента/устройства.

Есть два вида статусов команды:

1. Платформенные:

- `new` — команда была только что создана в Digital Twins.
- `sending` — команда была взята в работу в Peons.
- `sent` — команда была отправлена на передачу агенту в HTTP Gateway или MQTT Gateway.
- `failed` — отправка команды по каким-то причинам не удалась. Подробности в поле `reason`.

2. Статусы, которые обязан рапортовать агент:

- `received` — команда была получена агентом.
- `done` — команда успешно завершена.
- `skipped` — команда была по каким то причинам пропущена агентом. Например, при получении сразу нескольких команд на обновление конфигурации агент может выполнить только последнюю команду, а остальные перевести в `skipped`, заполнив поле `reason`).
- `failed` — агенту не удалось выполнить команду, подробные причины должны быть указаны в поле reason.

По результатам выполнения команды агент должен отчитаться о статусе команды в платформу через специальное API, послав статус команды `done` или `failed` с описанием возникшей ошибки в поле `reason`.

Этот протокол описывает лишь транспорт для передачи команд от платформы к агенту, реализация выполнения этих команд остается на усмотрение агента.

## Отправка логов

Протокол поддерживает отправку агентом произвольных логов в виде произвольной строки. При этом платформа может ограничивать количество принимаемых логов с агента в единицу времени.

Логи могут содержать информацию о функционировании:

- агента;
- подключенных устройств.

Полученные логи доступны для просмотра на странице «Логирование» в административной консоли платформы.

## Техническая спецификация

Протокол агента может работать как только поверх HTTP(S), так и поверх связки HTTP(S) + MQTT.

### Credentials

Логин агента формируется по шаблону `{ client_id }_{ agent_id }`.
Пароль берется из поля token агента.

### HTTP(S)

HTTP API расположено [здесь](../../../../api/api-iot/public-api/api-devices/http-api).

Для авторизации агента в HTTP API используется Basic authentication.
При подключении к платформе только по протоколу HTTP(S) платформа не может напрямую пересылать команды агенту, поэтому агент обязан периодически опрашивать апи платформы для получения команд на выполнение.

Данное описание может быть неполным/неточным, для просмотра актуальной спецификации API перейдите по [ссылке](../../../../api/api-iot/public-api).

- `GET /v1/agents/config` — эндпоинт для получения конфигурации, вызывается с параметром version=latest при бутстрапе агента для получения начальной конфигурации, а также с указанной в команде версией для обновления конфигурации по
пришедшей команде.
- `POST /v1/events` — эндопоинт для отправки данных в платформу, принимает массив значений вида `tag_id=value`.
- `POST /v1/logs` — эндпоинт для отправки логов в платформу, принимает массив значений вида
`timestamp=timestam_with_microsends`, `msg=string`.
- `GET /v1/commands` — эндпоинт для получения команд на выполнение. Данный эндпоинт необходимо периодически вызывать для получения новых команд на выполнение. Данный эндопоинт будет всегда возвращать список всех активных команд.
- `PATCH /v1/agents/{ agent_id }/commands/{command_id}/status` — эндпоинт для перевода взятой команды агента в конечный статус, принимает объект вида `status=received/done/failed/skipped, reason=optional_string_mesage_for_failed_or_skipped_status`.
- `PATCH /v1/devices/{ device_id }/commands/{command_id}/status` - эндпоинт для перевода взятой команды устройства в конечный статус, принимает объект вида `status=received/done/failed/skipped, reason=optional_string_mesage_for_failed_or_skipped_status`.
- `GET /v1/devices/{device_id}/config/{version}` — эндпоинт для получения конфигурации, которую необходимо физически применить на подключенное устройство в рамках выполнения команды.

### HTTP(S) + MQTT

При подключении агента к платформе через связку протоколов HTTP(S) + MQTT платформа может напрямую коммуницировать с агентом и отправлять ему команды без необходимости постоянного опроса http api.

### HTTP(S)

В протоколе на базе MQTT отсутствует поддержка следующих операций:

- `GET /v1/agents/config`
- `GET /v1/devices/{device_id}/config/{version}`

### MQTT

#### Отправка событий

Агент должен отправлять данные в топик `iot/event/fmt/json` с QOS=1 в следующем формате:

```json
  {
  "tags": [
    {
      "id": ..., // id конечного тэга, который представляет собой датчик
      "value": ..., // значение
      "timestamp": ... // timestamp in microseconds
    },
    ...
  ]    
}  
```

Например, чтобы послать сообщение для тэга с id=10 со значением '100', необходимо опубликовать
сообщение:
```json
  {
    "tags": [
      {
        "id": 10,
        "value": 100,
        "timestamp": 1
      }
    ]    
  }    
```

#### Команды

Для получения команд от платформы агент должен быть подписан на топик вида `iot/cmd/agent/+/fmt/json`, вместо одноуровневого `wildcard`. А еще должен стоять уникальный id клиента. Сообщение с командами публикуется с флагом `retain=1`, что позволяет клиенту гарантированно получить последнее сообщение с командами. Например, чтобы подписаться на команды для агента с id=1, необходимо подписаться на топик `iot/cmd/agent/1/fmt/json`.

В сообщении всегда собраны все активные команды для агента.

Команды имеют следующий формат:
```json
  {
      "command": {
        "id": "...", // command id
        "tags": [
          {
            "id": ..., // tag to change
            "value": ... // new tag value
          },
          ... 
        ],
        "timestamp": ... // timestamp in microseconds
      }, // active command for agent if any
      "devices": [
        {
          "device_id": 1,
          "command": {
             "id": "...", // command id
             "tags": [
               {
                 "id": ..., // tag to change
                 "value": ... // new tag value
               },
               ... 
             ],
             "timestamp": ... // timestamp in microseconds
          }
        }
      ] // active commands for devices if any
  }
```

Агент должен сообщать статус своей команды в отдельный топик вида `iot/cmd/agent/+/status/fmt/json` с QOS=1 сообщениями вида:
```json
  {
    "id": "...", // command id
    "status": "...", // skipped | received | failed | done
    "reason": "...", // optional field for failed status
    "timestamp": ... // timestamp in microseconds
  } 


Агент должен сообщать статусы команд для устройств в отдельные топики вида `iot/cmd/device/+/status/fmt/json` с QOS=1 сообщениями вида:
``` json
  {
    "id": "...", // command id
    "status": "...", // skipped | received | failed | done
    "reason": "...", // optional field for failed status
    "timestamp": ... // timestamp in microseconds
  } 
```

Поддерживаемые статусы команд:

- received — команда получена агентом/устройством.
- failed — агент/устройство не смогли применить команду, дополнительно в поле `reason` должна быть указан причина.
- done — агент/устройство успешно применили команду.

#### Логирование

Для отправки произвольных логов в платформу агент должен использовать топик `iot/log/fmt/json` с QOS=1 в формате:

```json
[
  {
    "msg": "...",
    "timestamp": ... // timestamp in microseconds
  }
]
```

## Общие команды

### Обновление конфигурации агента

Данная команда обязательна к реализации всеми агентами. Она всегда содержит набор значений для следующих тэгов агента:

- `$state/$config/$version`

По получении этой команды агент обязан получить конфигурацию указанной в команде версии из соответствующего эндпоинта HTTP API.

По успешному выполнению команды агент обязан отправить в платформу новые значения для следующих тэгов агента:

- `$state/$config/$version`
- `$state/$config/$updated_at`

### Обновление конфигурации на устройстве

Эта команда необязательна к реализации агентом и может быть применена только к устройству, которое поддерживает конфигурирование агентом.

Признаком того, что устройство может быть сконфигурировано агентом, является флаг `properties.readonly` выставленный в `false` у тэга устройства `$state/$config/$version`.

Команда всегда содержит набор значений для следующих тэгов устройства:

- `$state/$config/$version`

По получении данной команды агент обязан получить конфигурацию для устройства указанной в команде версии из соответствующего эндпоинта HTTP API.

Реализация обновления конфигурации устройства полностью отдается на откуп агенту.

По успешному выполнению команды агент обязан отправить в платформу новые значения для следующих тэгов устройства:

- `$state/$config/$version`
- `$state/$config/$updated_at`

### Обновление прошивки на агенте

Данная команда необязательна к реализации агентом и может быть применена только к агенту, который поддерживает автоматическое обновление прошивки.

Признаком того, что агент может обновлять свою прошивку является флаг properties.readonly выставленный в `false` у тэга агента `$state/$firmware/$source`.

Данная команда всегда содержит набор значений для следующих тэгов агента:

`$state/$firmware/$source` — источник, например, http url для скачивания новой прошивки.

Также команда может содержать следующие необязательные тэги:

- `$state/$firmware/$vendor`
- `$state/$firmware/$version`

Реализация обновления прошивки полностью отдается на откуп агенту.

По успешному выполнению команды агент обязан отправить в платформу новые значения для следующих тэгов агента:

- `$state/$firmware/$source`
- `$state/$firmware/$updated_at`

Еще агент может заполнить следующие тэги в зависимости от содержания команды/особенностей реализации:

- `$state/$firmware/$vendor`
- `$state/$firmware/$version`

### Обновление прошивки на устройстве

Данная команда необязательна к реализации агентом и может быть применена только к устройству, которое поддерживает автоматическое обновление прошивки.

Признаком того, что агент может обновлять прошивку у устройства является флаг `properties.readonly`, выставленный в `false` у тэга устройства `$state/$firmware/$source`.

Эта команда всегда содержит набор значений для следующих тэгов устройства:

- `$state/$firmware/$source` — источник, например, http url для загрузки новой прошивки.

Также команда может содержать следующие необязательные тэги:

- `$state/$firmware/$vendor`
- `$state/$firmware/$version`

Реализация обновления прошивки на устройстве полностью отдается на откуп агенту.
По успешному выполнению команды агент обязан отправить в платформу новые значения для следующих тэгов устройства:

- `$state/$firmware/$source`
- `$state/$firmware/$updated_at`

Еще агент может заполнить следующие тэги устройства в зависимости от содержания команды/особенностей реализации:

- `$state/$firmware/$vendor`,
- `$state/$firmware/$version`.