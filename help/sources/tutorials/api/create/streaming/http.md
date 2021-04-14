---
keywords: Experience Platform;home；熱門主題；流連接；建立流連接；api指南；教學課程；建立流連接；流攝取；攝取；
solution: Experience Platform
title: 使用API建立串流連線
topic: 教學課程
type: Tutorial
description: 本教學課程將協助您開始使用串流擷取API，這是Adobe Experience Platform資料擷取服務API的一部分。
exl-id: 9f7fbda9-4cd3-4db5-92ff-6598702adc34
translation-type: tm+mt
source-git-commit: 69abc982c4a820b850096d83761552ca526bca29
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 2%

---


# 使用API建立串流連線

Flow Service用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使用[!DNL Flow Service] API來引導您逐步執行使用Flow Service API建立串流連線的步驟。

## 快速入門

本指南需要對Adobe Experience Platform的下列組成部分有切實的瞭解：

- [[!DNL Experience Data Model (XDM)]](../../../../../xdm/home.md):組織體驗資料的 [!DNL Platform] 標準化架構。
- [[!DNL Real-time Customer Profile]](../../../../../profile/home.md):根據來自多個來源的匯整資料，即時提供統一的消費者個人檔案。

以下章節提供您需要知道的其他資訊，以便成功呼叫串流擷取API。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

- 授權：載體`{ACCESS_TOKEN}`
- x-api-key:`{API_KEY}`
- x-gw-ims-org-id:`{IMS_ORG}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

- x-sandbox-name:`{SANDBOX_NAME}`

>[!NOTE]
>
>如需[!DNL Platform]中沙盒的詳細資訊，請參閱[沙盒概述檔案](../../../../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型：application/json

## 建立連線

連線會指定來源，並包含讓流與串流擷取API相容所需的資訊。 建立連接時，您可以選擇建立未驗證和已驗證的連接。

### 非驗證連接

非驗證連線是您在要將資料串流至平台時，可建立的標準串流連線。

**API格式**

```http
POST /flowservice/connections
```

**請求**

為了建立串流連線，必須在POST請求中提供提供者ID和連線規格ID。 提供程式ID為`521eee4d-8cbe-4906-bb48-fb6bd4450033`，連接規範ID為`bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`。

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection"
         }
     }
 }
```

| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.sourceId` | 您要建立的串流連線ID。 |
| `auth.params.dataType` | 串流連線的資料類型。 此值必須為`xdm`。 |
| `auth.params.name` | 您要建立的串流連線名稱。 |
| `connectionSpec.id` | 串流連接的連接規範`id`。 |

**回應**

成功的回應會傳回HTTP狀態201，並包含新建連線的詳細資訊，包括其唯一識別碼(`id`)。

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 新建立的連接的`id`。 這在這裡稱為`{CONNECTION_ID}`。 |
| `etag` | 指派給連接的標識符，指定連接的修訂版本。 |

### 已驗證的連接

當您需要區分來自受信任來源和不受信任來源的記錄時，應使用已驗證的連線。 想要傳送包含個人識別資訊(PII)的資訊的使用者，在將資訊串流至平台時，應建立已驗證的連線。

**API格式**

```http
POST /flowservice/connections
```

**請求**

為了建立串流連線，必須在POST請求中提供提供者ID和連線規格ID。 提供程式ID為`521eee4d-8cbe-4906-bb48-fb6bd4450033`，連接規範ID為`bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb`。

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample streaming connection",
     "providerId": "521eee4d-8cbe-4906-bb48-fb6bd4450033",
     "description": "Sample description",
     "connectionSpec": {
         "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
         "version": "1.0"
     },
     "auth": {
         "specName": "Streaming Connection",
         "params": {
             "sourceId": "Sample connection",
             "dataType": "xdm",
             "name": "Sample connection",
             "authenticationRequired": true
         }
     }
 }
```


| 屬性 | 說明 |
| -------- | ----------- |
| `auth.params.sourceId` | 您要建立的串流連線ID。 |
| `auth.params.dataType` | 串流連線的資料類型。 此值必須為`xdm`。 |
| `auth.params.name` | 您要建立的串流連線名稱。 |
| `auth.params.authenticationRequired` | 指定已建立的串流連接的參數 |
| `connectionSpec.id` | 串流連接的連接規範`id`。 |

**回應**

成功的回應會傳回HTTP狀態201，並包含新建連線的詳細資訊，包括其唯一識別碼(`id`)。

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 新建立的連接的`id`。 這在這裡稱為`{CONNECTION_ID}`。 |
| `etag` | 指派給連接的標識符，指定連接的修訂版本。 |

## 取得串流端點URL

建立連線後，您現在可以擷取串流端點URL。

**API格式**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 您先前建立的連接的`id`值。 |

**請求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含所請求連接的詳細資訊。 串流端點URL會自動與連線建立，並可使用`inletUrl`值來擷取。

```json
{
    "items": [
        {
            "createdAt": 1583971856947,
            "updatedAt": 1583971856947,
            "createdBy": "{API_KEY}",
            "updatedBy": "{API_KEY}",
            "createdClient": "{USER_ID}",
            "updatedClient": "{USER_ID}",
            "id": "77a05521-91d6-451c-a055-2191d6851c34",
            "name": "Another new sample connection (Experience Event)",
            "description": "Sample description",
            "connectionSpec": {
                "id": "bc7b00d6-623a-4dfc-9fdb-f1240aeadaeb",
                "version": "1.0"
            },
            "state": "enabled",
            "auth": {
                "specName": "Streaming Connection",
                "params": {
                    "sourceId": "Sample connection (ExperienceEvent)",
                    "inletUrl": "https://dcs.adobedc.net/collection/a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "inletId": "a868e1ce678a911ef1482b083329af3cafa4bafdc781285f25911eaae9e00eb2",
                    "dataType": "xdm",
                    "name": "Sample connection (ExperienceEvent)"
                }
            },
            "version": "\"56008aee-0000-0200-0000-5e697e150000\"",
            "etag": "\"56008aee-0000-0200-0000-5e697e150000\""
        }
    ]
}
```

## 後續步驟

在本教學課程中，您已建立串流HTTP連線，讓您使用串流端點將資料內嵌至平台。 有關在UI中建立流連接的說明，請閱讀[建立流連接教程](../../../ui/create/streaming/http.md)。

要瞭解如何將資料串流至平台，請閱讀有關[串流時間系列資料](../../../../../ingestion/tutorials/streaming-time-series-data.md)的教學課程，或有關[串流記錄資料](../../../../../ingestion/tutorials/streaming-record-data.md)的教學課程。

## 附錄

本節提供有關使用API建立串流連線的補充資訊。

### 傳送訊息至已驗證的串流連線

如果串流連線已啟用驗證，則用戶端需要將`Authorization`標題新增至其請求。

如果`Authorization`標題不存在，或傳送無效／過期的存取Token，則會傳回HTTP 401未授權回應，回應類似如下：

**回應**

```json
{
    "type": "https://ns.adobe.com/adobecloud/problem/data-collection-service-authorization",
    "status": "401",
    "title": "Authorization",
    "report": {
        "message": "[id] Ims service token is empty"
    }
}
```
