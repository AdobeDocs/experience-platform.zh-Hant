---
keywords: Experience Platform;home；熱門主題；資料集連接流服務；流服務；流服務連接
solution: Experience Platform
title: 使用Flow Service API建立Adobe Experience Platform資料集基本連線
topic-legacy: overview
type: Tutorial
description: 瞭解如何使用Flow Service API建立與Adobe Experience Platform的資料集基礎連線。
exl-id: 5e829f4a-954b-4011-a003-c42c7a0d5617
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 1%

---

# 使用[!DNL Flow Service] API建立[!DNL Experience Platform]資料集基本連線

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

為了將來自第三方源的資料連接到[!DNL Platform] ，必須首先建立資料集基礎連接。

本教學課程使用[!DNL Flow Service] API來引導您完成建立資料集基礎連線的步驟。

## 快速入門

本教學課程需要對Adobe Experience Platform的下列部分有正確的理解：

* [體驗資料模型(XDM)系統](../../../xdm/home.md):組織客戶體驗資 [!DNL Experience Platform] 料的標準化架構。
   * [架構構成基礎](../../../xdm/schema/composition.md):瞭解XDM架構的基本建置區塊，包括架構組合的主要原則和最佳實務。
   * [架構註冊開發人員指南](../../../xdm/api/getting-started.md):包含您必須知道的重要資訊，以便成功執行對架構註冊表API的呼叫。這包括您的`{TENANT_ID}`、&quot;containers&quot;的概念，以及提出要求時所需的標題（請特別注意「接受」標題及其可能的值）。
* [目錄服務](../../../catalog/home.md):目錄是記錄資料位置和世系的系統 [!DNL Experience Platform]。
* [批次擷取](../../../ingestion/batch-ingestion/overview.md):批次擷取API可讓您將資料以批次檔案的形式內嵌至Experience Platform。
* [沙盒](../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要瞭解的其他資訊，以便使用[!DNL Flow Service] API成功連線至資料湖。

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要附加的媒體類型標題：

* `Content-Type: application/json`

## 查找連接規格

建立資料集基本連接的第一步是從[!DNL Flow Service]內檢索一組連接規範。

**API格式**

每個可用源都有其唯一的連接規範集，用於描述連接器屬性（如驗證要求）。 您可以執行GET請求並使用查詢參數來查找資料集基本連接的連接規範。

傳送不含查詢參數的GET請求時，將傳回所有可用來源的連線規格。 您可以包含查詢`property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"`，以取得資料集基本連線的資訊。

```http
GET /connectionSpecs
GET /connectionSpecs?property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"
```

**要求**

下列請求會擷取資料集基礎連線的連線規格。

```shell
curl -X GET \
    'https://platform.adobe.io/data/foundation/flowservice/connectionSpecs?property=id=="c604ff05-7f1a-43c0-8e18-33bf874cb11c"' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回建立基本連接所需的連接規範和唯一標識符(`id`)。

```json
{
    "items": [
        {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "name": "{NAME}",
            "providerId": "0ed90a81-07f4-4586-8190-b40eccef1c5a",
            "version": "1.0",
            "targetSpec": {
                "spec": {
                    "$schema": "http://json-schema.org/draft-07/schema#",
                    "type": "object",
                    "properties": {
                        "dataSetId": {
                            "type": "string"
                        }
                    },
                    "required": [
                        "dataSetId"
                    ]
                }
            },
            "attributes": {
                "category": "{CATEGORY}"
            },
            "permissionsInfo": {
                "view": [
                    {
                        "@type": "lowLevel",
                        "name": "Dataset",
                        "permissions": [
                            "read"
                        ]
                    }
                ],
                "manage": [
                    {
                        "@type": "lowLevel",
                        "name": "Dataset",
                        "permissions": [
                            "write"
                        ]
                    }
                ]
            }
        }
    ]
}
```

## 建立資料集基礎連線

基本連接指定源，並包含該源的憑據。 只需要一個資料集基本連線，因為它可用來建立多個來源連接器，以匯入不同的資料。

**API格式**

```http
POST /connections
```

**要求**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dataset Base Connection",
        "description": "Dataset Base Connection",
        "connectionSpec": {
            "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
            "version": "1.0"
        }
    }'
```

| 屬性 | 說明 |
| ------------- | --------------- |
| `connectionSpec.id` | 在上一步中檢索的連接規範`id`。 |

**回應**

成功的響應返回新建立的基本連接的詳細資訊，包括其唯一標識符(`id`)。 此ID是建立目標連線並從協力廠商來源連接器擷取資料的必要ID。

```json
{
    "id": "d6c3988d-14ef-4000-8398-8d14ef000021",
    "etag": "\"d502e61b-0000-0200-0000-5e62a1f90000\""
}
```

## 後續步驟

在本教學課程中，您使用[!DNL Flow Service] API建立了資料集基礎連線，並取得了連線的唯一ID值。 您可以使用此基本連接建立目標連接。 下列教學課程將逐步說明建立目標連線的步驟，視您使用的來源連接器類別而定：

* [雲端儲存空間](./collect/cloud-storage.md)
* [CRM](./collect/crm.md)
* [客戶成功](./collect/customer-success.md)
* [資料庫](./collect/database-nosql.md)
