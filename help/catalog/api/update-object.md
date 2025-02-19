---
keywords: Experience Platform；首頁；熱門主題；目錄；api；更新物件
solution: Experience Platform
title: 更新目錄物件
description: 您可以在PATCH請求的路徑中包含目錄物件的ID，以更新部分目錄物件。 本文介紹如何使用欄位和使用JSON修補程式標籤法，對目錄物件執行PATCH作業。
exl-id: 315de212-bf4d-40d5-a54f-9602a26d6852
source-git-commit: 5534cd5d5b0122ccbfcb3bae6c664c9f2d6eda8a
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 1%

---

# 更新目錄物件

您可以在PATCH要求的路徑中包含物件的ID，以更新[!DNL Catalog]物件的一部分。 本文介紹在目錄物件上執行PATCH作業的兩種方法：

* 使用欄位
* 使用JSON修補程式標籤法

>[!NOTE]
>
>物件上的PATCH作業無法修改其可展開的欄位，這些欄位代表相互關聯的物件。 必須直接修改相互關聯的物件。

## 使用欄位更新

下列範例呼叫示範如何使用欄位和值更新物件。

**API格式**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要更新的[!DNL Catalog]物件型別。 有效的物件包括： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | 您要更新之特定物件的識別碼。 |

**要求**

以下請求會將資料集的`name`和`description`欄位更新為承載中提供的值。 您可從承載中排除不需要更新的物件欄位。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
       "name":"Updated Dataset Name",
       "description":"Updated description for Sample Dataset"
      }'
```

**回應**

成功的回應會傳回陣列，其中包含已更新資料集的ID。 此ID應符合PATCH請求中傳送的ID。 針對此資料集執行GET要求時，現在會顯示只有`name`和`description`已更新，而所有其他值保持不變。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## 使用JSON修補程式標籤法更新 {#patch-notation}

下列範例呼叫示範如何使用JSON修補程式更新物件，如[RFC-6902](https://tools.ietf.org/html/rfc6902)中所述。

如需JSON修補程式語法的詳細資訊，請參閱[API基礎指南](../../landing/api-fundamentals.md#json-patch)。

**API格式**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 要更新的[!DNL Catalog]物件型別。 有效的物件包括： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | 您要更新之特定物件的識別碼。 |

**要求**

以下請求會將資料集的`name`和`description`欄位更新為每個JSON修補程式物件中提供的值。 使用JSON修補程式時，您也必須將Content-Type標頭設為`application/json-patch+json`。

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json-patch+json' \
  -d '[
        { "op": "add", "path": "/name", "value": "New Dataset Name" },
        { "op": "add", "path": "/description", "value": "New description for dataset" }
      ]'
```

**回應**

成功的回應會傳回包含已更新物件ID的陣列。 此ID應符合PATCH請求中傳送的ID。 針對此物件執行GET要求時，現在會顯示只有`name`和`description`已更新，而所有其他值保持不變。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## 使用PATCH v2標籤法更新 {#patch-v2-notation}

`/v2/dataSets/{DATASET_ID}`端點提供更靈活的方式，可更新複雜或深度巢狀資料集屬性。

通常，當您更新深層巢狀欄位（例如`a.b.c.d`）時，路徑中的每個層級都必須已存在。 如果缺少任何層級，您必須在設定最終值之前手動建立每個層級。 這通常需要多項作業，因而增加複雜度並增加錯誤發生率。

`/v2/dataSets/{DATASET_ID}`端點會自動在路徑中建立任何遺漏的層級。 PATCH `v2`作業不是在設定`d`之前手動檢查並新增`b`和`c`，而是為您執行此操作。

當您傳送PATCH要求至`/v2/dataSets/{DATASET_ID}`端點時，您只需要傳送最終結構，而且系統會在套用更新之前填入缺少的部分。

>[!NOTE]
>
>`/v2/dataSets/{id}`端點的`If-Match`和`If-None-Match`標頭為選用。 對此端點的PATCH請求會動態合併更新，從而允許進行修改而不擷取最新的資料集版本。 雖然這樣可以減少同時更新造成資料遺失的風險，但您可以搭配最新的`etag`使用`If-Match`，以確保變更僅套用至特定版本。 或者，如果資料集自上次已知版本以來未變更，`If-None-Match`可防止更新。

**API格式**

```http
PATCH /V2/DATASETS/{DATASET_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 要更新的資料集的識別碼。 |

**要求**

```shell
curl -X PATCH https://platform.adobe.io/data/foundation/catalog/v2/dataSets/67b3077efa10d92ab7a71858 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "extensions": {
            "adobe_lakeHouse": {
            "rowExpiration": {
                "ttlValue": "P9Y"
            }
            }
        }
    }'
```

**回應**

成功的回應會傳回陣列，內含更新資料集的ID，且此ID應符合PATCH請求中傳送的ID。 現在執行此物件的GET要求時，會顯示`extensions.adobe_lakeHouse.rowExpiration`物件已建立，不需要先執行手動建立步驟。

```json
[
    "@/dataSets/67b3077efa10d92ab7a71858"
]
```

### 更新前後範例資料集

以下範例JSON說明資料集結構&#x200B;**在** PATCH請求之前，其中`extensions.adobe_lakeHouse.rowExpiration`物件不存在於資料集中。

+++選取以檢視範例

```JSON
{
    "67b3077efa10d92ab7a71858": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "tags": {
            "adobe/siphon/table/format": [
                "delta"
            ],
            "adobe/pqs/table": [
                "testdataset_20250217_095510_966"
            ]
        },
        "classification": {
            "dataBehavior": "time-series",
            "managedBy": "CUSTOMER"
        },
        "createdUser": "{USER_ID}",
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "createdClient": "{CLIENT_ID}",
        "updatedUser": "{USER_ID}",
        "version": "1.0.0",
        "extensions": {
            "adobe_lakeHouse": {},
            "adobe_unifiedProfile": {}
        },
        "created": 1739786110978,
        "updated": 1739786111203,
        "viewId": "{VIEW_ID}",
        "basePath": "{STORAGE_PATH}",
        "fileDescription": {},
        "files": "@/dataSetFiles?dataSetId=67b3077efa10d92ab7a71858",
        "schemaRef": {
            "id": "{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed+json; version=1"
        },
        "persistence": {
            "adls": {
                "location": "{STORAGE_PATH}",
                "adlsType": "GEN2",
                "credentials": "@/dataSets/67b3077efa10d92ab7a71858/credentials"
            }
        }
    }
}
```

+++

下列JSON會在&#x200B;**PATCH請求之後顯示資料集結構**。 更新會自動建立遺失的`extensions.adobe_lakeHouse.rowExpiration`物件，不需要先執行手動建立步驟。 此範例示範`/v2/` PATCH要求如何免除多重作業的需求，讓更新更簡單、更有效率。


+++選取以檢視範例

```JSON
{
    "67b3077efa10d92ab7a71858": {
        "name": "Acme Sales Data",
        "description": "This dataset contains sales transaction records for Acme Corporation.",
        "tags": {
            "adobe/siphon/table/format": [
                "delta"
            ],
            "adobe/pqs/table": [
                "testdataset_20250217_095510_966"
            ]
        },
        "imsOrg": "{ORG_ID}",
        "sandboxId": "{SANDBOX_ID}",
        "extensions": {
            "adobe_lakeHouse": {
                "rowExpiration": {
                    "ttlValue": "{TTL_VALUE}"
                }
            },
            "adobe_unifiedProfile": {}
        },
        "version": "{VERSION}",
        "created": "{CREATED_TIMESTAMP}",
        "updated": "{UPDATED_TIMESTAMP}",
        "createdClient": "{CLIENT_ID}",
        "createdUser": "{USER_ID}",
        "updatedUser": "{USER_ID}",
        "classification": {
            "dataBehavior": "time-series",
            "managedBy": "CUSTOMER"
        },
        "viewId": "{VIEW_ID}",
        "basePath": "{STORAGE_PATH}",
        "fileDescription": {},
        "files": "@/dataSetFiles?dataSetId=67b3077efa10d92ab7a71858",
        "schemaRef": {
            "id": "{SCHEMA_ID}",
            "contentType": "{CONTENT_TYPE}"
        },
        "persistence": {
            "adls": {
                "location": "{STORAGE_PATH}",
                "adlsType": "{STORAGE_TYPE}",
                "credentials": "@/dataSets/67b3077efa10d92ab7a71858/credentials"
            }
        }
    }
}
```

+++
