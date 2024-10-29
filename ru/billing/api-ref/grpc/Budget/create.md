---
editable: false
sourcePath: en/_api-ref-grpc/billing/v1/api-ref/grpc/Budget/create.md
---

# Billing API, gRPC: BudgetService.Create {#Create}

Creates a budget for the specified billing account.

## gRPC request

**rpc Create ([CreateBudgetRequest](#yandex.cloud.billing.v1.CreateBudgetRequest)) returns ([operation.Operation](#yandex.cloud.operation.Operation))**

## CreateBudgetRequest {#yandex.cloud.billing.v1.CreateBudgetRequest}

```json
{
  "billingAccountId": "string",
  "name": "string",
  // Includes only one of the fields `costBudgetSpec`, `expenseBudgetSpec`, `balanceBudgetSpec`
  "costBudgetSpec": {
    "amount": "string",
    "notificationUserAccountIds": [
      "string"
    ],
    "thresholdRules": [
      {
        "type": "ThresholdType",
        "amount": "string",
        "notificationUserAccountIds": [
          "string"
        ]
      }
    ],
    "filter": {
      "serviceIds": [
        "string"
      ],
      "cloudFoldersFilters": [
        {
          "cloudId": "string",
          "folderIds": [
            "string"
          ]
        }
      ]
    },
    // Includes only one of the fields `resetPeriod`, `startDate`
    "resetPeriod": "ResetPeriodType",
    "startDate": "string",
    // end of the list of possible fields
    "endDate": "string"
  },
  "expenseBudgetSpec": {
    "amount": "string",
    "notificationUserAccountIds": [
      "string"
    ],
    "thresholdRules": [
      {
        "type": "ThresholdType",
        "amount": "string",
        "notificationUserAccountIds": [
          "string"
        ]
      }
    ],
    "filter": {
      "serviceIds": [
        "string"
      ],
      "cloudFoldersFilters": [
        {
          "cloudId": "string",
          "folderIds": [
            "string"
          ]
        }
      ]
    },
    // Includes only one of the fields `resetPeriod`, `startDate`
    "resetPeriod": "ResetPeriodType",
    "startDate": "string",
    // end of the list of possible fields
    "endDate": "string"
  },
  "balanceBudgetSpec": {
    "amount": "string",
    "notificationUserAccountIds": [
      "string"
    ],
    "thresholdRules": [
      {
        "type": "ThresholdType",
        "amount": "string",
        "notificationUserAccountIds": [
          "string"
        ]
      }
    ],
    "startDate": "string",
    "endDate": "string"
  }
  // end of the list of possible fields
}
```

#|
||Field | Description ||
|| billingAccountId | **string**

Required field. ID of the billing account to list budgets corresponding to.
To get the billing account ID, use [yandex.cloud.billing.v1.BillingAccountService.List](/docs/billing/api-ref/grpc/BillingAccount/list#List) request. ||
|| name | **string**

Required field. Name of the budget. ||
|| costBudgetSpec | **[CostBudgetSpec](#yandex.cloud.billing.v1.CostBudgetSpec)**

Cost budget specification.

Includes only one of the fields `costBudgetSpec`, `expenseBudgetSpec`, `balanceBudgetSpec`.

Specification of the budget. ||
|| expenseBudgetSpec | **[ExpenseBudgetSpec](#yandex.cloud.billing.v1.ExpenseBudgetSpec)**

Expense budget specification.

Includes only one of the fields `costBudgetSpec`, `expenseBudgetSpec`, `balanceBudgetSpec`.

Specification of the budget. ||
|| balanceBudgetSpec | **[BalanceBudgetSpec](#yandex.cloud.billing.v1.BalanceBudgetSpec)**

Balance budget specification.

Includes only one of the fields `costBudgetSpec`, `expenseBudgetSpec`, `balanceBudgetSpec`.

Specification of the budget. ||
|#

## CostBudgetSpec {#yandex.cloud.billing.v1.CostBudgetSpec}

Cost budget specification describes budget that can be used to control cost of cloud resources usage.

#|
||Field | Description ||
|| amount | **string**

Required field. Max cost threshold of the budget. Amount currency is the same as corresponding [yandex.cloud.billing.v1.BillingAccount.currency](/docs/billing/api-ref/grpc/BillingAccount/get#yandex.cloud.billing.v1.BillingAccount). ||
|| notificationUserAccountIds[] | **string**

IDs of the [yandex.cloud.iam.v1.UserAccount](/docs/iam/api-ref/grpc/Federation/listUserAccounts#yandex.cloud.iam.v1.UserAccount).
Specified users will be be notified if the budget exceeds. ||
|| thresholdRules[] | **[ThresholdRule](#yandex.cloud.billing.v1.ThresholdRule)**

List of the [ThresholdRule](#yandex.cloud.billing.v1.ThresholdRule).
Rules define intermediate cost thresholds of the budget. ||
|| filter | **[ConsumptionFilter](#yandex.cloud.billing.v1.ConsumptionFilter)**

Filter that can be used for specific resources selection. Only consumption cost of selected resources are used for the budget calculation. ||
|| resetPeriod | enum **ResetPeriodType**

Periodic start type that resets budget after specified period is finished.
First time budget is calculated in the current period, i.e. current month, quarter or year.

Includes only one of the fields `resetPeriod`, `startDate`.

Start type of the budget.

- `RESET_PERIOD_TYPE_UNSPECIFIED`
- `MONTHLY`: Reset budget every month.
- `QUARTER`: Reset budget every quarter.
- `ANNUALLY`: Reset budget every year. ||
|| startDate | **string**

Custom start date of the budget.
Must be the first day of a month and must be formatted like YYYY-MM-DD.

Includes only one of the fields `resetPeriod`, `startDate`.

Start type of the budget. ||
|| endDate | **string**

Required field. End date of the budget.
Must be the last day of a month and must be formatted like YYYY-MM-DD. ||
|#

## ThresholdRule {#yandex.cloud.billing.v1.ThresholdRule}

Rules that define intermediate cost thresholds of the budget.

#|
||Field | Description ||
|| type | enum **ThresholdType**

Required field. Type of the rule.

- `THRESHOLD_TYPE_UNSPECIFIED`
- `PERCENT`: Percent.
- `AMOUNT`: The same as budget amount. ||
|| amount | **string**

Required field. Amount of the rule.
* Must be less than 100 if type is PERCENT.
* Must be less than budget's amount if type is AMOUNT. ||
|| notificationUserAccountIds[] | **string**

IDs of the [yandex.cloud.iam.v1.UserAccount](/docs/iam/api-ref/grpc/Federation/listUserAccounts#yandex.cloud.iam.v1.UserAccount).
Specified users will be be notified if the threshold exceeds. ||
|#

## ConsumptionFilter {#yandex.cloud.billing.v1.ConsumptionFilter}

Filter that can be used for specific resources selection.

#|
||Field | Description ||
|| serviceIds[] | **string**

IDs of the [yandex.cloud.billing.v1.Service](/docs/billing/api-ref/grpc/Service/get#yandex.cloud.billing.v1.Service).
Only consumption of resources corresponding to the given services is used for the budget calculation.
Empty sequence means no services filters. ||
|| cloudFoldersFilters[] | **[CloudFoldersConsumptionFilter](#yandex.cloud.billing.v1.CloudFoldersConsumptionFilter)**

Cloud and folders consumption filter.
Only consumption within specified clouds and folders is used for the budget calculation.
Empty sequence means no cloud and folders filters. ||
|#

## CloudFoldersConsumptionFilter {#yandex.cloud.billing.v1.CloudFoldersConsumptionFilter}

Filter that can be used for specific cloud and its folders selection.

#|
||Field | Description ||
|| cloudId | **string**

ID of the [yandex.cloud.resourcemanager.v1.Cloud](/docs/resource-manager/api-ref/grpc/Cloud/get#yandex.cloud.resourcemanager.v1.Cloud).
Only consumption within specified cloud is used for the budget calculation. ||
|| folderIds[] | **string**

IDs of the [yandex.cloud.resourcemanager.v1.Folder](/docs/resource-manager/api-ref/grpc/Folder/get#yandex.cloud.resourcemanager.v1.Folder).
Only consumption within specified folders of the given cloud is used for the budget calculation.
Empty sequence means no folders filters and the whole cloud consumption will be used. ||
|#

## ExpenseBudgetSpec {#yandex.cloud.billing.v1.ExpenseBudgetSpec}

Expense budget specification describes budget that can be used to control expense of cloud resources usage.

#|
||Field | Description ||
|| amount | **string**

Required field. Max expense threshold of the budget. Amount currency is the same as corresponding [yandex.cloud.billing.v1.BillingAccount.currency](/docs/billing/api-ref/grpc/BillingAccount/get#yandex.cloud.billing.v1.BillingAccount). ||
|| notificationUserAccountIds[] | **string**

IDs of the [yandex.cloud.iam.v1.UserAccount](/docs/iam/api-ref/grpc/Federation/listUserAccounts#yandex.cloud.iam.v1.UserAccount).
Specified users will be be notified if the budget exceeds. ||
|| thresholdRules[] | **[ThresholdRule](#yandex.cloud.billing.v1.ThresholdRule)**

List of the [ThresholdRule](#yandex.cloud.billing.v1.ThresholdRule).
Rules define intermediate expense thresholds of the budget. ||
|| filter | **[ConsumptionFilter](#yandex.cloud.billing.v1.ConsumptionFilter)**

Filter that can be used for specific resources selection. Only consumption expense of selected resources are used for the budget calculation. ||
|| resetPeriod | enum **ResetPeriodType**

Periodic start type that resets budget after specified period is finished.
First time budget is calculated in the current period, i.e. current month, quarter or year.

Includes only one of the fields `resetPeriod`, `startDate`.

Start type of the budget.

- `RESET_PERIOD_TYPE_UNSPECIFIED`
- `MONTHLY`: Reset budget every month.
- `QUARTER`: Reset budget every quarter.
- `ANNUALLY`: Reset budget every year. ||
|| startDate | **string**

Custom start date of the budget.
Must be the first day of a month and must be formatted like YYYY-MM-DD.

Includes only one of the fields `resetPeriod`, `startDate`.

Start type of the budget. ||
|| endDate | **string**

Required field. End date of the budget.
Must be the last day of a month and must be formatted like YYYY-MM-DD. ||
|#

## BalanceBudgetSpec {#yandex.cloud.billing.v1.BalanceBudgetSpec}

Balance budget specification describes budget that can be used to control [yandex.cloud.billing.v1.BillingAccount.balance](/docs/billing/api-ref/grpc/BillingAccount/get#yandex.cloud.billing.v1.BillingAccount).

#|
||Field | Description ||
|| amount | **string**

Required field. Max balance threshold of the budget. Amount currency is the same as corresponding [yandex.cloud.billing.v1.BillingAccount.currency](/docs/billing/api-ref/grpc/BillingAccount/get#yandex.cloud.billing.v1.BillingAccount). ||
|| notificationUserAccountIds[] | **string**

IDs of the [yandex.cloud.iam.v1.UserAccount](/docs/iam/api-ref/grpc/Federation/listUserAccounts#yandex.cloud.iam.v1.UserAccount).
Specified users will be be notified if the budget exceeds. ||
|| thresholdRules[] | **[ThresholdRule](#yandex.cloud.billing.v1.ThresholdRule)**

List of the [ThresholdRule](#yandex.cloud.billing.v1.ThresholdRule).
Rules define intermediate balance thresholds of the budget. ||
|| startDate | **string**

Start_date of the budget.
Must be the first day of a month and must be formatted like YYYY-MM-DD. ||
|| endDate | **string**

Required field. End date of the budget.
Must be the last day of a month and must be formatted like YYYY-MM-DD. ||
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
    "budgetId": "string"
  },
  // Includes only one of the fields `error`, `response`
  "error": "google.rpc.Status",
  "response": {
    "id": "string",
    "name": "string",
    "createdAt": "google.protobuf.Timestamp",
    "billingAccountId": "string",
    "status": "BudgetStatus",
    // Includes only one of the fields `costBudget`, `expenseBudget`, `balanceBudget`
    "costBudget": {
      "amount": "string",
      "notificationUserAccountIds": [
        "string"
      ],
      "thresholdRules": [
        {
          "type": "ThresholdType",
          "amount": "string",
          "notificationUserAccountIds": [
            "string"
          ]
        }
      ],
      "filter": {
        "serviceIds": [
          "string"
        ],
        "cloudFoldersFilters": [
          {
            "cloudId": "string",
            "folderIds": [
              "string"
            ]
          }
        ]
      },
      // Includes only one of the fields `resetPeriod`, `startDate`
      "resetPeriod": "ResetPeriodType",
      "startDate": "string",
      // end of the list of possible fields
      "endDate": "string"
    },
    "expenseBudget": {
      "amount": "string",
      "notificationUserAccountIds": [
        "string"
      ],
      "thresholdRules": [
        {
          "type": "ThresholdType",
          "amount": "string",
          "notificationUserAccountIds": [
            "string"
          ]
        }
      ],
      "filter": {
        "serviceIds": [
          "string"
        ],
        "cloudFoldersFilters": [
          {
            "cloudId": "string",
            "folderIds": [
              "string"
            ]
          }
        ]
      },
      // Includes only one of the fields `resetPeriod`, `startDate`
      "resetPeriod": "ResetPeriodType",
      "startDate": "string",
      // end of the list of possible fields
      "endDate": "string"
    },
    "balanceBudget": {
      "amount": "string",
      "notificationUserAccountIds": [
        "string"
      ],
      "thresholdRules": [
        {
          "type": "ThresholdType",
          "amount": "string",
          "notificationUserAccountIds": [
            "string"
          ]
        }
      ],
      "startDate": "string",
      "endDate": "string"
    }
    // end of the list of possible fields
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
|| metadata | **[CreateBudgetMetadata](#yandex.cloud.billing.v1.CreateBudgetMetadata)**

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
|| response | **[Budget](#yandex.cloud.billing.v1.Budget)**

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

## CreateBudgetMetadata {#yandex.cloud.billing.v1.CreateBudgetMetadata}

#|
||Field | Description ||
|| budgetId | **string**

ID of the budget. ||
|#

## Budget {#yandex.cloud.billing.v1.Budget}

A Budget resource. For more information, see [/docs/billing/concepts/budget].

#|
||Field | Description ||
|| id | **string**

ID of the budget. ||
|| name | **string**

Name of the budget. ||
|| createdAt | **[google.protobuf.Timestamp](https://developers.google.com/protocol-buffers/docs/reference/google.protobuf#timestamp)**

Creation timestamp. ||
|| billingAccountId | **string**

ID of the billing account that the budget belongs to. ||
|| status | enum **BudgetStatus**

Status of the budget.

- `BUDGET_STATUS_UNSPECIFIED`
- `CREATING`: The budget is being created.
- `ACTIVE`: The budget is active.
- `FINISHED`: The budget is finished. ||
|| costBudget | **[CostBudgetSpec](#yandex.cloud.billing.v1.CostBudgetSpec2)**

Cost budget specification.

Includes only one of the fields `costBudget`, `expenseBudget`, `balanceBudget`.

Specification of the budget. ||
|| expenseBudget | **[ExpenseBudgetSpec](#yandex.cloud.billing.v1.ExpenseBudgetSpec2)**

Expense budget specification.

Includes only one of the fields `costBudget`, `expenseBudget`, `balanceBudget`.

Specification of the budget. ||
|| balanceBudget | **[BalanceBudgetSpec](#yandex.cloud.billing.v1.BalanceBudgetSpec2)**

Balance budget specification.

Includes only one of the fields `costBudget`, `expenseBudget`, `balanceBudget`.

Specification of the budget. ||
|#

## CostBudgetSpec {#yandex.cloud.billing.v1.CostBudgetSpec2}

Cost budget specification describes budget that can be used to control cost of cloud resources usage.

#|
||Field | Description ||
|| amount | **string**

Required field. Max cost threshold of the budget. Amount currency is the same as corresponding [yandex.cloud.billing.v1.BillingAccount.currency](/docs/billing/api-ref/grpc/BillingAccount/get#yandex.cloud.billing.v1.BillingAccount). ||
|| notificationUserAccountIds[] | **string**

IDs of the [yandex.cloud.iam.v1.UserAccount](/docs/iam/api-ref/grpc/Federation/listUserAccounts#yandex.cloud.iam.v1.UserAccount).
Specified users will be be notified if the budget exceeds. ||
|| thresholdRules[] | **[ThresholdRule](#yandex.cloud.billing.v1.ThresholdRule2)**

List of the [ThresholdRule](#yandex.cloud.billing.v1.ThresholdRule2).
Rules define intermediate cost thresholds of the budget. ||
|| filter | **[ConsumptionFilter](#yandex.cloud.billing.v1.ConsumptionFilter2)**

Filter that can be used for specific resources selection. Only consumption cost of selected resources are used for the budget calculation. ||
|| resetPeriod | enum **ResetPeriodType**

Periodic start type that resets budget after specified period is finished.
First time budget is calculated in the current period, i.e. current month, quarter or year.

Includes only one of the fields `resetPeriod`, `startDate`.

Start type of the budget.

- `RESET_PERIOD_TYPE_UNSPECIFIED`
- `MONTHLY`: Reset budget every month.
- `QUARTER`: Reset budget every quarter.
- `ANNUALLY`: Reset budget every year. ||
|| startDate | **string**

Custom start date of the budget.
Must be the first day of a month and must be formatted like YYYY-MM-DD.

Includes only one of the fields `resetPeriod`, `startDate`.

Start type of the budget. ||
|| endDate | **string**

Required field. End date of the budget.
Must be the last day of a month and must be formatted like YYYY-MM-DD. ||
|#

## ThresholdRule {#yandex.cloud.billing.v1.ThresholdRule2}

Rules that define intermediate cost thresholds of the budget.

#|
||Field | Description ||
|| type | enum **ThresholdType**

Required field. Type of the rule.

- `THRESHOLD_TYPE_UNSPECIFIED`
- `PERCENT`: Percent.
- `AMOUNT`: The same as budget amount. ||
|| amount | **string**

Required field. Amount of the rule.
* Must be less than 100 if type is PERCENT.
* Must be less than budget's amount if type is AMOUNT. ||
|| notificationUserAccountIds[] | **string**

IDs of the [yandex.cloud.iam.v1.UserAccount](/docs/iam/api-ref/grpc/Federation/listUserAccounts#yandex.cloud.iam.v1.UserAccount).
Specified users will be be notified if the threshold exceeds. ||
|#

## ConsumptionFilter {#yandex.cloud.billing.v1.ConsumptionFilter2}

Filter that can be used for specific resources selection.

#|
||Field | Description ||
|| serviceIds[] | **string**

IDs of the [yandex.cloud.billing.v1.Service](/docs/billing/api-ref/grpc/Service/get#yandex.cloud.billing.v1.Service).
Only consumption of resources corresponding to the given services is used for the budget calculation.
Empty sequence means no services filters. ||
|| cloudFoldersFilters[] | **[CloudFoldersConsumptionFilter](#yandex.cloud.billing.v1.CloudFoldersConsumptionFilter2)**

Cloud and folders consumption filter.
Only consumption within specified clouds and folders is used for the budget calculation.
Empty sequence means no cloud and folders filters. ||
|#

## CloudFoldersConsumptionFilter {#yandex.cloud.billing.v1.CloudFoldersConsumptionFilter2}

Filter that can be used for specific cloud and its folders selection.

#|
||Field | Description ||
|| cloudId | **string**

ID of the [yandex.cloud.resourcemanager.v1.Cloud](/docs/resource-manager/api-ref/grpc/Cloud/get#yandex.cloud.resourcemanager.v1.Cloud).
Only consumption within specified cloud is used for the budget calculation. ||
|| folderIds[] | **string**

IDs of the [yandex.cloud.resourcemanager.v1.Folder](/docs/resource-manager/api-ref/grpc/Folder/get#yandex.cloud.resourcemanager.v1.Folder).
Only consumption within specified folders of the given cloud is used for the budget calculation.
Empty sequence means no folders filters and the whole cloud consumption will be used. ||
|#

## ExpenseBudgetSpec {#yandex.cloud.billing.v1.ExpenseBudgetSpec2}

Expense budget specification describes budget that can be used to control expense of cloud resources usage.

#|
||Field | Description ||
|| amount | **string**

Required field. Max expense threshold of the budget. Amount currency is the same as corresponding [yandex.cloud.billing.v1.BillingAccount.currency](/docs/billing/api-ref/grpc/BillingAccount/get#yandex.cloud.billing.v1.BillingAccount). ||
|| notificationUserAccountIds[] | **string**

IDs of the [yandex.cloud.iam.v1.UserAccount](/docs/iam/api-ref/grpc/Federation/listUserAccounts#yandex.cloud.iam.v1.UserAccount).
Specified users will be be notified if the budget exceeds. ||
|| thresholdRules[] | **[ThresholdRule](#yandex.cloud.billing.v1.ThresholdRule2)**

List of the [ThresholdRule](#yandex.cloud.billing.v1.ThresholdRule2).
Rules define intermediate expense thresholds of the budget. ||
|| filter | **[ConsumptionFilter](#yandex.cloud.billing.v1.ConsumptionFilter2)**

Filter that can be used for specific resources selection. Only consumption expense of selected resources are used for the budget calculation. ||
|| resetPeriod | enum **ResetPeriodType**

Periodic start type that resets budget after specified period is finished.
First time budget is calculated in the current period, i.e. current month, quarter or year.

Includes only one of the fields `resetPeriod`, `startDate`.

Start type of the budget.

- `RESET_PERIOD_TYPE_UNSPECIFIED`
- `MONTHLY`: Reset budget every month.
- `QUARTER`: Reset budget every quarter.
- `ANNUALLY`: Reset budget every year. ||
|| startDate | **string**

Custom start date of the budget.
Must be the first day of a month and must be formatted like YYYY-MM-DD.

Includes only one of the fields `resetPeriod`, `startDate`.

Start type of the budget. ||
|| endDate | **string**

Required field. End date of the budget.
Must be the last day of a month and must be formatted like YYYY-MM-DD. ||
|#

## BalanceBudgetSpec {#yandex.cloud.billing.v1.BalanceBudgetSpec2}

Balance budget specification describes budget that can be used to control [yandex.cloud.billing.v1.BillingAccount.balance](/docs/billing/api-ref/grpc/BillingAccount/get#yandex.cloud.billing.v1.BillingAccount).

#|
||Field | Description ||
|| amount | **string**

Required field. Max balance threshold of the budget. Amount currency is the same as corresponding [yandex.cloud.billing.v1.BillingAccount.currency](/docs/billing/api-ref/grpc/BillingAccount/get#yandex.cloud.billing.v1.BillingAccount). ||
|| notificationUserAccountIds[] | **string**

IDs of the [yandex.cloud.iam.v1.UserAccount](/docs/iam/api-ref/grpc/Federation/listUserAccounts#yandex.cloud.iam.v1.UserAccount).
Specified users will be be notified if the budget exceeds. ||
|| thresholdRules[] | **[ThresholdRule](#yandex.cloud.billing.v1.ThresholdRule2)**

List of the [ThresholdRule](#yandex.cloud.billing.v1.ThresholdRule2).
Rules define intermediate balance thresholds of the budget. ||
|| startDate | **string**

Start_date of the budget.
Must be the first day of a month and must be formatted like YYYY-MM-DD. ||
|| endDate | **string**

Required field. End date of the budget.
Must be the last day of a month and must be formatted like YYYY-MM-DD. ||
|#