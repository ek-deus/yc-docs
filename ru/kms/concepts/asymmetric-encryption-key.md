# Асимметричная ключевая пара шифрования в {{ kms-short-name }}

Асимметричная ключевая пара шифрования состоит из двух частей: открытого ключа шифрования (Public key) и закрытого ключа шифрования (Private key). Открытый ключ используется для шифрования, закрытый — для расшифрования.

{{ kms-name }} позволяет выгружать открытый ключ для шифрования текста на стороне клиента. Расшифровать такой текст в {{ kms-short-name }} можно с использованием закрытого ключа. Получить прямой доступ к закрытому ключу в {{ kms-short-name }} нельзя.

## Параметры ключевой пары шифрования {#parameters}

Для ключевой пары шифрования {{ kms-short-name }} доступны следующие параметры:
* Идентификатор — уникальный идентификатор ключевой пары в {{ yandex-cloud }}. Используется для работы с ключевыми парами с помощью SDK, [API](../../glossary/rest-api.md) и CLI.
* Имя — имя ключевой пары, неуникально и может быть использовано для работы с ключевыми парами с помощью CLI, если в каталоге только одна ключевая пара с таким именем.
* Алгоритм шифрования – алгоритм, используемый для шифрования. Поддерживаются следующие алгоритмы асимметричного шифрования: 
    * `rsa-2048-enc-oaep-sha-256`;
    * `rsa-3072-enc-oaep-sha-256`;
    * `rsa-4096-enc-oaep-sha-256`.

* Статус — текущее состояние ключевой пары. Возможные статусы: 
    * `Creating` — ключевая пара создается.
    * `Active` — ключевая пара может использоваться для шифрования и расшифрования.
    * `Inactive` — ключевая пара не может использоваться.
    
    Изменить статус ключевой пары с `Active` на `Inactive` и обратно можно вызовом gRPC API [AsymmetricEncryptionKeyService/Update](../api-ref/grpc/asymmetric_encryption_key_service.md#Update).

## Использование ключевой пары шифрования {#use}

Асимметричную ключевую пару шифрования можно использовать в операциях шифрования и расшифрования данных при наличии определенных [ролей](../security/index.md#roles-list). Вы можете временно заблокировать операции с использованием ключевой пары, отозвав роли или изменив ее статус на `Inactive`. Подробнее читайте в разделе [{#T}](../security/index.md).

## Удаление ключевой пары шифрования {#delete}

Удаление ключевой пары шифрования или родительского ресурса (каталога или облака), в котором содержалась ключевая пара, приводит к уничтожению содержащегося в нем криптографического материала. После этого вы не сможете расшифровать данные, зашифрованные открытым ключом ключевой пары.