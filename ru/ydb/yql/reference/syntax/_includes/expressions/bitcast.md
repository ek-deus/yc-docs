---
sourcePath: ru/ydb/ydb-docs-core/ru/core/yql/reference/yql-docs-core-2/syntax/_includes/expressions/bitcast.md
sourcePath: ru/ydb/yql/reference/yql-docs-core-2/syntax/_includes/expressions/bitcast.md
---

## BITCAST {#bitcast}
Выполняет побитное преобразование целочисленного значения к указанному целочисленному типу. Преобразование всегда успешно, но может потерять точность или старшие биты.

**Примеры**
``` yql
SELECT
    BITCAST(100000ul AS Uint32),     -- 100000
    BITCAST(100000ul AS Int16),      -- -31072
    BITCAST(100000ul AS Uint16),     -- 34464
    BITCAST(-1 AS Int16),            -- -1
    BITCAST(-1 AS Uint16);           -- 65535
```