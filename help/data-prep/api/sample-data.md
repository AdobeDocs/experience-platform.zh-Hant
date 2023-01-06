---
keywords: Experience Platform；首頁；熱門主題；資料準備；api指南；範例資料；
solution: Experience Platform
title: 範例資料API端點
description: 您可以使用Adobe Experience Platform API中的「/samples」端點，以程式設計方式擷取、建立、更新及驗證對應範例資料。
source-git-commit: d39ae3a31405b907f330f5d54c91b95c0f999eee
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 4%

---


# 範例資料端點

為對應集建立架構時，可使用範例資料。 您可以使用 `/samples` 資料準備API中的端點，以程式設計方式擷取、建立和更新範例資料。

## 清單範例資料

您可以向提出GET要求，以擷取IMS組織的所有對應範例資料清單 `/samples` 端點。

**API格式**

此 `/samples` 端點支援數個查詢參數，可協助篩選結果。 目前，您必須同時包含 `start` 和 `limit` 參數。

```http
GET /samples?limit={LIMIT}&start={START}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{LIMIT}` | **必填**. 指定返回的映射示例資料的數量。 |
| `{START}` | **必填**. 指定結果頁的偏移。 若要取得結果的第一頁，請將值設為 `start=0`. |

**要求**

下列請求會在您的IMS組織內擷取最後兩個對應範例資料。

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples?limit=2&start=0 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含對應範例資料的最後兩個物件的相關資訊。

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

您可以透過向 `/samples` 端點。

```http
POST /samples
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Smith\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含新建立範例資料的相關資訊。

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

您可以透過向 `/samples/upload` 端點。

**API格式**

```http
POST /samples/upload
```

**要求**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/samples \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: multipart/form-data' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -F 'file=@{PATH_TO_FILE}.json'
```

**回應**

成功的回應會傳回HTTP狀態200，並包含新建立範例資料的相關資訊。

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

您可以在GET要求的路徑中提供範例資料的ID，以便查詢其特定物件 `/samples` 端點。

**API格式**

```http
GET /samples/{SAMPLE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SAMPLE_ID}` | 您要擷取之範例資料物件的ID。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
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

您可以在PUT請求的路徑中提供特定範例資料物件ID給 `/samples` 端點。

**API格式**

```http
PUT /samples/{SAMPLE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SAMPLE_ID}` | 要更新的範例資料物件的ID。 |

**要求**

下列要求會更新指定的範例資料。 具體來說，姓氏從「Smith」更新為「Lee」。

```shell
curl -X PUT https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "sampleData": "{\"FirstName\":\"Johnson\",\"LastName\":\"Lee\", \"id\": \"3197210762560\"}",
    "sampleType": "JSON"    
  }'
```

**回應**

成功的回應會傳回HTTP狀態200，並附上更新範例資料的相關資訊。

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
