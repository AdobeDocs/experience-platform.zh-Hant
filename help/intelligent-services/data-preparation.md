---
keywords: Experience Platform;home;intelligent services;popular topics
solution: Experience Platform
title: 準備資料以用於智慧型服務
topic: Intelligent Services
translation-type: tm+mt
source-git-commit: 9a2e6f7db441b804f17ec91d06d359439c3d5da5
workflow-type: tm+mt
source-wordcount: '1595'
ht-degree: 0%

---


# 準備資料以用於智慧型服務

為了讓智慧型服務能夠從行銷事件資料中發掘見解，資料必須以標準結構進行語義豐富和維護。 智慧型服務運用Experience Data Model(XDM)架構來達成此目標。 具體而言，Intelligent Services中使用的所有資料集都必須符合 **Consumer ExperienceEvent(CEE)** XDM架構。

本檔案提供將行銷事件資料從多個管道對應至此架構的一般指引，概述有關架構中重要欄位的資訊，以協助您判斷如何有效地將資料對應至其架構。

## 工作流程摘要

準備程式會視您的資料儲存在Adobe Experience Platform或外部而定。 本節概述了在兩種情況下需要採取的必要步驟。

### 外部資料準備

如果您的資料儲存在外部， [!DNL Experience Platform]請遵循下列步驟：

1. 請連絡Adobe諮詢服務以要求專屬Azure Blob儲存容器的存取憑證。
1. 使用您的存取憑證，將資料上傳至Blob容器。
1. 與Adobe諮詢服務合作，將您的資料對應至 [Consumer ExperienceEvent架構](#cee-schema) ，並將其內嵌至智慧服務。

### [!DNL Experience Platform] 資料準備

如果您的資料已儲存在中 [!DNL Platform]，請遵循下列步驟：

1. 檢閱Consumer ExperienceEvent架構的 [結構](#cee-schema) ，並判斷您的資料是否可對應至其欄位。
1. 請連絡Adobe諮詢服務，協助您將資料對應至架構並將其內嵌至智慧型服務，或如 [果您要自行對應資料](#mapping) ，請依照本指南的步驟進行。

## 瞭解CEE架構 {#cee-schema}

消費者體驗事件結構描述個人的行為，因為它與數位行銷事件（網路或行動裝置）以及線上或離線商務活動有關。 智慧服務需要使用此模式，因為其語義上定義良好的欄位（列），以避免任何未知名稱，否則會使資料不那麼清晰。

智慧型服務會利用此架構中的幾個關鍵欄位，從您的行銷事件資料產生深入資訊，所有這些資料都可在根層級找到並展開，以顯示其必要的子欄位。

![](./images/data-preparation/schema-expansion.gif)

與所有XDM模式一樣，CEE混合模式具有可擴充性。 換言之，CEE混音中可新增其他欄位，若有需要，可在多個結構中加入不同的變數。

在公用 [XDM儲存庫中可找到混合的完整示例](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)，並應用作以下部分中概述的關鍵欄位的參考。

## 關鍵字欄位

以下各節將重點介紹CEE混合內的關鍵欄位，這些欄位應用於智慧服務以生成有用的見解，包括說明和參考文檔的連結，以獲得更多示例。

>[!IMPORTANT] Attribution `xdm:channel` AI必須填寫欄位（如下面第一節所述） **** ，才能與您的資料搭配使用，而客戶AI則沒有任何必填欄位。 強烈建議使用所有其他關鍵字欄位，但非必填欄位。

### xdm:channel

此欄位代表與ExperienceEvent相關的行銷渠道。 欄位包含頻道類型、媒體類型和位置類型的相關資訊。 **必須提&#x200B;_供此欄_,Attribution AI才能處理您的資料**。

![](./images/data-preparation/channel.png)

**範例架構**

```json
{
  "@id": "https://ns.adobe.com/xdm/channels/facebook-feed",
  "@type": "https://ns.adobe.com/xdm/channel-types/social",
  "xdm:mediaType": "earned",
  "xdm:mediaAction": "clicks"
}
```

如需每個必要子欄位的完整資訊，請 `xdm:channel`參閱體驗 [管道架構規範](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) 。 有關某些映射示例，請參見 [下表](#example-channels)。

#### 頻道映射範例 {#example-channels}

下表提供映射至架構的行銷渠道的一些范 `xdm:channel` 例：

| Player Name | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| 付費搜尋 | https:/<span>/ns.adobe.com/xdm/channel-types/search | 付款 | 點擊 |
| 社交——行銷 | https:/<span>/ns.adobe.com/xdm/channel-types/social | 掙 | 點擊 |
| 顯示 | https:/<span>/ns.adobe.com/xdm/channel-types/display | 付款 | 點擊 |
| 電子郵件 | https:/<span>/ns.adobe.com/xdm/channel-types/email | 付款 | 點擊 |
| 內部反向連結 | https:/<span>/ns.adobe.com/xdm/channel-types/direct | 擁有 | 點擊 |
| 顯示檢視 | https:/<span>/ns.adobe.com/xdm/channel-types/display | 付款 | 印象 |
| QR Code重新導向 | https:/<span>/ns.adobe.com/xdm/channel-types/direct | 擁有 | 點擊 |
| 行動 | https:/<span>/ns.adobe.com/xdm/channel-types/mobile | 擁有 | 點擊 |

### xdm:productListItems

此欄位是代表客戶選擇之產品的一系列項目，包括產品SKU、名稱、價格和數量。

![](./images/data-preparation/productListItems.png)

**範例架構**

```json
[
  {
    "xdm:SKU": "1002352692",
    "xdm:name": "24-Watt 8-Light Chrome Integrated LED Bath Light",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 159.45
  },
  {
    "xdm:SKU": "3398033623",
    "xdm:name": "16ft RGB LED Strips",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 79.99
  }
]
```

有關每個必填子欄位的完整資訊，請 `xdm:productListItems`參閱商務詳細信 [息架構規範](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) 。

### xdm：商務

此欄位包含ExperienceEvent的商務相關資訊，包括採購訂單編號和付款資訊。

![](./images/data-preparation/commerce.png)

**範例架構**

```json
{
    "xdm:order": {
      "xdm:purchaseID": "a8g784hjq1mnp3",
      "xdm:purchaseOrderNumber": "123456",
      "xdm:payments": [
        {
          "xdm:transactionID": "transactid-a111",
          "xdm:paymentAmount": 59,
          "xdm:paymentType": "credit_card",
          "xdm:currencyCode": "USD"
        },
        {
          "xdm:transactionId": "transactid-a222",
          "xdm:paymentAmount": 100,
          "xdm:paymentType": "gift_card",
          "xdm:currencyCode": "USD"
        }
      ],
      "xdm:currencyCode": "USD",
      "xdm:priceTotal": 159
    },
    "xdm:purchases": {
      "xdm:value": 1
    }
  }
```

有關每個必填子欄位的完整資訊，請 `xdm:commerce`參閱商務詳細信 [息架構規範](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) 。

### xdm:web

此欄位代表與ExperienceEvent相關的網頁詳細資料，例如互動、頁面詳細資料和反向連結。

![](./images/data-preparation/web.png)

**範例架構**

```json
{
  "xdm:webPageDetails": {
    "xdm:siteSection": "Shopping Cart",
    "xdm:server": "example.com",
    "xdm:name": "Purchase Confirmation",
    "xdm:URL": "https://www.example.com/orderConf",
    "xdm:errorPage": false,
    "xdm:homePage": false,
    "xdm:pageViews": {
      "xdm:value": 1
    }
  },
  "xdm:webReferrer": {
    "xdm:URL": "https://www.example.com/checkout",
    "xdm:referrerType": "internal"
  }
}
```

如需每個必要子欄位的完整資訊，請 `xdm:productListItems`參閱 [ExperienceEvent Web詳細資訊結構規格](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) 。

### xdm：行銷

此欄位包含與觸點作用中之行銷活動相關的資訊。

![](./images/data-preparation/marketing.png)

**範例架構**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

有關每個必填子欄位的完整資訊，請 `xdm:productListItems`參閱行銷 [說明](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md) 。

## 對應和收錄資料(#mapping)

一旦您確定行銷事件資料是否可映射至CEE架構，下一步就是決定要將哪些資料匯入智慧型服務。 智慧型服務中使用的所有歷史資料都必須落在資料四個月的最短時間範圍內，加上預期做為回顧期間的天數。

在決定您要傳送的資料範圍後，請聯絡Adobe諮詢服務，協助將資料對應至架構，並將其內嵌至服務。

如果您有訂閱， [!DNL Adobe Experience Platform] 而且想要親自對應及收錄資料，請依照下節所述的步驟進行。

### 使用Adobe Experience Platform

>[!NOTE] 下列步驟需要訂閱Experience Platform。 如果您沒有平台存取權，請跳至下 [一步](#next-steps) 。

本節概述將資料對應並收錄至Experience Platform以用於智慧型服務的工作流程，包括教學課程的連結以取得詳細步驟。

#### 建立CEE架構和資料集

當您準備開始準備擷取資料時，第一個步驟是建立採用CEE mixin的新XDM架構。 下列教學課程將逐步說明在UI或API中建立新架構的程式：

* [在UI中建立結構](../xdm/tutorials/create-schema-ui.md)
* [在API中建立結構](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT] 上述教學課程會遵循建立架構的一般工作流程。 為架構選擇類時，必須使用 **XDM ExperienceEvent類**。 選擇此類後，可以將CEE混合添加到模式。

將CEE混音新增至架構後，您就可以視資料中其他欄位的需要新增其他混音。

建立並儲存架構後，您就可以根據該架構建立新的資料集。 下列教學課程將逐步說明在UI或API中建立新資料集的程式：

* [在UI中建立資料集](../catalog/datasets/user-guide.md#create) （依照工作流程使用現有架構）
* [在API中建立資料集](../catalog/datasets/create.md)

#### 新增主要身分命名空間標籤至資料集

如果您要從、或其他外 [!DNL Adobe Audience Manager]部來源 [!DNL Adobe Analytics]匯入資料，則必須新增標 `primaryIdentityNameSpace` 記至資料集。 這可以通過向目錄服務API發出PATCH請求來完成。

如果您從本機CSV檔案擷取資料，可跳至下一節的對應與 [擷取資料](#ingest)。

在遵循下列範例API呼叫之前，請參閱目錄開 [發人員指南中的](../catalog/api/getting-started.md) 「快速入門」一節，以取得有關必要標題的重要資訊。

**API格式**

```http
PATCH /dataSets/{DATASET_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{DATASET_ID}` | 您先前建立之資料集的ID。 |

**請求**

您必須在請求裝載中提供適當的值和標 `primaryIdentityNamespace` 記值， `sourceConnectorId` 視您要從哪個來源擷取資料。

下列請求會為Audience Manager新增適當的標籤值：

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "tags": {
          "primaryIdentityNameSpace": ["mcid"],
          "sourceConnectorId": ["audiencemanager"],
        }
      }'
```

下列請求會為Analytics新增適當的標籤值：

```shell
curl -X PATCH \
  https://platform.adobe.io/data/foundation/catalog/dataSets/5ba9452f7de80400007fc52a \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
        "tags": {
          "primaryIdentityNameSpace": ["aaid"],
          "sourceConnectorId": ["analytics"],
        }
      }'
```

>[!NOTE] 如需在Platform中使用身分名稱空間的詳細資訊，請參閱身分名稱 [空間概觀](../identity-service/namespaces.md)。

**回應**

成功的回應會傳回包含已更新資料集ID的陣列。 此ID應與PATCH請求中發送的ID匹配。

```json
[
    "@/dataSets/5ba9452f7de80400007fc52a"
]
```

#### 映射和收錄資料 {#ingest}

建立CEE架構和資料集後，您可以開始將資料表對應至架構，並將該資料內嵌至平台。 請參閱將CSV檔 [案對應至XDM架構的教學課程](../ingestion/tutorials/map-a-csv-file.md) ，以取得如何在UI中執行此動作的步驟。 在填入資料集後，可使用相同的資料集來擷取其他資料檔案。

如果您的資料儲存在支援的協力廠商應用程式中，您也可以選擇建立來源連 [接器](../sources/home.md) ，即時將行銷事件資料收錄到平台。

## 下一步 {#next-steps}

本檔案提供有關準備資料以用於智慧型服務的一般指引。 如果您需要根據使用案例提供其他諮詢服務，請聯絡Adobe諮詢支援。

在您成功將客戶體驗資料填入資料集後，您就可以使用智慧服務產生見解。 請參閱下列檔案以開始使用：

* [Attribution AI概觀](./attribution-ai/overview.md)
* [客戶人工智慧概觀](./customer-ai/overview.md)
