---
editable: false
sourcePath: en/_api-ref-grpc/mdb/clickhouse/v1/api-ref/grpc/Database/get.md
---

# Managed Service for ClickHouse API, gRPC: DatabaseService.Get

Returns the specified ClickHouse Database resource.

To get the list of available ClickHouse Database resources, make a [List](/docs/managed-clickhouse/api-ref/grpc/Database/list#List) request.

## gRPC request

**rpc Get ([GetDatabaseRequest](#yandex.cloud.mdb.clickhouse.v1.GetDatabaseRequest)) returns ([Database](#yandex.cloud.mdb.clickhouse.v1.Database))**

## GetDatabaseRequest {#yandex.cloud.mdb.clickhouse.v1.GetDatabaseRequest}

```json
{
  "cluster_id": "string",
  "database_name": "string"
}
```

#|
||Field | Description ||
|| cluster_id | **string**

Required field. ID of the ClickHouse cluster that the database belongs to.
To get the cluster ID, use a [ClusterService.List](/docs/managed-clickhouse/api-ref/grpc/Cluster/list#List) request. ||
|| database_name | **string**

Required field. Name of the ClickHouse Database resource to return.
To get the name of the database, use a [DatabaseService.List](/docs/managed-clickhouse/api-ref/grpc/Database/list#List) request. ||
|#

## Database {#yandex.cloud.mdb.clickhouse.v1.Database}

```json
{
  "name": "string",
  "cluster_id": "string"
}
```

A ClickHouse Database resource. For more information, see the
[Developer's Guide](/docs/managed-clickhouse/concepts).

#|
||Field | Description ||
|| name | **string**

Name of the database. ||
|| cluster_id | **string**

ID of the ClickHouse cluster that the database belongs to. ||
|#