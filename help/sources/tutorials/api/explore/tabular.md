---
keywords: Experience Platform；首頁；熱門主題；來源；API；探索；流程服務
title: 使用流量服務API探索表格來源
description: 本教學課程使用流量服務API來探索表格型來源的內容與結構。
exl-id: 0c7a5b8a-2071-4ac2-b2d1-c5534e7c7d9c
source-git-commit: 3bdeec8284873b8d9368f833b24e9922ed489019
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 2%

---

# 使用 [!DNL Flow Service] API

本教學課程提供如何探索和預覽資料表的結構和內容的步驟，使用 [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API。

>[!NOTE]
>
> 要瀏覽資料表，您必須已具有表格源的有效基本連接ID。 如果您沒有此ID，請參閱下列教學課程，了解如何為表格來源建立基本連線ID的步驟： <ul><li>[Advertising](../../../home.md#advertising)</li><li>[CRM](../../../home.md#customer-relationship-management)</li><li>[客戶成功](../../../home.md#customer-success)</li><li>[資料庫](../../../home.md#database)</li><li>[電子商務](../../../home.md#ecommerce)</li><li>[行銷自動化](../../../home.md#marketing-automation)</li><li>[付款](../../../home.md#payments)</li><li>[通訊協定](../../../home.md#protocols)</li></ul>

## 快速入門

本指南需要妥善了解下列Adobe Experience Platform元件：

* [來源](../../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../../landing/api-guide.md).

## 探索資料表

您可以向 [!DNL Flow Service] API，同時提供來源的基本連線ID。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 源的基本連接ID。 |

**要求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/5e73e5a2-dc36-45a8-9f16-93c7a43af318/explore?objectType=root' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應從源返回表陣列。 找出您要帶入Platform的表格，並注意其 `path` 屬性，因為您必須在下一個步驟中提供屬性，以檢查其結構。

```json
[
    {
        "type": "table",
        "name": "ACME Spring Campaign",
        "path": "acmeSpringCampaign",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "ACME Summer Campaign",
        "path": "acmeSummerCampaign",
        "canPreview": true,
        "canFetchSchema": true
    }
]
```

## Inspect表的結構

若要檢查資料表的內容，請向 [!DNL Flow Service] API，同時將表的路徑指定為查詢參數。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 源的基本連接ID。 |
| `{TABLE_PATH}` | 要檢查的表的路徑屬性。 |

**要求**

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/flowservice/connections/5e73e5a2-dc36-45a8-9f16-93c7a43af318/explore?objectType=table&object=acmeSpringCampaign' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回有關指定表的內容和結構的資訊。 有關表格各欄的詳細資訊位於 `columns` 陣列。

```json
{
  "format": "flat",
  "schema": {
    "columns": [
      {
        "name": "TestID",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Name",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Datefield",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "complaint_type",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "complaint_description",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "status",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "status_change_date",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      },
      {
        "name": "city",
        "type": "string",
        "xdm": {
          "type": "string"
        }
      },
      {
        "name": "Datefield2",
        "type": "string",
        "meta:xdmType": "date-time",
        "xdm": {
          "type": "string",
          "format": "date-time"
        }
      }
    ]
  }
}
```

## 後續步驟

依照本教學課程，您已收集資料表格的結構和內容的相關資訊。 此外，您已擷取要內嵌至Platform的表格路徑。 您可以使用此資訊建立源連接和資料流，將資料帶入Platform。 有關如何使用建立源連接和資料流的具體步驟，請參閱以下教程 [!DNL Flow Service] API:

* [廣告來源](../collect/advertising.md)
* [CRM來源](../collect/crm.md)
* [客戶成功來源](../collect/customer-success.md)
* [資料庫源](../collect/database-nosql.md)
* [電子商務來源](../collect/ecommerce.md)
* [行銷自動化來源](../collect/marketing-automation.md)
* [付款來源](../collect/payments.md)
* [協定源](../collect/protocols.md)
