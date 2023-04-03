---
title: 加速查詢端點
description: 了解如何以無狀態方式存取查詢加速儲存，以根據匯總的資料快速傳回結果。 本檔案提供Query Service accelerated-querys端點的範例HTTP要求和回應。
exl-id: 29ea4d25-9c46-4b29-a6d7-45ac33dcb0fb
source-git-commit: aa209dce9268a15a91db6e3afa7b6066683d76ea
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 1%

---

# 加速查詢端點

作為Data Distiller SKU的一部分， [查詢服務API](https://developer.adobe.com/experience-platform-apis/references/query-service/) 可讓您對加速的存放區進行無狀態查詢。 傳回的結果是以匯總的資料為基礎。 結果延遲的減少允許更互動的資訊交換。 加速查詢API也可用來提升效能 [使用者定義的控制面板](../../dashboards/user-defined-dashboards.md).

繼續閱讀本指南之前，請確定您已閱讀並了解 [查詢服務API指南](./getting-started.md) 以便成功使用查詢服務API。

## 快速入門

必須有Data Distiller SKU才能使用查詢加速存放區。 請參閱 [包裝](../packages.md) 和 [護欄](../guardrails.md#query-accelerated-store) 與資料Distiller SKU相關的檔案。 如果您沒有Data Distiller SKU，請聯絡您的Adobe客戶服務代表以取得詳細資訊。

<!-- Document is hidden temporarily
Please see the [packaging](../packages.md), [guardrails](../guardrails.md#query-accelerated-store), and [licensing](../data-distiller/license-usage.md) documentation that relates to the Data Distiller SKU. 
-->

以下各節詳細說明透過查詢服務API以無狀態方式存取查詢加速儲存所需的API呼叫。 每個呼叫都包含一般API格式、顯示必要標題的範例要求，以及範例回應。

## 執行加速查詢 {#run-accelerated-query}

向發出POST要求 `/accelerated-queries` 端點來執行加速查詢。 查詢會直接包含在要求裝載中，或以範本ID參照。

**API格式**

```shell
POST /accelerated-queries
```

### 請求

>[!IMPORTANT]
>
>向 `/accelerated-queries` 端點需要SQL陳述式或模板ID，但不需要兩者。 在請求中提交兩者會導致錯誤。

以下請求將請求主體中的SQL查詢提交到加速儲存。

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/acceleated-queries
 -H 'Authorization: {ACCESS_TOKEN}'
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'Content-Type: application/json' \
 -H 'Accept: application/json' \
 -d '
 {
   "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
   "sql": "SELECT * FROM accounts;",
   "name": "Sample Accelerated Query",
   "description": "A sample of an accelerated query."
 }
'
```

此替代請求會將請求內文中的範本ID提交至加速儲存。 來自相應模板的SQL用於查詢加速儲存。

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/acceleated-queries
 -H 'Authorization: {ACCESS_TOKEN}'
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}'
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'Content-Type: application/json' \
 -H 'Accept: application/json' \
 -d '
 {
   "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
   "templateId": "5d8228e7-4200-e3de-11e9-7f27416c5f0d",
   "name": "Sample Accelerated Query",
   "description": "A sample of an accelerated query."
 }
'
```

| 屬性 | 說明 |
|---|---|
| `dbName` | 要對其進行加速查詢的資料庫的名稱。 的值 `dbName` 應採用 `{SANDBOX_NAME}:{ACCELERATED_STORE_DATABASE}.{ACCELERATED_STORE_SCHEMA}`. 提供的資料庫必須存在於加速儲存中，否則請求將導致錯誤。 您也必須確定 `x-sandbox-name` 中的標頭和沙箱名稱 `dbName` 請參閱相同的沙箱。 |
| `sql` | SQL陳述式字串。 允許的大小上限為1000000個字元。 |
| `templateId` | 在對 `/templates` 端點。 |
| `name` | 加速查詢的選用易記、描述性名稱。 |
| `description` | 關於查詢目的的可選注釋，以幫助其他用戶了解其目的。 允許的最大大小為1000位元組。 |

**回應**

成功的回應會以查詢建立的臨機架構傳回HTTP狀態200。

>[!NOTE]
>
>下列回應已為簡潔而截斷。

```json
{
  "queryId": "315a0a66-0fbb-4810-bc30-484cea5e0f1e",
  "resultsMeta": {
    "_adhoc": {
      "type": "object",
      "meta:xdmType": "object",
      "properties": {
                "Units": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_code_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_name_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_code": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_name": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_aggregation_NZSIOC": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Value": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Year": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Variable_category": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                },
                "Industry_code_ANZSIC06": {
                    "type": "string",
                    "meta:xdmType": "string",
                    "default": null
                }
            }
        }
    },
  "results": [
     {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H26",
            "Variable_name": "Fixed tangible assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "282",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H27",
            "Variable_name": "Additions to fixed assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "35",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        {
            "Units": "Dollars (millions)",
            "Industry_code_NZSIOC": "CC411",
            "Industry_name_NZSIOC": "Printing",
            "Variable_code": "H28",
            "Variable_name": "Disposals of fixed assets",
            "Industry_aggregation_NZSIOC": "Level 4",
            "Value": "9",
            "Year": "2020",
            "Variable_category": "Financial position",
            "Industry_code_ANZSIC06": "ANZSIC06 groups C161 and C162"
        },
        ...
    ],
  "request": {
    "dbName": "acmesbox1:acmeacceldb:accmeaggschema",
    "sql": "SELECT * FROM accounts;",
    "name": "Sample Accelerated Query",
    "description": "A sample of an accelerated query."
  }
}
```

| 屬性 | 說明 |
|---|---|
| `queryId` | 已建立查詢的ID值。 |
| `resultsMeta` | 此物件包含結果中傳回之每欄的中繼資料，讓使用者知道每欄的名稱和類型。 |
| `resultsMeta._adhoc` | 臨機體驗資料模型(XDM)結構，其欄位的名稱是僅由單一資料集使用。 |
| `resultsMeta._adhoc.type` | 臨機結構的資料類型。 |
| `resultsMeta._adhoc.meta:xdmType` | 這是系統為XDM欄位類型產生的值。 如需可用類型的詳細資訊，請參閱 [可用的XDM類型](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/custom-fields-api.html). |
| `resultsMeta._adhoc.properties` | 這些是查詢資料集的欄名稱。 |
| `resultsMeta._adhoc.results` | 這些是查詢的資料集的列名稱。 它們會反映每個傳回的欄。 |
