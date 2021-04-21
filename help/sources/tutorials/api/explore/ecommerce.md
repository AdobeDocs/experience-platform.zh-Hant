---
keywords: Experience Platform；首頁；熱門主題；電子商務；電子商務
solution: Experience Platform
title: 使用Flow Service API探索電子商務連線
topic-legacy: overview
description: 本教學課程使用Flow Service API來探索電子商務連線。
exl-id: 832ce399-6c9f-40da-8e7c-5434503c16b6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 2%

---

# 使用[!DNL Flow Service] API探索電子商務連線

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使用[!DNL Flow Service] API來探索協力廠商&#x200B;**[!UICONTROL eCommerce]**&#x200B;連線。

## 快速入門

本指南需要對Adobe Experience Platform的下列組成部分有切實的瞭解：

* [[!DNL Sources]](../../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [[!DNL Sandboxes]](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您需要瞭解的其他資訊，以便使用[!DNL Flow Service] API成功連線至&#x200B;**[!UICONTROL eCommerce]**&#x200B;連線。

### 取得連線ID

要使用[!DNL Platform] API來探索&#x200B;**[!UICONTROL eCommerce]**&#x200B;連接，您必須擁有有效的連接ID。 如果您尚未建立要使用的&#x200B;**[!UICONTROL eCommerce]**&#x200B;連線，則可以透過下列教學課程建立連線：

* [Shopify](../create/ecommerce/shopify.md)

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集必要標題的值

若要呼叫[!DNL Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程後，所有[!DNL Experience Platform] API呼叫中每個所需標題的值都會顯示在下面：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都隔離到特定的虛擬沙盒。 對[!DNL Platform] API的所有請求都需要一個標題，該標題指定要在中執行操作的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要附加的媒體類型標題：

* `Content-Type: application/json`

## 探索您的資料表格

使用&#x200B;**[!UICONTROL eCommerce]**&#x200B;連接ID，您可以執行GET請求來瀏覽資料表。 使用以下調用查找要檢查或裝入[!DNL Platform]的表的路徑。

**API格式**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
```

| 參數 | 說明 |
| --- | --- |
| `{CONNECTION_ID}` | 您的&#x200B;**[!UICONTROL eCommerce]**&#x200B;連線ID。 |

**要求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應從&#x200B;**[!UICONTROL eCommerce]**&#x200B;連接返回表陣列。 查找要帶入[!DNL Platform]的表，並記下其`path`屬性，因為在下一步中需要提供該表來檢查其結構。

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

## Inspect桌子的結構

要從&#x200B;**[!UICONTROL eCommerce]**&#x200B;連接檢查表的結構，請在指定`object`查詢參數內表的路徑時執行GET請求。

**API格式**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | **[!UICONTROL eCommerce]**&#x200B;連接的連接ID。 |
| `{TABLE_PATH}` | **[!UICONTROL eCommerce]**&#x200B;連接中表的路徑。 |

**要求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=table&object=Orders' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回指定表的結構。 有關每個表列的詳細資訊位於`columns`陣列的元素中。

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

通過本教程，您已探索了&#x200B;**[!UICONTROL eCommerce]**&#x200B;連接，找到了要嵌入[!DNL Platform]的表的路徑，並獲取了有關其結構的資訊。 您可以在下一個教學課程中使用這項資訊來收集電子商務資料，並將其匯入Platform](../collect/ecommerce.md)。[
