---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 使用API建立串流連線
topic: tutorial
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 2%

---


# 使用API建立串流連線

本教學課程將協助您開始使用串流擷取API，這是Adobe Experience Platform資料API的一 [!DNL Ingestion Service] 部分。

## 快速入門

必須註冊串流連線，才能開始將資料串流至Adobe Experience Platform。 在註冊串流連線時，您需要提供一些關鍵詳細資訊，例如串流資料來源。

在註冊串流連線後，身為資料產生者的您將擁有可用來將資料串流至平台的唯一URL。

本教學課程也需要具備各種Adobe Experience Platform服務的相關知識。 在開始本教學課程之前，請先閱讀下列服務的檔案：

- [[!DNL體驗資料模型(XDM)]](../../xdm/home.md):組織體驗資料的 [!DNL Platform] 標準化架構。
- [[!DNL即時客戶基本資料]](../../profile/home.md):根據來自多個來源的匯整資料，即時提供統一的消費者個人檔案。

以下章節提供您需要知道的其他資訊，以便成功呼叫串流擷取API。

### 讀取範例API呼叫

本指南提供範例API呼叫，以示範如何格式化您的請求。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

### 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

- 授權：生產者 `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

中的所有資 [!DNL Experience Platform] 源都與特定虛擬沙盒隔離。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>如需中沙盒的詳細資訊 [!DNL Platform]，請參閱沙 [盒概述檔案](../../sandboxes/home.md)。

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的標題：

- 內容類型：application/json

## 建立連線

連線會指定來源，並包含讓流與串流擷取API相容所需的資訊。

**API格式**

```http
POST /flowservice/connections
```

**請求**

>[!NOTE]
>
>必須使用列 `providerId` 出和的 `connectionSpec` 值 **** ，如示例中所示，因為它們是您為串流擷取建立串流連線的API所指定的值。

```shell
curl -X POST https://platform.adobe.io/data/foundation/flowservice/connections \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "name": "Sample name",
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

**回應**

成功的回應會傳回HTTP狀態201，並包含新建連線的詳細資訊。

```json
{
    "id": "77a05521-91d6-451c-a055-2191d6851c34",
    "etag": "\"a500e689-0000-0200-0000-5e31df730000\""
}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `id` | 新建 `id` 的連線的名稱。 這在這裡稱為 `{CONNECTION_ID}`。 |
| `etag` | 指派給連接的標識符，指定連接的修訂版本。 |

## 取得資料收集URL

建立連線後，您現在可以擷取資料收集URL。

**API格式**

```http
GET /flowservice/connections/{CONNECTION_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 您 `id` 先前建立的連接的值。 |

**請求**

```shell
curl -X GET https://platform.adobe.io/data/foundation/flowservice/connections/{CONNECTION_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含所請求連接的詳細資訊。 資料收集URL會自動與連線建立，並可使用值來擷 `inletUrl` 取。

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

現在您已建立串流連線，您可以串流化時間系列或記錄資料，讓您在其中內嵌資料 [!DNL Platform]。 若要瞭解如何將時間系列資料串流 [!DNL Platform]至，請前往串 [流時間系列資料教學課程](./streaming-time-series-data.md)。 若要瞭解如何將記錄資料串流 [!DNL Platform]至，請至串流 [記錄資料教學課程](./streaming-record-data.md)。

## 附錄

本節提供有關使用API建立串流連線的補充資訊。

### 驗證的串流連線

驗證資料收集可讓Adobe Experience Platform服務(例如 [!DNL Real-time Customer Profile] 和 [!DNL Identity])區隔來自受信任來源和不受信任來源的記錄。 想要傳送個人識別資訊(PII)的客戶可以透過傳送IMS存取Token作為POST要求的一部分進行傳送——如果IMS Token有效，則記錄會標示為從受信任來源收集。

如需建立已驗證串流連線的詳細資訊，請參閱建立已驗 [證串流連線教學課程](create-authenticated-streaming-connection.md)。