---
keywords: Experience Platform；家庭；智慧服務；熱門主題；智慧服務；智慧服務
solution: Experience Platform, Intelligent Services
title: 準備資料以用於智慧型服務
topic: Intelligent Services
description: 為了讓智慧型服務能夠從行銷事件資料中發掘見解，資料必須以標準結構進行語義豐富和維護。 智慧型服務運用Experience Data Model(XDM)架構來達成此目標。 具體來說，Intelligent Services中使用的所有資料集都必須符合Consumer ExperienceEvent(CEE)XDM架構。
exl-id: 17bd7cc0-da86-4600-8290-cd07bdd5d262
translation-type: tm+mt
source-git-commit: b311a5970a121a3277bdb72f5a1285216444b339
workflow-type: tm+mt
source-wordcount: '2020'
ht-degree: 1%

---

# 準備要用於[!DNL Intelligent Services]的資料

為了[!DNL Intelligent Services]從行銷事件資料中發掘見解，資料必須在標準結構中加以語義豐富和維護。 [!DNL Intelligent Services] 利 [!DNL Experience Data Model] 用(XDM)模式來實現此目的。具體而言，[!DNL Intelligent Services]中使用的所有資料集都必須符合Consumer ExperienceEvent(CEE)XDM架構。

本檔案提供將行銷事件資料從多個管道對應至此架構的一般指引，概述有關架構中重要欄位的資訊，以協助您判斷如何有效地將資料對應至其架構。

## 工作流程摘要

準備程式視您的資料儲存在Adobe Experience Platform或外部而定。 本節概述了在兩種情況下需要採取的必要步驟。

### 外部資料準備

如果您的資料儲存在[!DNL Experience Platform]以外，請遵循下列步驟：

1. 請聯絡Adobe諮詢服務以要求專屬Azure Blob儲存容器的存取憑證。
1. 使用您的存取憑證，將資料上傳至Blob容器。
1. 使用Adobe咨詢服務獲取映射至[消費者體驗事件模式](#cee-schema)的資料，並收錄至[!DNL Intelligent Services]。

### [!DNL Experience Platform] 資料準備

如果您的資料已儲存在[!DNL Platform]中，請遵循下列步驟：

1. 檢閱[Consumer ExperienceEvent架構](#cee-schema)的結構，並判斷您的資料是否可對應至其欄位。
1. 請聯絡Adobe諮詢服務，協助您將資料對應至架構，並將其內嵌至[!DNL Intelligent Services]，或[，如果您要自行對應資料，請依照本指南中的步驟進行。](#mapping)

## 瞭解CEE方案{#cee-schema}

消費者體驗事件結構描述個人的行為，因為它與數位行銷事件（網路或行動裝置）以及線上或離線商務活動有關。 由於[!DNL Intelligent Services]在語義上定義良好的欄位（欄），因此必須使用此架構，以避免任何未知名稱，否則會降低資料的清晰度。

CEE架構與所有XDM ExperienceEvent架構一樣，會在發生事件（或事件集）時擷取系統的時間序列狀態，包括時間點和相關主體的身分。 「體驗事件」是所發生事件的事實記錄，因此它們是不可變的，代表所發生的事件，而無需匯總或解讀。

[!DNL Intelligent Services] 利用此架構中的幾個關鍵欄位，從行銷事件資料產生深入資訊，所有這些資料都可在根層級找到並展開，以顯示其必要的子欄位。

![](./images/data-preparation/schema-expansion.gif)

與所有XDM模式一樣，CEE混合模式具有可擴充性。 換言之，CEE混音中可新增其他欄位，若有需要，可在多個結構中加入不同的變數。

在[public XDM repository](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)中可找到混音的完整示例。 此外，您還可以檢視並複製下列[JSON檔案](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json)，以取得如何結構化資料以符合CEE架構的範例。 在瞭解以下章節中概述的關鍵欄位時，請參閱這兩個範例，以決定如何將您自己的資料對應至架構。

## 關鍵字欄位

在CEE混音中，應使用幾個關鍵欄位，以便[!DNL Intelligent Services]產生有用的見解。 本節說明這些欄位的使用案例和預期資料，並提供參考檔案的連結，以取得更多範例。

### 必填欄位

強烈建議使用所有鍵欄位，但有兩個欄位是&#x200B;**required**，以便[!DNL Intelligent Services]工作：

* [主要身份欄位](#identity)
* [xdm:timestamp](#timestamp)
* [xdm:channel](#channel) (僅對Attribution AI必需)

#### 主要身份{#identity}

架構中的其中一個欄位必須設為主要識別欄位，這可讓[!DNL Intelligent Services]將每個時間系列資料例項連結至個別人員。

您必鬚根據資料的來源和性質，決定最佳欄位作為主要身分識別。 身分欄位必須包含&#x200B;**identity namespace**，指出欄位預期的身分資料類型為值。 某些有效的命名空間值包括：

* &quot;電子郵件&quot;
* &quot;phone&quot;
* &quot;mcid&quot;(針對Adobe Audience ManagerID)
* &quot;aid&quot;(針對Adobe AnalyticsID)

如果您不確定您應使用哪個欄位做為主要身分識別，請連絡Adobe諮詢服務以決定最佳解決方案。 如果未設定主標識，Intelligent Service應用程式將使用以下預設行為：

| 預設 | Attribution AI | 客戶人工智慧 |
| --- | --- | --- |
| Identity欄 | `endUserIDs._experience.aaid.id` | `endUserIDs._experience.mcid.id` |
| 命名空間 | AAID | ECID |

要設定主標識，請從&#x200B;**[!UICONTROL Schemas]**&#x200B;頁籤導航到您的模式，然後選擇模式名稱超連結以開啟&#x200B;**[!DNL Schema Editor]**。

![導覽至架構](./images/data-preparation/navigate_schema.png)

接著，導覽至您要當做主要身分的欄位，並加以選取。 **[!UICONTROL Field properties]**&#x200B;功能表隨即開啟。

![選取欄位](./images/data-preparation/find_field.png)

在&#x200B;**[!UICONTROL Field properties]**&#x200B;功能表中，向下捲動直到找到&#x200B;**[!UICONTROL Identity]**&#x200B;複選框。 選中該框後，將顯示將選定身份設定為&#x200B;**[!UICONTROL Primary identity]**&#x200B;的選項。 也選擇此框。

![選擇複選框](./images/data-preparation/set_primary_identity.png)

接著，您必須從下拉式清單中預先定義的名稱空間清單中提供&#x200B;**[!UICONTROL Identity namespace]**。 在此示例中，選擇ECID名稱空間是因為使用了Adobe Audience ManagerID `mcid.id`。 選擇&#x200B;**[!UICONTROL Apply]**&#x200B;以確認更新，然後選擇右上角的&#x200B;**[!UICONTROL Save]**&#x200B;以保存對架構所做的更改。

![儲存變更](./images/data-preparation/select_namespace.png)

#### xdm:timestamp {#timestamp}

此欄位表示事件發生的日期時間。 此值必須以字串形式提供，如ISO 8601標準。

#### xdm:channel {#channel}

>[!NOTE]
>
>此欄位僅在使用Attribution AI時為必填欄位。

此欄位代表與ExperienceEvent相關的行銷渠道。 欄位包含頻道類型、媒體類型和位置類型的相關資訊。

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

有關`xdm:channel`每個必要子欄位的完整資訊，請參閱[體驗渠道方案](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md)規範。 有關某些示例映射，請參見[下表](#example-channels)。

#### 通道映射示例{#example-channels}

下表提供映射至`xdm:channel`架構的行銷渠道的一些範例：

| Channel | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| 付費搜尋 | https:/<span>/ns.adobe.com/xdm/channel-types/search | 付款 | 點擊 |
| 社交——行銷 | https:/<span>/ns.adobe.com/xdm/channel-types/social | 掙 | 點擊 |
| 顯示 | https:/<span>/ns.adobe.com/xdm/channel-types/display | 付款 | 點擊 |
| 電子郵件 | https:/<span>/ns.adobe.com/xdm/channel-types/email | 付款 | 點擊 |
| 內部反向連結 | https:/<span>/ns.adobe.com/xdm/channel-types/direct | 擁有 | 點擊 |
| 顯示檢視 | https:/<span>/ns.adobe.com/xdm/channel-types/display | 付款 | 印象 |
| QR Code重新導向 | https:/<span>/ns.adobe.com/xdm/channel-types/direct | 擁有 | 點擊 |
| 行動 | https:/<span>/ns.adobe.com/xdm/channel-types/mobile | 擁有 | 點擊 |

### 建議欄位

本節將概述其餘的關鍵欄位。 雖然[!DNL Intelligent Services]不一定需要這些欄位才能運作，但強烈建議您盡可能多地使用這些欄位，以獲得更豐富的見解。

#### xdm:productListItems

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

有關`xdm:productListItems`每個必需子欄位的完整資訊，請參閱[商務詳細資訊方案](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md)規範。

#### xdm：商務

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

有關`xdm:commerce`每個必需子欄位的完整資訊，請參閱[商務詳細資訊方案](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md)規範。

#### xdm:web

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

有關`xdm:productListItems`每個必要子欄位的完整資訊，請參閱[ExperienceEvent Web詳細資料結構](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md)規格。

#### xdm：行銷

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

有關`xdm:productListItems`每個必要子欄位的完整資訊，請參閱[行銷說明](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md)規格。

## 映射和接收資料{#mapping}

在您確定行銷事件資料是否可映射至CEE架構後，下一步是決定要將哪些資料放入[!DNL Intelligent Services]。 [!DNL Intelligent Services]中使用的所有歷史資料都必須落在資料四個月的最短時間範圍內，加上預期做為回顧期間的天數。

在決定您要傳送的資料範圍後，請聯絡Adobe諮詢服務，協助將資料對應至架構，並將其內嵌至服務。

如果您有[!DNL Adobe Experience Platform]訂閱，而且想要親自對應及收錄資料，請遵循下節所述的步驟。

### 使用Adobe Experience Platform

>[!NOTE]
>
>下列步驟需要訂閱Experience Platform。 如果您沒有平台的存取權，請跳至[後續步驟](#next-steps)區段。

本節概述了將資料對應並收錄至[!DNL Intelligent Services]Experience Platform的工作流程，包括教學課程的連結，以取得詳細步驟。

#### 建立CEE架構和資料集

當您準備開始準備擷取資料時，第一個步驟是建立採用CEE mixin的新XDM架構。 下列教學課程將逐步說明在UI或API中建立新架構的程式：

* [在UI中建立結構](../xdm/tutorials/create-schema-ui.md)
* [在API中建立結構](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>上述教學課程會遵循建立架構的一般工作流程。 選擇架構的類時，必須使用&#x200B;**XDM ExperienceEvent類**。 選擇此類後，可以將CEE混合添加到模式。

將CEE混音新增至架構後，您就可以視資料中其他欄位的需要新增其他混音。

建立並儲存架構後，您就可以根據該架構建立新的資料集。 下列教學課程將逐步說明在UI或API中建立新資料集的程式：

* [在UI中建立資料集](../catalog/datasets/user-guide.md#create) （依照工作流程使用現有架構）
* [在API中建立資料集](../catalog/datasets/create.md)

建立資料集後，您可以在&#x200B;**[!UICONTROL Datasets]**&#x200B;工作區的平台UI中找到它。

![](images/data-preparation/dataset-location.png)

#### 將身分欄位新增至資料集

如果要從[!DNL Adobe Audience Manager]、[!DNL Adobe Analytics]或其他外部源導入資料，則可以選擇將模式欄位設定為標識欄位。 要將模式欄位設定為身份欄位，請查看在[UI教程](../xdm/tutorials/create-schema-ui.md#identity-field)或[API教程](../xdm/tutorials/create-schema-api.md#define-an-identity-descriptor)中設定身份欄位的部分，以建立模式。

如果您從本機CSV檔案擷取資料，可跳至[映射的下一節，並擷取資料](#ingest)。

#### 映射並收錄資料{#ingest}

建立CEE架構和資料集後，您可以開始將資料表對應至架構，並將該資料內嵌至平台。 有關如何在UI中執行此操作的步驟，請參閱[將CSV檔案映射到XDM架構](../ingestion/tutorials/map-a-csv-file.md)的教程。 您可以使用下列[範例JSON檔案](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json)來測試擷取程式，然後再使用您自己的資料。

在填入資料集後，可使用相同的資料集來擷取其他資料檔案。

如果您的資料儲存在支援的協力廠商應用程式中，您也可以選擇建立[來源連接器](../sources/home.md)，即時將行銷事件資料內嵌至[!DNL Platform]。

## 下一步 {#next-steps}

本檔案提供有關準備資料以用於[!DNL Intelligent Services]的一般指引。 如果您需要根據您的使用案例進行其他諮詢，請聯絡Adobe諮詢支援。

在您成功將客戶體驗資料填入資料集後，您就可以使用[!DNL Intelligent Services]產生見解。 請參閱下列檔案以開始使用：

* [Attribution AI 概述](./attribution-ai/overview.md)
* [Customer AI 概述](./customer-ai/overview.md)
