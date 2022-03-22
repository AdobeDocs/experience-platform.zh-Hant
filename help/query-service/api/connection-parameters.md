---
keywords: Experience Platform；首頁；熱門主題；查詢服務；api指南；連接參數；查詢服務；
solution: Experience Platform
title: 連接參數API終結點
topic-legacy: connection parameters
description: 通過向/connection_parameters端點發出GET請求，可檢索用於使用互動式服務的連接參數。
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: cff95575530e0db00d34ff1ea4c90e5422b6562d
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 1%

---

# 連接參數終結點

## 示例API調用

以下部分將引導您完成可以使用 [!DNL Query Service] API。 該調用包括一般API格式、顯示所需標頭的示例請求和示例響應。

### 請求連接參數

可通過向Web站點發出GET請求來檢索連接參數 `/connection_parameters` 端點。 有關使用連接參數通過互動式服務進行連接的客戶端的詳細資訊，請閱讀有關 [查詢服務客戶端](../clients/overview.md)。

**API格式**

```http
GET /connection_parameters
```

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/connection_parameters
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應將返回HTTP狀態200，並返回連接參數。

```json
{
    "username": "{USERNAME}",
    "dbName": "prod:all",
    "host": "{HOSTNAME}",
    "version": 1,
    "port": 80,
    "token": "{TOKEN}",
    "compressedToken": "{COMPRESSED_TOKEN}",
    "websocketHost": "{WEBSOCKET_HOSTNAME}"
}
```
