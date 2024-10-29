---
editable: false
sourcePath: en/_api-ref-grpc/dataproc/v1/api-ref/grpc/Cluster/create.md
---

# Data Proc API, gRPC: ClusterService.Create {#Create}

Creates a cluster in the specified folder.

## gRPC request

**rpc Create ([CreateClusterRequest](#yandex.cloud.dataproc.v1.CreateClusterRequest)) returns ([operation.Operation](#yandex.cloud.operation.Operation))**

## CreateClusterRequest {#yandex.cloud.dataproc.v1.CreateClusterRequest}

```json
{
  "folderId": "string",
  "name": "string",
  "description": "string",
  "labels": "string",
  "configSpec": {
    "versionId": "string",
    "hadoop": {
      "services": [
        "Service"
      ],
      "properties": "string",
      "sshPublicKeys": [
        "string"
      ],
      "initializationActions": [
        {
          "uri": "string",
          "args": [
            "string"
          ],
          "timeout": "int64"
        }
      ]
    },
    "subclustersSpec": [
      {
        "name": "string",
        "role": "Role",
        "resources": {
          "resourcePresetId": "string",
          "diskTypeId": "string",
          "diskSize": "int64"
        },
        "subnetId": "string",
        "hostsCount": "int64",
        "assignPublicIp": "bool",
        "autoscalingConfig": {
          "maxHostsCount": "int64",
          "preemptible": "bool",
          "measurementDuration": "google.protobuf.Duration",
          "warmupDuration": "google.protobuf.Duration",
          "stabilizationDuration": "google.protobuf.Duration",
          "cpuUtilizationTarget": "double",
          "decommissionTimeout": "int64"
        }
      }
    ]
  },
  "zoneId": "string",
  "serviceAccountId": "string",
  "bucket": "string",
  "uiProxy": "bool",
  "securityGroupIds": [
    "string"
  ],
  "hostGroupIds": [
    "string"
  ],
  "deletionProtection": "bool",
  "logGroupId": "string"
}
```

#|
||Field | Description ||
|| folderId | **string**

Required field. ID of the folder to create a cluster in.

To get a folder ID make a [yandex.cloud.resourcemanager.v1.FolderService.List](/docs/resource-manager/api-ref/grpc/Folder/list#List) request. ||
|| name | **string**

Name of the cluster. The name must be unique within the folder.
The name can't be changed after the Data Proc cluster is created. ||
|| description | **string**

Description of the cluster. ||
|| labels | **string**

Cluster labels as `key:value` pairs. ||
|| configSpec | **[CreateClusterConfigSpec](#yandex.cloud.dataproc.v1.CreateClusterConfigSpec)**

Required field. Configuration and resources for hosts that should be created with the cluster. ||
|| zoneId | **string**

Required field. ID of the availability zone where the cluster should be placed.

To get the list of available zones make a [yandex.cloud.compute.v1.ZoneService.List](/docs/compute/api-ref/grpc/Zone/list#List) request. ||
|| serviceAccountId | **string**

Required field. ID of the service account to be used by the Data Proc manager agent. ||
|| bucket | **string**

Name of the Object Storage bucket to use for Data Proc jobs. ||
|| uiProxy | **bool**

Enable UI Proxy feature. ||
|| securityGroupIds[] | **string**

User security groups. ||
|| hostGroupIds[] | **string**

Host groups to place VMs of cluster on. ||
|| deletionProtection | **bool**

Deletion Protection inhibits deletion of the cluster ||
|| logGroupId | **string**

ID of the cloud logging log group to write logs. If not set, logs will not be sent to logging service ||
|#

## CreateClusterConfigSpec {#yandex.cloud.dataproc.v1.CreateClusterConfigSpec}

#|
||Field | Description ||
|| versionId | **string**

Version of the image for cluster provisioning.

All available versions are listed in the [documentation](/docs/data-proc/concepts/environment). ||
|| hadoop | **[HadoopConfig](#yandex.cloud.dataproc.v1.HadoopConfig)**

Data Proc specific options. ||
|| subclustersSpec[] | **[CreateSubclusterConfigSpec](#yandex.cloud.dataproc.v1.CreateSubclusterConfigSpec)**

Specification for creating subclusters. ||
|#

## HadoopConfig {#yandex.cloud.dataproc.v1.HadoopConfig}

Hadoop configuration that describes services installed in a cluster,
their properties and settings.

#|
||Field | Description ||
|| services[] | enum **Service**

Set of services used in the cluster (if empty, the default set is used).

- `SERVICE_UNSPECIFIED`
- `HDFS`
- `YARN`
- `MAPREDUCE`
- `HIVE`
- `TEZ`
- `ZOOKEEPER`
- `HBASE`
- `SQOOP`
- `FLUME`
- `SPARK`
- `ZEPPELIN`
- `OOZIE`
- `LIVY` ||
|| properties | **string**

Properties set for all hosts in `*-site.xml` configurations. The key should indicate
the service and the property.

For example, use the key 'hdfs:dfs.replication' to set the `dfs.replication` property
in the file `/etc/hadoop/conf/hdfs-site.xml`. ||
|| sshPublicKeys[] | **string**

List of public SSH keys to access to cluster hosts. ||
|| initializationActions[] | **[InitializationAction](#yandex.cloud.dataproc.v1.InitializationAction)**

Set of init-actions ||
|#

## InitializationAction {#yandex.cloud.dataproc.v1.InitializationAction}

#|
||Field | Description ||
|| uri | **string**

URI of the executable file ||
|| args[] | **string**

Arguments to the initialization action ||
|| timeout | **int64**

Execution timeout ||
|#

## CreateSubclusterConfigSpec {#yandex.cloud.dataproc.v1.CreateSubclusterConfigSpec}

#|
||Field | Description ||
|| name | **string**

Name of the subcluster. ||
|| role | enum **Role**

Required field. Role of the subcluster in the Data Proc cluster.

- `ROLE_UNSPECIFIED`
- `MASTERNODE`: The subcluster fulfills the master role.

  Master can run the following services, depending on the requested components:
* HDFS: Namenode, Secondary Namenode
* YARN: ResourceManager, Timeline Server
* HBase Master
* Hive: Server, Metastore, HCatalog
* Spark History Server
* Zeppelin
* ZooKeeper
- `DATANODE`: The subcluster is a DATANODE in a Data Proc cluster.

  DATANODE can run the following services, depending on the requested components:
* HDFS DataNode
* YARN NodeManager
* HBase RegionServer
* Spark libraries
- `COMPUTENODE`: The subcluster is a COMPUTENODE in a Data Proc cluster.

  COMPUTENODE can run the following services, depending on the requested components:
* YARN NodeManager
* Spark libraries ||
|| resources | **[Resources](#yandex.cloud.dataproc.v1.Resources)**

Required field. Resource configuration for hosts in the subcluster. ||
|| subnetId | **string**

Required field. ID of the VPC subnet used for hosts in the subcluster. ||
|| hostsCount | **int64**

Number of hosts in the subcluster. ||
|| assignPublicIp | **bool**

Assign public ip addresses for all hosts in subcluter. ||
|| autoscalingConfig | **[AutoscalingConfig](#yandex.cloud.dataproc.v1.AutoscalingConfig)**

Configuration for instance group based subclusters ||
|#

## Resources {#yandex.cloud.dataproc.v1.Resources}

#|
||Field | Description ||
|| resourcePresetId | **string**

ID of the resource preset for computational resources available to a host (CPU, memory etc.).
All available presets are listed in the [documentation](/docs/data-proc/concepts/instance-types). ||
|| diskTypeId | **string**

Type of the storage environment for the host.
Possible values:
* network-hdd - network HDD drive,
* network-ssd - network SSD drive. ||
|| diskSize | **int64**

Volume of the storage available to a host, in bytes. ||
|#

## AutoscalingConfig {#yandex.cloud.dataproc.v1.AutoscalingConfig}

#|
||Field | Description ||
|| maxHostsCount | **int64**

Upper limit for total instance subcluster count. ||
|| preemptible | **bool**

Preemptible instances are stopped at least once every 24 hours, and can be stopped at any time
if their resources are needed by Compute.
For more information, see [Preemptible Virtual Machines](/docs/compute/concepts/preemptible-vm). ||
|| measurementDuration | **[google.protobuf.Duration](https://developers.google.com/protocol-buffers/docs/reference/csharp/class/google/protobuf/well-known-types/duration)**

Required field. Time in seconds allotted for averaging metrics. ||
|| warmupDuration | **[google.protobuf.Duration](https://developers.google.com/protocol-buffers/docs/reference/csharp/class/google/protobuf/well-known-types/duration)**

The warmup time of the instance in seconds. During this time,
traffic is sent to the instance, but instance metrics are not collected. ||
|| stabilizationDuration | **[google.protobuf.Duration](https://developers.google.com/protocol-buffers/docs/reference/csharp/class/google/protobuf/well-known-types/duration)**

Minimum amount of time in seconds allotted for monitoring before
Instance Groups can reduce the number of instances in the group.
During this time, the group size doesn't decrease, even if the new metric values
indicate that it should. ||
|| cpuUtilizationTarget | **double**

Defines an autoscaling rule based on the average CPU utilization of the instance group. ||
|| decommissionTimeout | **int64**

Timeout to gracefully decommission nodes during downscaling. In seconds. Default value: 120 ||
|#

## operation.Operation {#yandex.cloud.operation.Operation}

```json
{
  "id": "string",
  "description": "string",
  "createdAt": "google.protobuf.Timestamp",
  "createdBy": "string",
  "modifiedAt": "google.protobuf.Timestamp",
  "done": "bool",
  "metadata": {
    "clusterId": "string"
  },
  // Includes only one of the fields `error`, `response`
  "error": "google.rpc.Status",
  "response": {
    "id": "string",
    "folderId": "string",
    "createdAt": "google.protobuf.Timestamp",
    "name": "string",
    "description": "string",
    "labels": "string",
    "monitoring": [
      {
        "name": "string",
        "description": "string",
        "link": "string"
      }
    ],
    "config": {
      "versionId": "string",
      "hadoop": {
        "services": [
          "Service"
        ],
        "properties": "string",
        "sshPublicKeys": [
          "string"
        ],
        "initializationActions": [
          {
            "uri": "string",
            "args": [
              "string"
            ],
            "timeout": "int64"
          }
        ]
      }
    },
    "health": "Health",
    "status": "Status",
    "zoneId": "string",
    "serviceAccountId": "string",
    "bucket": "string",
    "uiProxy": "bool",
    "securityGroupIds": [
      "string"
    ],
    "hostGroupIds": [
      "string"
    ],
    "deletionProtection": "bool",
    "logGroupId": "string"
  }
  // end of the list of possible fields
}
```

An Operation resource. For more information, see [Operation](/docs/api-design-guide/concepts/operation).

#|
||Field | Description ||
|| id | **string**

ID of the operation. ||
|| description | **string**

Description of the operation. 0-256 characters long. ||
|| createdAt | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**

Creation timestamp. ||
|| createdBy | **string**

ID of the user or service account who initiated the operation. ||
|| modifiedAt | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**

The time when the Operation resource was last modified. ||
|| done | **bool**

If the value is `false`, it means the operation is still in progress.
If `true`, the operation is completed, and either `error` or `response` is available. ||
|| metadata | **[CreateClusterMetadata](#yandex.cloud.dataproc.v1.CreateClusterMetadata)**

Service-specific metadata associated with the operation.
It typically contains the ID of the target resource that the operation is performed on.
Any method that returns a long-running operation should document the metadata type, if any. ||
|| error | **[google.rpc.Status](https://cloud.google.com/tasks/docs/reference/rpc/google.rpc#status)**

The error result of the operation in case of failure or cancellation.

Includes only one of the fields `error`, `response`.

The operation result.
If `done == false` and there was no failure detected, neither `error` nor `response` is set.
If `done == false` and there was a failure detected, `error` is set.
If `done == true`, exactly one of `error` or `response` is set. ||
|| response | **[Cluster](#yandex.cloud.dataproc.v1.Cluster)**

The normal response of the operation in case of success.
If the original method returns no data on success, such as Delete,
the response is [google.protobuf.Empty](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#google.protobuf.Empty).
If the original method is the standard Create/Update,
the response should be the target resource of the operation.
Any method that returns a long-running operation should document the response type, if any.

Includes only one of the fields `error`, `response`.

The operation result.
If `done == false` and there was no failure detected, neither `error` nor `response` is set.
If `done == false` and there was a failure detected, `error` is set.
If `done == true`, exactly one of `error` or `response` is set. ||
|#

## CreateClusterMetadata {#yandex.cloud.dataproc.v1.CreateClusterMetadata}

#|
||Field | Description ||
|| clusterId | **string**

ID of the cluster that is being created. ||
|#

## Cluster {#yandex.cloud.dataproc.v1.Cluster}

A Data Proc cluster. For details about the concept, see [documentation](/docs/data-proc/concepts/).

#|
||Field | Description ||
|| id | **string**

ID of the cluster. Generated at creation time. ||
|| folderId | **string**

ID of the folder that the cluster belongs to. ||
|| createdAt | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**

Creation timestamp. ||
|| name | **string**

Name of the cluster. The name is unique within the folder. ||
|| description | **string**

Description of the cluster. ||
|| labels | **string**

Cluster labels as `key:value` pairs. ||
|| monitoring[] | **[Monitoring](#yandex.cloud.dataproc.v1.Monitoring)**

Monitoring systems relevant to the cluster. ||
|| config | **[ClusterConfig](#yandex.cloud.dataproc.v1.ClusterConfig)**

Configuration of the cluster. ||
|| health | enum **Health**

Aggregated cluster health.

- `HEALTH_UNKNOWN`: Object is in unknown state (we have no data).
- `ALIVE`: Object is alive and well (for example, all hosts of the cluster are alive).
- `DEAD`: Object is inoperable (it cannot perform any of its essential functions).
- `DEGRADED`: Object is partially alive (it can perform some of its essential functions). ||
|| status | enum **Status**

Cluster status.

- `STATUS_UNKNOWN`: Cluster state is unknown.
- `CREATING`: Cluster is being created.
- `RUNNING`: Cluster is running normally.
- `ERROR`: Cluster encountered a problem and cannot operate.
- `STOPPING`: Cluster is stopping.
- `STOPPED`: Cluster stopped.
- `STARTING`: Cluster is starting. ||
|| zoneId | **string**

ID of the availability zone where the cluster resides. ||
|| serviceAccountId | **string**

ID of service account for the Data Proc manager agent. ||
|| bucket | **string**

Object Storage bucket to be used for Data Proc jobs that are run in the cluster. ||
|| uiProxy | **bool**

Whether UI Proxy feature is enabled. ||
|| securityGroupIds[] | **string**

User security groups. ||
|| hostGroupIds[] | **string**

Host groups hosting VMs of the cluster. ||
|| deletionProtection | **bool**

Deletion Protection inhibits deletion of the cluster ||
|| logGroupId | **string**

ID of the cloud logging log group to write logs. If not set, default log group for the folder will be used.
To prevent logs from being sent to the cloud set cluster property dataproc:disable_cloud_logging = true ||
|#

## Monitoring {#yandex.cloud.dataproc.v1.Monitoring}

Metadata of a monitoring system for a Data Proc cluster.

#|
||Field | Description ||
|| name | **string**

Name of the monitoring system. ||
|| description | **string**

Description of the monitoring system. ||
|| link | **string**

Link to the monitoring system. ||
|#

## ClusterConfig {#yandex.cloud.dataproc.v1.ClusterConfig}

#|
||Field | Description ||
|| versionId | **string**

Image version for cluster provisioning.
All available versions are listed in the [documentation](/docs/data-proc/concepts/environment). ||
|| hadoop | **[HadoopConfig](#yandex.cloud.dataproc.v1.HadoopConfig2)**

Data Proc specific configuration options. ||
|#

## HadoopConfig {#yandex.cloud.dataproc.v1.HadoopConfig2}

Hadoop configuration that describes services installed in a cluster,
their properties and settings.

#|
||Field | Description ||
|| services[] | enum **Service**

Set of services used in the cluster (if empty, the default set is used).

- `SERVICE_UNSPECIFIED`
- `HDFS`
- `YARN`
- `MAPREDUCE`
- `HIVE`
- `TEZ`
- `ZOOKEEPER`
- `HBASE`
- `SQOOP`
- `FLUME`
- `SPARK`
- `ZEPPELIN`
- `OOZIE`
- `LIVY` ||
|| properties | **string**

Properties set for all hosts in `*-site.xml` configurations. The key should indicate
the service and the property.

For example, use the key 'hdfs:dfs.replication' to set the `dfs.replication` property
in the file `/etc/hadoop/conf/hdfs-site.xml`. ||
|| sshPublicKeys[] | **string**

List of public SSH keys to access to cluster hosts. ||
|| initializationActions[] | **[InitializationAction](#yandex.cloud.dataproc.v1.InitializationAction2)**

Set of init-actions ||
|#

## InitializationAction {#yandex.cloud.dataproc.v1.InitializationAction2}

#|
||Field | Description ||
|| uri | **string**

URI of the executable file ||
|| args[] | **string**

Arguments to the initialization action ||
|| timeout | **int64**

Execution timeout ||
|#