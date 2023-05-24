---
keywords: Experience Platform；主題；熱門主題；資料準備；api指南；示例資料；
solution: Experience Platform
title: 示例資料API終結點
description: 可以使用Adobe Experience PlatformAPI中的「/samples」端點以寫程式方式檢索、建立、更新和驗證映射示例資料。
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 5%

---


# 示例資料終結點

在為映射集建立架構時可以使用示例資料。 您可以使用 `/samples` 資料準備API中的端點，以寫程式方式檢索、建立和更新示例資料。

## 列出示例資料

您可以通過向以下站點發出GET請求來檢索組織的所有映射示例資料的清單 `/samples` 端點。

**API格式**

的 `/samples` 終結點支援多個查詢參數以幫助篩選結果。 當前，必須同時包括 `start` 和 `limit` 參數。

```http
GET /samples?limit={LIMIT}&start={START}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{LIMIT}` | **必填**. 指定返回的映射示例資料數。 |
| `{START}` | **必填**. 指定結果頁的偏移。 要獲取結果的第一頁，請將值設定為 `start=0`。 |

**要求**

以下請求將檢索您組織內的最後兩個映射示例資料。

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples?limit=2&start=0 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含映射示例資料的最後兩個對象的資訊。

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

## 建立示例資料

您可以通過向POST `/samples` 端點。

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

成功的響應返回HTTP狀態200，其中包含有關新建立的示例資料的資訊。

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

## 通過上載檔案建立示例資料

您可以通過向Web站點發出POST請求來使用檔案建立示例資料 `/samples/upload` 端點。

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

成功的響應返回HTTP狀態200，其中包含有關新建立的示例資料的資訊。

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

通過在GET請求到的路徑中提供示例資料的ID，可以查找示例資料的特定對象 `/samples` 端點。

**API格式**

```http
GET /samples/{SAMPLE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SAMPLE_ID}` | 要檢索的示例資料對象的ID。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/samples/1fc0b6c20bae49d8ab33209ed126bdcd \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含要檢索的示例資料對象的資訊。

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

## 更新示例資料

通過在PUT請求路徑中提供特定示例資料對象的ID，可以更新特定示例資料對象 `/samples` 端點。

**API格式**

```http
PUT /samples/{SAMPLE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{SAMPLE_ID}` | 要更新的示例資料對象的ID。 |

**要求**

以下請求更新指定的示例資料。 具體來說，它將姓氏從&quot;史密斯&quot;更新為&quot;李&quot;。

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

成功的響應返回HTTP狀態200，其中包含有關更新的示例資料的資訊。

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
