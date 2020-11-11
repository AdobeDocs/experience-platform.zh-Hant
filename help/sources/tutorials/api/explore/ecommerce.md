---
keywords: Experience Platform;home;popular topics;ecommerce;eCommerce
solution: Experience Platform
title: 使用Flow Service API探索電子商務連線
topic: overview
description: 本教學課程使用Flow Service API來探索電子商務連線。
translation-type: tm+mt
source-git-commit: 4696bcb17427bb50549a315294baf7fbd87ac01d
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 2%

---


# 使用 [!DNL Flow Service] API探索電子商務連線

[!DNL Flow Service] 用於收集和集中Adobe Experience Platform內不同來源的客戶資料。 該服務提供用戶介面和REST風格的API，所有支援的源都可從中連接。

本教學課程使 [!DNL Flow Service] 用API來探索協力廠商的 **[!UICONTROL 電子商務]** 。

## 快速入門

本指南需要有效瞭解Adobe Experience Platform的下列元件：

* [[!DNL Sources]](../../../home.md): [!DNL Experience Platform] 允許從各種來源接收資料，同時提供使用服務構建、標籤和增強傳入資料的 [!DNL Platform] 能力。
* [[!DNL Sandboxes]](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

以下各節提供您必須知道的其他資訊，以便使用 **[!UICONTROL API成功連線至]** 電子商務 [!DNL Flow Service] 連線。

### 取得連線ID

若要使用API探索 **[!UICONTROL 您的電子商務連]** 線 [!DNL Platform] ，您必須擁有有效的連線ID。 如果您尚未建立您要使用的 **[!UICONTROL 電子商務連線]** ，您可以透過下列教學課程來建立連線：

* [Shopify](../create/ecommerce/shopify.md)

### 讀取範例API呼叫

本教學課程提供範例API呼叫，以示範如何設定請求的格式。 這些包括路徑、必要標題和正確格式化的請求負載。 也提供API回應中傳回的範例JSON。 如需範例API呼叫檔案中所用慣例的詳細資訊，請參閱疑難排解指 [南中有關如何讀取範例API呼叫的](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)[!DNL Experience Platform] 章節。

### 收集必要標題的值

若要呼叫API，您必 [!DNL Platform] 須先完成驗證教 [學課程](../../../../tutorials/authentication.md)。 完成驗證教學課程後，將提供所有 [!DNL Experience Platform] API呼叫中每個必要標題的值，如下所示：

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

中的所有資 [!DNL Experience Platform]源(包括屬於這些資源 [!DNL Flow Service])都隔離到特定的虛擬沙盒。 對API的所 [!DNL Platform] 有請求都需要一個標題，該標題會指定要在中執行的操作的沙盒名稱：

* `x-sandbox-name: {SANDBOX_NAME}`

所有包含裝載(POST、PUT、PATCH)的請求都需要額外的媒體類型標題：

* `Content-Type: application/json`

## 探索您的資料表格

使用 **[!UICONTROL eCommerce]** connection ID，您可以執行GET請求來探索資料表格。 使用以下調用查找要檢查或裝入的表的路徑 [!DNL Platform]。

**API格式**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=root
```

| 參數 | 說明 |
| --- | --- |
| `{CONNECTION_ID}` | 您的 **[!UICONTROL 電子商務]** 連線ID。 |

**請求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會從您的電子商務連線傳回 **[!UICONTROL 一組表]** 。 尋找您要放入的表格， [!DNL Platform] 並記下其屬性，因 `path` 為您必須在下個步驟中提供表格以檢查其結構。

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

## 檢查表格結構

要從 **[!UICONTROL eCommerce連接檢查表的結構]** ，請在指定查詢參數內表的路徑時執行GET `object` 請求。

**API格式**

```http
GET /connections/{CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{CONNECTION_ID}` | 您電子商務連線的 **[!UICONTROL 連線ID]** 。 |
| `{TABLE_PATH}` | 電子商務連線中表 **[!UICONTROL 的路徑]** 。 |

**請求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/582f4f8d-71e9-4a5c-a164-9d2056318d6c/explore?objectType=table&object=Orders' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回指定表的結構。 有關每個表列的詳細資訊位於陣列的元 `columns` 素中。

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

在本教程中，您已探索過 **[!UICONTROL eCommerce]** 連線、找到您要收錄的表格路徑 [!DNL Platform]，並取得其結構的相關資訊。 您可以在下一個教學課程中使用此資 [訊來收集電子商務資料並將其匯入平台](../collect/ecommerce.md)。
