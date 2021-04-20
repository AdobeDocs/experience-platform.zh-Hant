---
keywords: Experience Platform; home；熱門主題；資料準備；api指南；示例資料；
solution: Experience Platform
title: 範例資料API端點
topic: sample data
description: '您可以使用Adobe Experience PlatformAPI中的「/samples」端點，以程式設計方式擷取、建立、更新及驗證對應範例資料。 '
translation-type: tm+mt
source-git-commit: a2c966ae2401faa572cbba974ce6f572d5280a8f
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 4%

---


# 範例資料端點

為映射集建立架構時可使用示例資料。 您可以使用資料準備API中的`/samples`端點，以程式設計方式擷取、建立和更新範例資料。

## 列出範例資料

您可以向`/samples`端點提出GET請求，以檢索IMS組織的所有映射示例資料清單。

**API格式**

`/samples`端點支援數個查詢參數，以協助篩選結果。 目前，您必須同時包含`start`和`limit`參數，做為請求的一部分。

```http
GET /samples?limit={LIMIT}&start={START}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{LIMIT}` | **必填**. 指定傳回的映射範例資料數。 |
| `{START}` | **必填**. 指定結果頁的偏移。 若要取得第一頁的結果，請將值設定為`start=0`。 |

**請求**

下列請求將擷取您IMS組織內最後兩個對應範例資料。

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples?limit=2&start=0 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含映射範例資料的最後兩個物件的相關資訊。

```json
{
    "data": [
        {
            "id": "2a429a0057ce47109a4b3e2bc256d755",
            "version": 0,
            "createdDate": 1582250863000,
            "modifiedDate": 1582250863000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "sampleData": "{\"id\":\"\",\"first_name\":\"\",\"last_name\":\"\",\"email\":\"\",\"gender\":\"\",\"ip_address\":\"\"}",
            "sampleType": "JSON"
        },
        {
            "id": "0248bfb352214f908bdd6cf9c19447e1",
            "version": 0,
            "createdDate": 1582250892000,
            "modifiedDate": 1582250892000,
            "createdBy": "acp_xql_gateway",
            "modifiedBy": "acp_xql_gateway",
            "sampleData": "{\"id\":\"\",\"first_name\":\"\",\"last_name\":\"\",\"email\":\"\",\"gender\":\"\",\"ip_address\":\"\"}",
            "sampleType": "JSON"
        }
    ],
    "_page": {
        "count": 2,
        "limit": 2
    }
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `sampleData` |  |
| `sampleType` |  |

## 建立範例資料

您可以向`/samples`端點發出POST請求，以建立示例資料。

```http
POST /samples
```

**請求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Smith\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含您新建立之範例資料的相關資訊。

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 0,
    "createdDate": 1615335404492,
    "modifiedDate": 1615335404492,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## 上傳檔案以建立範例資料

通過向`/samples/upload`端點發出POST請求，可以使用檔案建立示例資料。

**API格式**

```http
POST /samples/upload
```

**請求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: multipart/form-data' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -F 'file=@{PATH_TO_FILE}.json'
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含您新建立之範例資料的相關資訊。

```json
{
    "id": "1fb33209ed126bdcdc0b6c20bae49d8a",
    "version": 0,
    "createdDate": 1615335404492,
    "modifiedDate": 1615335404492,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## 查找特定的示例資料對象

您可在`/samples`端點的GET請求路徑中提供範例資料的特定物件ID，以尋找範例資料。

**API格式**

```http
GET /samples/{SAMPLE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SAMPLE_ID}` | 您要擷取之範例資料物件的ID。 |

**請求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含您要擷取之範例資料物件的資訊。

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 0,
    "createdDate": 1615335404000,
    "modifiedDate": 1615335404000,
    "createdBy": "{CREATED_BY}",
    "modifiedBy": "{MODIFIED_BY}",
    "sampleData": "{\"FirstName\":\"carl\",\"LastName\":\"hooper\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```

## 更新範例資料

您可以在`/samples`端點的PUT請求路徑中提供特定樣本資料對象的ID，以更新該對象。

**API格式**

```http
PUT /samples/{SAMPLE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SAMPLE_ID}` | 您要更新之範例資料物件的ID。 |

**請求**

下列請求會更新指定的範例資料。 具體來說，它會將姓氏從&quot;Smith&quot;更新為&quot;Lee&quot;。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Lee\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含更新範例資料的相關資訊。

```json
{
    "id": "1fc0b6c20bae49d8ab33209ed126bdcd",
    "version": 1,
    "createdDate": 1615335404000,
    "modifiedDate": 1615337870375,
    "createdBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "modifiedBy": "CAEB5DE75E6FBFAC0A494110@techacct.adobe.com",
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Lee\", \"id\": \"123456\"}",
    "sampleType": "JSON"
}
```
