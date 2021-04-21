---
keywords: Experience Platform; home；熱門主題；查詢服務；api指南；連接參數；查詢服務；
solution: Experience Platform
title: 連接參數API端點
topic-legacy: connection parameters
description: 通過向/connection_parameters端點發出GET請求，可檢索連接參數以使用互動式服務。
exl-id: 1667f4a5-e6e5-41e9-8f9d-6d2c63c7d7d6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 1%

---

# 連接參數端點

## 範例API呼叫

現在您已瞭解要使用哪些標題，可以開始呼叫[!DNL Query Service] API。 以下各節將介紹您可使用[!DNL Query Service] API進行的各種API呼叫。 每個呼叫都包含一般API格式、顯示必要標題的範例要求，以及範例回應。

### 請求連線參數

通過向`/connection_parameters`端點發出GET請求，可以檢索連接參數。 有關使用連接參數通過互動式服務進行連接的客戶端的詳細資訊，請閱讀[查詢服務客戶端](../clients/overview.md)上的文檔。

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

成功的回應會以您的連線參數傳回HTTP狀態200。

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
