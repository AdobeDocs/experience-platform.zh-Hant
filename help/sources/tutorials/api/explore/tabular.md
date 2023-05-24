---
keywords: Experience Platform；首頁；熱門主題；源；API;explore;flow服務
title: 使用流服務API瀏覽表格源
description: 本教程使用流服務API來瀏覽基於表的源的內容和結構。
exl-id: 0c7a5b8a-2071-4ac2-b2d1-c5534e7c7d9c
source-git-commit: 3bdeec8284873b8d9368f833b24e9922ed489019
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 2%

---

# 使用 [!DNL Flow Service] API

本教程提供了有關如何使用 [[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API。

>[!NOTE]
>
> 為了瀏覽資料表，您必須已具有表格源的有效基連接ID。 如果沒有此ID，請參閱以下教程，瞭解如何為表格源建立基本連接ID的步驟： <ul><li>[Advertising](../../../home.md#advertising)</li><li>[CRM](../../../home.md#customer-relationship-management)</li><li>[客戶成功](../../../home.md#customer-success)</li><li>[資料庫](../../../home.md#database)</li><li>[電子商務](../../../home.md#ecommerce)</li><li>[營銷自動化](../../../home.md#marketing-automation)</li><li>[付款](../../../home.md#payments)</li><li>[協定](../../../home.md#protocols)</li></ul>

## 快速入門

本指南要求對Adobe Experience Platform的下列組成部分有工作上的理解：

* [源](../../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../../landing/api-guide.md)。

## 瀏覽資料表

可通過向Web站點發出GET請求來檢索有關資料表結構的資訊 [!DNL Flow Service] API，同時提供源的基本連接ID。

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

成功的響應從源返回表陣列。 查找要帶入平台的表並注意其 `path` 屬性，因為在下一步中需要提供該屬性來檢查其結構。

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

## Inspect桌子的結構

要檢查資料表的內容，請向 [!DNL Flow Service] 將表路徑指定為查詢參數時的API。

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

成功的響應返回有關指定表的內容和結構的資訊。 有關每個表列的詳細資訊位於 `columns` 陣列。

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

按照本教程，您已收集了有關資料表結構和內容的資訊。 此外，您已檢索到要輸入到「平台」中的表的路徑。 您可以使用此資訊建立源連接和資料流，以將資料帶到平台。 有關如何使用建立源連接和資料流的具體步驟，請參見以下教程 [!DNL Flow Service] API:

* [廣告來源](../collect/advertising.md)
* [CRM源](../collect/crm.md)
* [客戶成功來源](../collect/customer-success.md)
* [資料庫源](../collect/database-nosql.md)
* [電子商務來源](../collect/ecommerce.md)
* [營銷自動化來源](../collect/marketing-automation.md)
* [付款來源](../collect/payments.md)
* [協定源](../collect/protocols.md)
