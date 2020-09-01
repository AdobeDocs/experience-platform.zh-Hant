---
keywords: Experience Platform;home;popular topics;query service;api guide;connection parameters;Query service;
solution: Experience Platform
title: 查詢服務開發人員指南
topic: connection parameters
translation-type: tm+mt
source-git-commit: c5d3be4706ca6d6a30e203067db6ddc894b9bfb4
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 1%

---


# 連接參數

## 範例API呼叫

現在，您已瞭解要使用哪些標題，可以開始呼叫 [!DNL Query Service] API。 以下各節將介紹您可使用API進行的各種API [!DNL Query Service] 呼叫。 每個呼叫都包含一般API格式、顯示必要標題的範例要求，以及範例回應。

### 請求互動式服務的連接參數

通過向端點發出GET請求 [，可以檢索連接參](../creating-queries/writing-queries.md) 數以使用互動式服 `/connection_parameters` 務。 有關使用連接參數通過互動式服務進行連接的客戶端的詳細資訊，請閱讀查詢服務客戶端的 [文檔](../clients/overview.md)。

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
