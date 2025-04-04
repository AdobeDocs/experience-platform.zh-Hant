---
keywords: Experience Platform；首頁；熱門主題；來源；API；探索；流程服務
title: 使用流量服務API探索表格Source
description: 本教學課程使用流程服務API來探索表格來源的內容和結構。
exl-id: 0c7a5b8a-2071-4ac2-b2d1-c5534e7c7d9c
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '471'
ht-degree: 5%

---

# 使用[!DNL Flow Service] API探索資料表

本教學課程提供如何使用[[!DNL Flow Service]](https://www.adobe.io/experience-platform-apis/references/flow-service/) API來探索及預覽資料表的結構與內容的步驟。

>[!NOTE]
>
> 為了探索您的資料表，您必須擁有表格式來源的有效基本連線ID。 如果您沒有此ID，請參閱下列教學課程，以瞭解如何為表格式來源建立基本連線ID的步驟： <ul><li>[Advertising](../../../home.md#advertising)</li><li>[CRM](../../../home.md#customer-relationship-management)</li><li>[客戶成功](../../../home.md#customer-success)</li><li>[資料庫](../../../home.md#database)</li><li>[電子商務](../../../home.md#ecommerce)</li><li>[行銷自動化](../../../home.md#marketing-automation)</li><li>[付款](../../../home.md#payments)</li><li>[通訊協定](../../../home.md#protocols)</li></ul>

## 快速入門

本指南需要您深入了解下列 Adobe Experience Platform 元件：

* [來源](../../../home.md)： [!DNL Experience Platform]允許從各種來源擷取資料，同時讓您能夠使用[!DNL Experience Platform]服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../sandboxes/home.md)： [!DNL Experience Platform]提供可將單一[!DNL Experience Platform]執行個體分割成個別虛擬環境的虛擬沙箱，以利開發及改進數位體驗應用程式。

### 使用Experience Platform API

如需如何成功呼叫Experience Platform API的詳細資訊，請參閱[Experience Platform API快速入門](../../../../landing/api-guide.md)指南。

## 探索您的資料表

您可以在提供來源的基本連線ID的同時，對[!DNL Flow Service] API發出GET要求，以擷取資料表結構的資訊。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 來源的基本連線ID。 |

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

成功的回應會從您的來源傳回資料表陣列。 尋找您要帶入Experience Platform的表格並記下其`path`屬性，因為您必須在下一個步驟中提供它以檢查其結構。

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

## 檢查表格的結構

若要檢查資料表的內容，請在將表格的路徑指定為查詢引數時，對[!DNL Flow Service] API執行GET要求。

**API格式**

```http
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| 參數 | 說明 |
| --- | --- |
| `{BASE_CONNECTION_ID}` | 來源的基本連線ID。 |
| `{TABLE_PATH}` | 您要檢查之資料表的路徑屬性。 |

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

成功的回應會傳回指定之資料表的內容和結構的相關資訊。 有關每個資料表資料行的詳細資料位於`columns`陣列的元素中。

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

依照本教學課程，您已收集有關資料表結構和內容的資訊。 此外，您已擷取要擷取至Experience Platform的表格路徑。 您可以使用此資訊建立來源連線和資料流，將您的資料匯入Experience Platform。 如需有關如何使用[!DNL Flow Service] API建立來源連線和資料流的特定步驟，請參閱下列教學課程：

* [Advertising來源](../collect/advertising.md)
* [CRM來源](../collect/crm.md)
* [客戶成功來源](../collect/customer-success.md)
* [資料庫來源](../collect/database-nosql.md)
* [電子商務來源](../collect/ecommerce.md)
* [行銷自動化來源](../collect/marketing-automation.md)
* [付款來源](../collect/payments.md)
* [通訊協定來源](../collect/protocols.md)
