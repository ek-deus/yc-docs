---
title: Справочник аудитных логов {{ cloud-logging-full-name }} в {{ at-full-name }}
description: На этой странице приведен справочник событий сервиса {{ cloud-logging-name }}, отслеживаемых в {{ at-name }}.
---

# Справочник аудитных логов {{ at-full-name }}

В {{ at-name }} поддерживается отслеживание событий уровня конфигурации (Control Plane) для {{ cloud-logging-full-name }}. Подробнее см. [{#T}](../audit-trails/concepts/format.md).

Общий вид значения поля `event_type` (_тип события_):

```text
{{ at-event-prefix }}.audit.logging.<имя_события>
```

{% include [logging-events](../_includes/audit-trails/events/logging-events.md) %}