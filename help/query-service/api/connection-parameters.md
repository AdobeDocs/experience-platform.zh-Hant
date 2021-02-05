---
keywords: Experience Platform;home;popular topics;query service;api guide;connection parameters;Query service;
solution: Experience Platform
title: 連接參數API端點
topic: connection parameters
description: 通過向/connection_parameters端點發出GET請求，可以檢索連接參數以使用互動式服務。
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
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

**請求**

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
