---
editable: false
sourcePath: en/_api-ref-grpc/vpc/v1/api-ref/grpc/RouteTable/get.md
---

# Virtual Private Cloud API, gRPC: RouteTableService.Get {#Get}

Returns the specified RouteTable resource.

To get the list of available RouteTable resources, make a [List](/docs/vpc/api-ref/grpc/RouteTable/list#List) request.

## gRPC request

**rpc Get ([GetRouteTableRequest](#yandex.cloud.vpc.v1.GetRouteTableRequest)) returns ([RouteTable](#yandex.cloud.vpc.v1.RouteTable))**

## GetRouteTableRequest {#yandex.cloud.vpc.v1.GetRouteTableRequest}

```json
{
  "routeTableId": "string"
}
```

#|
||Field | Description ||
|| routeTableId | **string**

Required field. ID of the RouteTable resource to return.
To get the route table ID use a [RouteTableService.List](/docs/vpc/api-ref/grpc/RouteTable/list#List) request. ||
|#

## RouteTable {#yandex.cloud.vpc.v1.RouteTable}

```json
{
  "id": "string",
  "folderId": "string",
  "createdAt": "google.protobuf.Timestamp",
  "name": "string",
  "description": "string",
  "labels": "string",
  "networkId": "string",
  "staticRoutes": [
    {
      // Includes only one of the fields `destinationPrefix`
      "destinationPrefix": "string",
      // end of the list of possible fields
      // Includes only one of the fields `nextHopAddress`, `gatewayId`
      "nextHopAddress": "string",
      "gatewayId": "string",
      // end of the list of possible fields
      "labels": "string"
    }
  ]
}
```

A RouteTable resource. For more information, see [Static Routes](/docs/vpc/concepts/routing).

#|
||Field | Description ||
|| id | **string**

ID of the route table. ||
|| folderId | **string**

ID of the folder that the route table belongs to. ||
|| createdAt | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**

Creation timestamp in [RFC3339](https://www.ietf.org/rfc/rfc3339.txt) text format. ||
|| name | **string**

Name of the route table.
The name must be unique within the folder.
Value must match the regular expression `\|[a-zA-Z]([-_a-zA-Z0-9]{0,61}[a-zA-Z0-9])?`. ||
|| description | **string**

Optional description of the route table. 0-256 characters long. ||
|| labels | **string**

Resource labels, `key:value` pairs.
No more than 64 per resource.
The string length in characters for each key must be 1-63.
Each value must match the regular expression `[-_0-9a-z]*`.
Each key must match the regular expression `[a-z][-_0-9a-z]*`. ||
|| networkId | **string**

ID of the network the route table belongs to. ||
|| staticRoutes[] | **[StaticRoute](#yandex.cloud.vpc.v1.StaticRoute)**

List of static routes. ||
|#

## StaticRoute {#yandex.cloud.vpc.v1.StaticRoute}

A StaticRoute resource. For more information, see [Static Routes](/docs/vpc/concepts/routing).

#|
||Field | Description ||
|| destinationPrefix | **string**

Destination subnet in CIDR notation

Includes only one of the fields `destinationPrefix`. ||
|| nextHopAddress | **string**

Next hop IP address

Includes only one of the fields `nextHopAddress`, `gatewayId`. ||
|| gatewayId | **string**

Next hop gateway id

Includes only one of the fields `nextHopAddress`, `gatewayId`. ||
|| labels | **string**

Resource labels as `` key:value `` pairs. Maximum of 64 per resource. ||
|#