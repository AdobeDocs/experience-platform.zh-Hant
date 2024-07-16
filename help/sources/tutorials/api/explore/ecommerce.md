---
keywords: Experience Platform；首頁；熱門主題；電子商務；電子商務
solution: Experience Platform
title: 使用流量服務API探索電子商務連線
description: 本教學課程使用流程服務API來探索電子商務連線。
exl-id: 832ce399-6c9f-40da-8e7c-5434503c16b6
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 13%

---

# 使用[!DNL Flow Service] API探索電子商務連線

[!DNL Flow Service]用於收集及集中來自Adobe Experience Platform內各種不同來源的客戶資料。 此服務提供使用者介面和RESTful API，所有支援的來源都可從此API連線。

此教學課程使用[!DNL Flow Service] API來探索第三方&#x200B;**[!UICONTROL 電子商務]**&#x200B;連線。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [[!DNL Sources]](../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Platform]服務來建構、加標籤及增強傳入資料。
* [[!DNL Sandboxes]](../../../../sandboxes/home.md)： [!DNL Experience Platform]提供的虛擬沙箱可將單一[!DNL Platform]執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線至&#x200B;**[!UICONTROL 電子商務]**&#x200B;連線。

### 取得連線ID

若要使用[!DNL Platform] API探索您的&#x200B;**[!UICONTROL 電子商務]**&#x200B;連線，您必須擁有有效的連線識別碼。 如果您還沒有要使用的&#x200B;**[!UICONTROL 電子商務]**&#x200B;連線，您可以透過下列教學課程來建立連線：

* [Shopify](../create/ecommerce/shopify.md)

### 讀取範例 API 呼叫

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用範例API呼叫慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集所需標頭的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都與特定的虛擬沙箱隔離。 對[!DNL Platform] API的所有請求都需要標頭，以指定將在其中執行作業的沙箱名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的媒體型別標頭：

* `Content-Type: application/json`

## 探索您的資料表

使用您的&#x200B;**[!UICONTROL 電子商務]**&#x200B;連線ID，您可以透過執行GET請求來探索資料表。 使用以下呼叫來尋找您要檢查或擷取至[!DNL Platform]的資料表的路徑。

**API格式**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
```

| 參數 | 說明 |
| --- | --- |
| `{CONNECTION_ID}` | 您的&#x200B;**[!UICONTROL 電子商務]**&#x200B;連線識別碼。 |

**要求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會從您的&#x200B;**[!UICONTROL 電子商務]**&#x200B;連線傳回資料表陣列。 尋找您要帶入[!DNL Platform]的資料表並記下其`path`屬性，因為您必須在下個步驟中提供它以檢查其結構。

```json
[
    {
        "type": "table",
        "name": "Shopify.Abandoned_Checkout_Discount_Codes",
        "path": "Shopify.Abandoned_Checkout_Discount_Codes",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Abandoned_Checkout_Line_Items",
        "path": "Shopify.Abandoned_Checkout_Line_Items",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Blogs",
        "path": "Shopify.Blogs",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Shopify.Orders",
        "path": "Shopify.Orders",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect表格的結構

若要從您的&#x200B;**[!UICONTROL 電子商務]**&#x200B;連線檢查資料表的結構，請在指定`object`查詢引數中的資料表路徑時執行GET要求。

**API格式**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 您的&#x200B;**[!UICONTROL 電子商務]**&#x200B;連線的連線識別碼。 |
| `{TABLE_PATH}` | 您的&#x200B;**[!UICONTROL 電子商務]**&#x200B;連線中的資料表路徑。 |

**要求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=table&object=Orders' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回指定資料表的結構。 有關每個資料表資料行的詳細資料位於`columns`陣列的元素中。

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Blog_Id",
                "type": "double",
                "xdm": {
                    "type": "number"
                }
            },
            {
                "name": "Title",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Created_At",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
            {
                "name": "Tags",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            }
        ]
    },
    "data": [
        {
            "Updated_At": "2020-11-05T10:54:36",
            "Title": "News",
            "Commentable": "no",
            "Blog_Id": 5.5458332804E10,
            "Handle": "news",
            "Created_At": "2020-02-14T09:11:15"
        }
    ]
}
```

## 後續步驟

依照本教學課程，您已探索您的&#x200B;**[!UICONTROL 電子商務]**&#x200B;連線，找到您要擷取至[!DNL Platform]的資料表路徑，並取得有關其結構的資訊。 您可以在下一個教學課程中使用此資訊，以[收集電子商務資料並將其帶入Platform](../collect/ecommerce.md)。
