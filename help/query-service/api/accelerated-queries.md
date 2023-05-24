---
title: 加速查詢終結點
description: 瞭解如何以無狀態方式訪問查詢加速儲存，以快速返回基於聚合資料的結果。 此文檔提供查詢服務加速查詢終結點的示例HTTP請求和響應。
exl-id: 29ea4d25-9c46-4b29-a6d7-45ac33dcb0fb
source-git-commit: aa209dce9268a15a91db6e3afa7b6066683d76ea
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 1%

---

# 加速查詢終結點

作為資料DistillerSKU的一部分， [查詢服務API](https://developer.adobe.com/experience-platform-apis/references/query-service/) 允許您對加速儲存進行無狀態查詢。 返回的結果基於聚合資料。 結果延遲的減少允許更互動式的資訊交換。 加速查詢API還用於提供電源 [用戶定義的儀表板](../../dashboards/user-defined-dashboards.md)。

在繼續閱讀本指南之前，請確保您已閱讀並瞭解 [查詢服務API指南](./getting-started.md) 以便成功使用查詢服務API。

## 快速入門

資料DistillerSKU需要使用查詢加速儲存。 請參閱 [包裝](../packages.md) 和 [護欄](../guardrails.md#query-accelerated-store) 與資料DistillerSKU相關的文檔。 如果您沒有資料DistillerSKU，請聯繫您的Adobe客戶服務代表以獲取詳細資訊。

<!-- Document is hidden temporarily
Please see the [packaging](../packages.md), [guardrails](../guardrails.md#query-accelerated-store), and [licensing](../data-distiller/license-usage.md) documentation that relates to the Data Distiller SKU. 
-->

以下各節詳細介紹了通過查詢服務API以無狀態方式訪問查詢加速儲存所需的API調用。 每個調用包括一般API格式、顯示所需標頭的示例請求和示例響應。

## 運行加速查詢 {#run-accelerated-query}

向POST請求 `/accelerated-queries` 要運行加速查詢的終結點。 查詢直接包含在請求負載中，或使用模板ID引用。

**API格式**

```shell
POST /accelerated-queries
```

### 請求

>[!IMPORTANT]
>
>請求 `/accelerated-queries` 終結點需要SQL陳述式或模板ID，但不需要兩者。 在請求中提交這兩項都會導致錯誤。

以下請求將請求正文中的SQL查詢提交到加速儲存。

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

此備用請求將請求正文中的模板ID提交到加速儲存。 來自相應模板的SQL用於查詢加速儲存。

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
| `dbName` | 要對其進行加速查詢的資料庫的名稱。 的值 `dbName` 應採用 `{SANDBOX_NAME}:{ACCELERATED_STORE_DATABASE}.{ACCELERATED_STORE_SCHEMA}`。 所提供的資料庫必須存在於加速儲存中，否則請求將導致錯誤。 您還必須確保 `x-sandbox-name` 標頭和沙箱名稱 `dbName` 參考同一沙盒。 |
| `sql` | SQL陳述式字串。 允許的最大大小為100000個字元。 |
| `templateId` | 在向Web站點發出POST請求時，建立並另存為模板的查詢的唯一標識符 `/templates` 端點。 |
| `name` | 加速查詢的可選人性化描述性名稱。 |
| `description` | 有關查詢意圖的可選注釋，以幫助其他用戶瞭解其目的。 允許的最大大小為1000位元組。 |

**回應**

成功的響應返回HTTP狀態200，並且查詢建立了臨時架構。

>[!NOTE]
>
>以下響應已被截斷以便簡化。

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
| `queryId` | 建立的查詢的ID值。 |
| `resultsMeta` | 此對象包含結果中返回的每個列的元資料，以便用戶知道每個列的名稱和類型。 |
| `resultsMeta._adhoc` | 一種即席體驗資料模型(XDM)架構，其欄位僅由單個資料集使用而命名。 |
| `resultsMeta._adhoc.type` | 即席架構的資料類型。 |
| `resultsMeta._adhoc.meta:xdmType` | 這是系統為XDM欄位類型生成的值。 有關可用類型的詳細資訊，請參閱 [可用XDM類型](https://experienceleague.adobe.com/docs/experience-platform/xdm/tutorials/custom-fields-api.html)。 |
| `resultsMeta._adhoc.properties` | 這些是查詢的資料集的列名。 |
| `resultsMeta._adhoc.results` | 這些是查詢的資料集的行名。 它們反映每個返回的列。 |
