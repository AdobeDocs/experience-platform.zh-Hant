---
keywords: Experience Platform；首頁；熱門主題；付款
solution: Experience Platform
title: 使用流程服務API來探索付款系統
description: 本教學課程使用流程服務API來探索付款應用程式。
exl-id: 7d0231de-46c0-49df-8a10-aeb42a2c8822
source-git-commit: 104db777446b19fa9e3ea7538ae1dda6f51a00b1
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 12%

---

# 使用[!DNL Flow Service] API探索付款系統

[!DNL Flow Service]用於收集及集中來自Adobe Experience Platform內各種不同來源的客戶資料。 此服務提供使用者介面和RESTful API，所有支援的來源都可從此API連線。

此教學課程使用[!DNL Flow Service] API來探索付款應用程式。

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

下列章節提供您需瞭解的其他資訊，才能使用[!DNL Flow Service] API成功連線至付款應用程式。

### 收集必要的認證

您必須與支付應用程式有使用中的連線，才能探索您來源的檔案和檔案結構。 如需詳細資訊，請閱讀下列檔案：

* [[!DNL Square]](../create/payments/square.md)
* [[!DNL Stripe]](../create/payments/stripe.md)

### 讀取範例 API 呼叫

本教學課程提供範例API呼叫，示範如何格式化您的請求。 這些包括路徑、必要的標頭和正確格式化的請求承載。 此外，也提供 API 回應中傳回的範例 JSON。 如需檔案中所使用範例API呼叫慣例的詳細資訊，請參閱[!DNL Experience Platform]疑難排解指南中[如何讀取範例API呼叫](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request)一節。

### 收集所需標頭的值

若要呼叫[!DNL Experience Platform] API，您必須先完成[驗證教學課程](https://www.adobe.com/go/platform-api-authentication-en)。 完成驗證教學課程會提供所有 [!DNL Experience Platform] API 呼叫中每個必要標頭的值，如下所示：

* 授權：持有人`{ACCESS_TOKEN}`
* x-api-key： `{API_KEY}`
* x-gw-ims-org-id： `{ORG_ID}`

[!DNL Experience Platform]中的所有資源（包括屬於[!DNL Flow Service]的資源）都與特定的虛擬沙箱隔離。 對[!DNL Experience Platform] API的所有請求都需要標頭，以指定將在其中執行作業的沙箱名稱：

* x-sandbox-name： `{SANDBOX_NAME}`

包含裝載(POST、PUT、PATCH)的所有請求都需要額外的媒體型別標頭：

* Content-Type： `application/json`

## 探索您的資料表

使用付款系統的連線ID，即可執行GET請求來探索資料表格。 使用以下呼叫來尋找您要檢查或擷取至[!DNL Experience Platform]的資料表的路徑。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 付款基礎連線的識別碼。 |

**要求**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/24151d58-ffa7-4960-951d-58ffa7396097/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會從您的付款系統傳回一連串表格。 尋找您要帶入[!DNL Experience Platform]的資料表並記下其`path`屬性，因為您必須在下個步驟中提供它以檢查其結構。

```json
[
    {
        "type": "table",
        "name": "Stripe.Billing_Plans",
        "path": "Stripe.Billing_Plans",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Stripe.Billing_Plans_Payment_Definition",
        "path": "Stripe.Billing_Plans_Payment_Definition",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Stripe.Billing_Plans_Payment_Definition_Charge_Models",
        "path": "Stripe.Billing_Plans_Payment_Definition_Charge_Models",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Stripe.Catalog_Products",
        "path": "Stripe.Catalog_Products",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## 檢查表格的結構

若要從您的付款系統檢查表格結構，請在指定表格路徑為查詢引數時執行GET要求。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{BASE_CONNECTION_ID}` | 您的付款系統的連線ID。 |
| `{TABLE_PATH}` | 付款系統內表格的路徑。 |

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/24151d58-ffa7-4960-951d-58ffa7396097/explore?objectType=table&object=test1.Mytable' \
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
                "name": "Product_Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Product_Name",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Description",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Type",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
        ]
    }
}
```

## 後續步驟

依照本教學課程，您已探索您的付款系統、找到您要擷取至[!DNL Experience Platform]的表格路徑，並取得有關其結構的資訊。 您可以在下個教學課程中使用此資訊，從您的付款系統[收集資料，並將其帶入Experience Platform](../collect/payments.md)。
