---
keywords: Experience Platform；首頁；熱門主題；查詢服務；api指南；連線參數；查詢服務；
solution: Experience Platform
title: 連線參數API端點
description: 通過向/connection_parameters端點發出GET請求，可以檢索連接參數以使用互動式服務。
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 1%

---

# 連接參數端點

## 範例API呼叫

以下小節會逐步帶您了解您可使用 [!DNL Query Service] API。 呼叫包含一般API格式、顯示必要標題的範例要求，以及範例回應。

### 要求連線參數

您可以向 `/connection_parameters` 端點。 有關使用連接參數通過互動式服務進行連接的客戶端的詳細資訊，請閱讀 [查詢服務客戶端](../clients/overview.md).

**API格式**

```http
GET /connection_parameters
```

**要求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/connection_parameters
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回含有您連線參數的HTTP狀態200。

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
