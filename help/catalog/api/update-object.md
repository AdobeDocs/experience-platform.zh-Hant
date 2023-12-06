---
keywords: Experience Platform；首頁；熱門主題；目錄；api；更新物件
solution: Experience Platform
title: 更新目錄物件
description: 您可以在PATCH請求的路徑中包含目錄物件的ID，以更新其一部分。 本文介紹如何使用欄位和使用JSON修補程式標籤法，對目錄物件執行PATCH作業。
exl-id: 315de212-bf4d-40d5-a54f-9602a26d6852
source-git-commit: 296a988a67871933723ad0474c113cb93fdbf255
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 2%

---

# 更新目錄物件

您可以更新部分 [!DNL Catalog] 物件，方法是在PATCH請求的路徑中包含其ID。 本文介紹在目錄物件上執行PATCH作業的兩種方法：

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
| `{OBJECT_TYPE}` | 型別 [!DNL Catalog] 要更新的物件。 有效的物件包括： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | 您要更新之特定物件的識別碼。 |

**要求**

以下請求會更新 `name` 和 `description` 資料集的欄位對應到承載中提供的值。 您可從承載中排除不需要更新的物件欄位。

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

成功的回應會傳回陣列，其中包含已更新資料集的ID。 此ID應符合PATCH請求中傳送的ID。 為此資料集執行GET要求現在只會顯示 `name` 和 `description` 已更新，而所有其他值維持不變。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

## 使用JSON修補程式標籤法更新

下列範例呼叫示範如何使用JSON修補程式更新物件，如中所述 [RFC-6902](https://tools.ietf.org/html/rfc6902).

如需JSON修補程式語法的詳細資訊，請參閱 [API基礎指南](../../landing/api-fundamentals.md#json-patch).

**API格式**

```http
PATCH /{OBJECT_TYPE}/{OBJECT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{OBJECT_TYPE}` | 型別 [!DNL Catalog] 要更新的物件。 有效的物件包括： <ul><li>`batches`</li><li>`dataSets`</li><li>`dataSetFiles`</li></ul> |
| `{OBJECT_ID}` | 您要更新之特定物件的識別碼。 |

**要求**

以下請求會更新 `name` 和 `description` 資料集的欄位對應到每個JSON修補程式物件中提供的值。 使用JSON修補程式時，您還必須將Content-Type標頭設為 `application/json-patch+json`.

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

成功的回應會傳回包含已更新物件ID的陣列。 此ID應符合PATCH請求中傳送的ID。 執行此物件的GET要求現在只會顯示 `name` 和 `description` 已更新，而所有其他值維持不變。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```
