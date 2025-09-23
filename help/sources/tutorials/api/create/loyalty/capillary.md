---
title: 使用流量服務API連線Capillity至Experience Platform
description: 瞭解如何使用API將Capillity連線至Experience Platform。
hide: true
hidefromtoc: true
source-git-commit: 7119ca51e0a4db09c8adb68bcde41ab3837439d1
workflow-type: tm+mt
source-wordcount: '1112'
ht-degree: 1%

---

# 使用[!DNL Capillary Streaming Events] API連線[!DNL Flow Service]至Experience Platform

閱讀本指南，瞭解如何使用[!DNL Capillary Streaming Events]和[[!DNL Flow Service] API](https://developer.adobe.com/experience-platform-apis/references/flow-service/)，將資料從您的[!DNL Capillary]帳戶串流至Adobe Experience Platform。

## 快速入門

本指南需要您深入瞭解下列Experience Platform元件：

* [來源](../../../../home.md)： Experience Platform允許從各種來源擷取資料，同時讓您能夠使用Experience Platform服務來建構、加標籤以及增強傳入的資料。
* [沙箱](../../../../../sandboxes/home.md)： Experience Platform提供的虛擬沙箱可將單一Experience Platform執行個體分割成個別的虛擬環境，以利開發及改進數位體驗應用程式。

### 收集必要的認證

閱讀[[!DNL Capillary Streaming Events] 總覽](../../../../connectors/loyalty/capillary.md)以取得驗證的相關資訊。

### 使用Experience Platform API

閱讀[Experience Platform API快速入門](../../../../../landing/api-guide.md)的指南，瞭解如何成功呼叫Experience Platform API。

>[!BEGINSHADEBOX]

## 開發人員流程檢查清單

1. 使用結構描述登入建立或選擇您的目標&#x200B;**體驗資料模型(XDM)結構描述**。 使用此XDM結構描述在目錄服務中&#x200B;**建立資料集**。
2. 建立&#x200B;**基底連線**&#x200B;以儲存您的[!DNL Capillary]認證。
3. 建立&#x200B;**來源連線**&#x200B;以繫結至您的`baseConnectionId`。
4. 建立&#x200B;**目標連線**&#x200B;以確保您的資料登陸到資料湖。
5. 使用「資料準備」建立對應，將您的[!DNL Capillary]來源欄位對應到正確的XDM欄位。
6. 使用您的`sourceConnectionId`、`targetConnectionId`和`mappingID`建立資料流
7. 使用單一範例設定檔/交易事件進行eTest以驗證您的資料流。

>[!ENDSHADEBOX]

## 建立基礎連線 {#base-connection}

基礎連線會保留認證和連線詳細資料。 若要為[!DNL Capillary]建立基底連線，請對`/connections` API的[!DNL Flow Service]端點提出POST要求，並在要求內文中提供您的[!DNL Capillary]認證。

**API格式**

```https
POST /connections
```

**要求**

下列要求會建立[!DNL Capillary]的基礎連線：

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Capillary base connection",
    "description": "Base connection to authenticate the [!DNL Capillary] source.",
    "connectionSpec": {
      "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
      "version": "1.0"
    },
    "auth": {
      "specName": "OAuth generic-rest-connector",
      "params": {
        "clientId": "{CLIENT_ID}",
        "clientSecret": "{CLIENT_SECRET}",
        "accessToken": "{ACCESS_TOKEN}"
      }
    }
  }'
```

**回應**

```
A successful response returns the newly created base connection, including its unique connection identifier (id). This ID is required to explore your source's file structure and contents in the next step.

{
     "id": "70383d02-2777-4be7-a309-9dd6eea1b46d",
     "etag": "\"d64c8298-add4-4667-9a49-28195b2e2a84\""
}
```

### 建立來源連線

若要建立來源連線，請在提供您的基本連線ID時，對`/sourceConnections`端點提出POST要求。

**API格式**

```http
POST /flowservice/sourceConnections
```

**要求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/sourceConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
      "name": "Capillary Streaming",
      "description": "Capillary Streaming",
      "baseConnectionId": "70383d02-2777-4be7-a309-9dd6eea1b46d",
      "connectionSpec": {
          "id": "6360f136-5980-4111-8bdf-15d29eab3b5a",
          "version": "1.0"
      }
    }'
```

**回應**

成功的回應會傳回HTTP狀態201，其中包含新建立的來源連線的詳細資料，包括其唯一識別碼(`id`)。

```json
{
  "id": "34ece231-294d-416c-ad2a-5a5dfb2bc69f",
  "etag": "\"d505125b-0000-0200-0000-637eb7790000\""
}
```

### 結構描述設定

>[!BEGINTABS]

>[!TAB 設定檔擷取]

設定檔包含身分和忠誠度屬性。 檢視下列裝載以根據[!DNL Capillary]設定檔結構描述的範例。 您可以設定此結構並對應至XDM個別設定檔。

**要求**

```json
{
  "identityMap": {
    "email": [
      {
        "authenticatedState": "ambiguous",
        "id": "john.doe@capillarytech.com",
        "primary": true
      }
    ]
  },
  "loyalty": {
    "tier": "gold",
    "points": 1250,
    "lifetimePoints": 122,
    "expiredPoints": 12,
    "pointsRedeemed": 500,
    "program": "loyalty program name",
    "status": "active"
  }
}
```

**回應**

```json
{
  "id": "8c19f1c3-4b91-47cd-8cb5-b152a93f7349",
  "status": "success",
  "message": "Profile record ingested successfully"
}
```

>[!TAB 交易擷取]

交易會擷取商務活動。 檢視下列裝載以取得以[!DNL Capillary]事件結構描述為基礎的範例。 您可以設定此結構並對應至XDM體驗事件。

**要求**

```json
{
  "_id": "T0001",
  "timestamp": "2025-07-14T12:00:00-06:00",
  "identityMap": {
    "email": [
      {
        "authenticatedState": "ambiguous",
        "id": "john@capillarytech.com",
        "primary": true
      }
    ]
  },
  "commerce": {
    "commerceScope": {
      "storeCode": "HSR"
    },
    "order": {
      "priceTotal": 90
    }
  },
  "productLineItems": [
    {
      "SKU": "sku_01",
      "quantity": 1,
      "priceTotal": 100,
      "name": "Kitkat",
      "discountAmount": 10
    }
  ]
}
```

**回應**

```json
{
  "id": "T0001",
  "status": "success",
  "message": "Transaction event ingested successfully"
}
```

>[!ENDTABS]

### 支援的事件

[!DNL Capillary]來源支援下列事件：

* `pointsIssued`
* `tierDowngraded`
* `tierUpgraded`
* `pointsExpiryChange`
* `pointsExpired`
* `transactionUpdated`
* `customerAdded`
* `tierDowngradeReminder`
* `promotionEarned`
* `pointsExpiryReminder`
* `pointsRedeemed`
* `transactionAdded`
* `tierRenewed`
* `customerUpdated`


### 歷史資料移轉

您可以將歷史忠誠度和交易資料帶入Experience Platform。 只要從[!DNL Capillary]將您的資料匯出為結構化CSV檔案、使用[!DNL SFTP]安全地傳輸這些檔案，並將它們擷取到您的Experience Platform資料集中。 初始移轉後，您的資料將透過事件導向聯結器即時保持最新。

### 建立目標XDM結構描述 {#target-schema}

Experience Data Model (XDM)結構描述提供一種標準化方式，可在Experience Platform中組織和描述客戶體驗資料。 若要將來源資料內嵌至Experience Platform，您必須先建立目標XDM結構描述，定義您要內嵌的資料結構和型別。 此結構描述可作為您擷取之資料將存放的Experience Platform資料集的藍圖。

可透過對[結構描述登入API](https://developer.adobe.com/experience-platform-apis/references/schema-registry/)執行POST要求來建立目標XDM結構描述。 如需如何建立目標XDM架構的詳細步驟，請閱讀以下指南：

* [使用API建立結構描述](../../../../../xdm/api/schemas.md)。
* [使用UI建立結構描述](../../../../../xdm/tutorials/create-schema-ui.md)。

建立後，稍後將需要目標XDM結構描述`$id`以用於您的目標資料集和對應。

## 建立目標資料集 {#target-dataset}

資料集是資料集合的儲存和管理結構，通常會像有欄（結構描述）和列（欄位）的表格一樣結構。 成功擷取至Experience Platform的資料會以資料集的形式儲存在資料湖中。 在此步驟中，您可以建立新資料集或使用現有資料集。

您可以對[目錄服務API](https://developer.adobe.com/experience-platform-apis/references/catalog/)發出POST要求，同時在承載中提供目標結構描述的ID，藉此建立目標資料集。 如需如何建立目標資料集的詳細步驟，請參閱[使用API建立資料集](../../../../../catalog/api/create-dataset.md)的指南。


## 建立目標連線 {#target}

目標連線代表與擷取資料著陸目的地之間的連線。 若要建立目標連線，您必須提供與Data Lake關聯的固定連線規格ID。 此連線規格識別碼為： `c604ff05-7f1a-43c0-8e18-33bf874cb11c`。

**API格式**

```http
POST /targetConnections
```

**要求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/targetConnections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Capillary Target Connection",
      "description": "Capillary Target Connection",
      "data": {
          "schema": {
              "id": "https://ns.adobe.com/{TENANT_ID}/schemas/52b59140414aa6a370ef5e21155fd7a686744b8739ecc168",
              "version": "application/vnd.adobe.xed-full+json;version=1"
          }
      },
      "params": {
          "dataSetId": "6889f4f89b982b2b90bc1207"
      },
      "connectionSpec": {
          "id": "c604ff05-7f1a-43c0-8e18-33bf874cb11c",
          "version": "1.0"
      }
    }'
```

### 建立對應 {#mapping}

接著，將來源資料對應至目標資料集所固定的目標結構描述。 若要建立對應，請對`mappingSets`API[[!DNL Data Prep] 的](https://developer.adobe.com/experience-platform-apis/references/data-prep/)端點提出POST要求。 包含您的目標XDM結構描述ID和您要建立之對應集的詳細資訊。

將「毛細管」欄位對應至對應的XDM結構描述欄位，如下所示：

| 來源結構描述 | 目標結構描述 |
|------------------------------|-------------------------------|
| `identityMap.email.id` | `xdm:identityMap.email` |
| `loyalty.points` | `xdm:loyaltyPoints` |
| `loyalty.tier` | `xdm:loyaltyTier` |
| `commerce.order.priceTotal` | `xdm:commerce.order.priceTotal` |
| `productLineItems.SKU` | `xdm:productListItems.SKU` |

### 建立資料流 {#flow}

建立來源連線、對應及目標連線後，您可以設定資料流，將資料從[!DNL Capillary]移至Experience Platform。

典型的資料流包括：

* **設定檔資料流**：將[!DNL Capillary]設定檔資料擷取至XDM個別設定檔資料集。
* **交易資料流**：將[!DNL Capillary]交易資料擷取至XDM ExperienceEvent資料集。

**要求**

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "Capillary dataflow",
    "description": "Capillary → Experience Platform dataflow",
    "flowSpec": {
      "id": "6499120c-0b15-42dc-936e-847ea3c24d72",
      "version": "1.0"
    },
    "sourceConnectionIds": "{SOURCE_CONNECTION_ID}",
    "targetConnectionIds": "{TARGET_CONNECTION_ID}",
    "transformations": [
      {
        "name": "Mapping",
        "params": {
          "mappingId": "{MAPPING_ID}",
          "mappingVersion": "0"
        }
      }
    ],
    "scheduleParams": {
      "startTime": "1625040887",
      "frequency": "minute",
      "interval": 15
    }
  }'
```

>[!NOTE]
>
>`startTime`處於UNIX紀元秒內。

**回應**

成功的回應會傳回您的資料流及其對應的資料流ID。

```json
{
  "id": "92f11b8c-0a9f-45a9-8239-60b4e8430a88",
  "status": "enabled",
  "message": "Dataflow created successfully"
}
```

## 錯誤處理

聯結器包含下列情況的健全錯誤處理：

* **驗證錯誤**：驗證失敗時自動重新整理Adobe認證。
* **速率限制錯誤**：在達到API速率限制時，實作具有指數回溯的重試。
* **網路錯誤**：記錄並重試失敗的網路要求。
* **資料驗證錯誤**：記錄無效的裝載，以進行手動檢閱和解決。

所有錯誤都隨錯誤型別、時間戳記、請求裝載和Adobe API回應等詳細資訊一起記錄，以促進疑難排解和偵錯。

## 測試您的連線

請依照下列步驟，瞭解測試連線時可採取的步驟：

* 向`/connections/{BASE_CONNECTION_ID}`發出GET請求並提供您的基本連線ID，以驗證您的基本連線是否存在。 在此步驟中，您也可以確認基礎連線的狀態已設為`active`。
* 向`/flowservice/sourceConnections/{SOURCE_CONNECTION_ID}`發出GET請求並提供您的來源連線ID以驗證您的來源連線。
* 使用您的串流端點URL來傳送範例設定檔裝載（使用設定檔擷取JSON）。
* 導覽至您在Experience Platform UI中的資料集，並對資料集執行查詢以確認您的記錄。
* 使用「資料準備」記錄檔來檢查錯誤。
* 如果您必須開啟支援票證，請確保您具備下列條件：
   * 請求承載
   * 回應內文
   * Request-id
   * 時間戳記
   * 資源ID

## 附錄

如需其他作業指南，請瀏覽下列檔案

* [監視資料流](../../../../../dataflows/ui/monitor-sources.md)
* [更新資料流](../../../ui/update-dataflows.md)
* [刪除資料流](../../../ui/delete.md)
* [更新來源帳戶](../../../ui/update.md)
