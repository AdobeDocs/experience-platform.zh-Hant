---
keywords: Experience Platform；首頁；熱門主題；電子商務；電子商務
solution: Experience Platform
title: 使用流服務API瀏覽電子商務連接
description: 本教程使用流服務API來瀏覽電子商務連接。
exl-id: 832ce399-6c9f-40da-8e7c-5434503c16b6
source-git-commit: 90eb6256179109ef7c445e2a5a8c159fb6cbfe28
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 2%

---

# 使用 [!DNL Flow Service] API

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供了用戶介面和REST風格的API，所有支援的源都可從中連接。

本教程使用 [!DNL Flow Service] API用於探索第三方 **[!UICONTROL 電子商務]** 連接。

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [[!DNL Sources]](../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [[!DNL Sandboxes]](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

以下各節提供了成功連接到 **[!UICONTROL 電子商務]** 使用 [!DNL Flow Service] API。

### 獲取連接ID

為了探索 **[!UICONTROL 電子商務]** 連接使用 [!DNL Platform] API，必須具有有效的連接ID。 如果尚未連接 **[!UICONTROL 電子商務]** 要使用的連接，您可以通過以下教程建立一個連接：

* [修改](../create/ecommerce/shopify.md)

### 讀取示例API調用

本教程提供了示例API調用，以演示如何格式化請求。 這些包括路徑、必需的標頭和正確格式化的請求負載。 還提供了API響應中返回的示例JSON。 有關示例API調用文檔中使用的約定的資訊，請參見上的 [如何讀取示例API調用](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) 的 [!DNL Experience Platform] 疑難解答指南。

### 收集所需標題的值

為了呼叫 [!DNL Platform] API，必須首先完成 [驗證教程](https://www.adobe.com/go/platform-api-authentication-en)。 完成身份驗證教程將提供所有中每個必需標頭的值 [!DNL Experience Platform] API調用，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

中的所有資源 [!DNL Experience Platform]包括那些 [!DNL Flow Service]，與特定虛擬沙箱隔離。 所有請求 [!DNL Platform] API需要一個標頭，該標頭指定操作將在以下位置進行的沙盒的名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含負載(POST、PUT、PATCH)的請求都需要附加的媒體類型報頭：

* `Content-Type: application/json`

## 瀏覽資料表

使用 **[!UICONTROL 電子商務]** 連接ID，您可以通過執行GET請求來瀏覽資料表。 使用以下調用查找要檢查或插入的表的路徑 [!DNL Platform]。

**API格式**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
```

| 參數 | 說明 |
| --- | --- |
| `{CONNECTION_ID}` | 您 **[!UICONTROL 電子商務]** 連接ID。 |

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

成功的響應會從 **[!UICONTROL 電子商務]** 連接。 查找要放入的表 [!DNL Platform] 並注意到 `path` 屬性，因為在下一步中需要提供該屬性來檢查其結構。

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

從 **[!UICONTROL 電子商務]** 連接，在指定表的路徑時執行GET請求 `object` 查詢參數。

**API格式**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 您的連接ID **[!UICONTROL 電子商務]** 連接。 |
| `{TABLE_PATH}` | 表在您 **[!UICONTROL 電子商務]** 連接。 |

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

成功的響應返回指定表的結構。 有關每個表列的詳細資訊位於 `columns` 陣列。

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

通過學完本教程，您已探索了 **[!UICONTROL 電子商務]** 連接，找到要插入的表的路徑 [!DNL Platform]並獲取了有關其結構的資訊。 您可以在下一教程中使用此資訊 [收集電子商務資料並將其導入平台](../collect/ecommerce.md)。
