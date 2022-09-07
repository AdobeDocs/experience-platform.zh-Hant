---
keywords: Experience Platform；首頁；智慧服務；熱門主題；智慧服務；智慧服務
solution: Experience Platform
title: 準備資料以用於Intelligent Services
topic-legacy: Intelligent Services
description: 為了讓Intelligent Services從您的行銷事件資料中探索深入分析，資料必須在語義上加以擴充並維護為標準結構。 Intelligent Services會使用Experience Data Model(XDM)結構來達成此目標。
exl-id: 17bd7cc0-da86-4600-8290-cd07bdd5d262
source-git-commit: e33d59c4ac28f55ba6ae2fc073d02f8738159263
workflow-type: tm+mt
source-wordcount: '2936'
ht-degree: 0%

---

# 準備資料以用於 [!DNL Intelligent Services]

為了 [!DNL Intelligent Services] 若要從行銷事件資料中探索深入分析，資料必須在語義上加以擴充並維護為標準結構。 [!DNL Intelligent Services] 善用 [!DNL Experience Data Model] (XDM)結構來達成此目標。 尤其是 [!DNL Intelligent Services] 必須符合消費者ExperienceEvent(CEE)XDM架構，或使用Adobe Analytics連接器。 此外，Customer AI支援Adobe Audience Manager連接器。

本檔案提供將行銷事件資料從多個管道對應至CEE架構的一般指引，概述架構內重要欄位的資訊，協助您判斷如何將資料有效對應至架構。 如果您打算使用Adobe Analytics資料，請檢視 [Adobe Analytics資料準備](#analytics-data). 如果您打算使用Adobe Audience Manager資料（僅限Customer AI），請檢視 [AdobeAudience Manager資料準備](#AAM-data).

## 資料需求

[!DNL Intelligent Services] 根據您建立的目標，需要不同數量的歷史資料。 無論如何，您準備的資料 **all** [!DNL Intelligent Services] 必須同時包含正面和負面的客戶歷程/事件。 同時包含負事件和正事件可提高模型精度和準確度。

例如，如果您使用Customer AI來預測購買產品的傾向，Customer AI的模型需要成功購買路徑的範例和失敗路徑的範例。 這是因為在模型訓練期間，Customer AI會了解導致購買的事件和歷程。 這也包括未購買的客戶所採取的動作，例如在將項目新增至購物車時停止歷程的個人。 這些客戶可能表現出類似的行為，但Customer AI可提供深入分析並深入分析導致傾向分數較高的主要差異和因素。 同樣地，Attribution AI需要事件和歷程兩種類型，才能依接觸點位置顯示量度，例如接觸點效益、最上層轉換路徑和劃分。

如需歷史資料需求的更多範例和資訊，請造訪 [Customer AI](./customer-ai/input-output.md#data-requirements) 或 [Attribution AI](./attribution-ai/input-output.md#data-requirements) 輸入/輸出檔案中的歷史資料需求區段。

### 連結資料的准則

建議您盡可能將使用者的事件拼接在通用ID之間。 例如，您可能有10個事件中「id1」的使用者資料。 之後，同一位使用者刪除了Cookie ID，並在後續20個事件中記錄為「id2」。 如果您知道id1和id2對應至相同的使用者，最佳作法是將所有30個事件以通用id匯整。

如果無法這麼做，在建立模型輸入資料時，您應將每組事件視為不同的使用者。 這可確保在模型訓練和計分期間取得最佳結果。

## 工作流程摘要

準備程式會依您的資料儲存在Adobe Experience Platform還是外部而有所不同。 本節總結了在兩種情況下需要採取的必要步驟。

### 外部資料準備

如果您的資料儲存在Experience Platform之外，您必須將資料對應至 [消費者體驗事件結構](#cee-schema). 此結構可以與自訂欄位群組搭配使用，以更妥善地擷取客戶資料。 對應後，您就可以使用消費者體驗事件結構建立資料集，並 [將資料內嵌至Platform](../ingestion/home.md). 然後，在設定 [!DNL Intelligent Service].

視 [!DNL Intelligent Service] 若您想使用，可能需要不同欄位。 請注意，如果您有可用資料，最好將資料新增至欄位。 若要進一步了解必填欄位，請造訪 [Attribution AI](./attribution-ai/input-output.md) 或 [Customer AI](./customer-ai/input-output.md) 輸入/輸出指南。

### Adobe Analytics資料準備 {#analytics-data}

Customer AI和Attribution AI原生支援Adobe Analytics資料。 若要使用Adobe Analytics資料，請依照檔案中概述的步驟，設定 [Analytics來源連接器](../sources/tutorials/ui/create/adobe-applications/analytics.md).

在來源連接器將您的資料串流至Experience Platform後，您就可以在執行個體設定期間，選取Adobe Analytics作為資料來源，接著再選取資料集。 在連接設定期間，會自動建立所有必要架構欄位組和各個欄位。 您不需要將資料集（擷取、轉換、載入）ETL為CEE格式。

如果比較透過Adobe Analytics來源連接器傳送至Adobe Experience Platform的資料與Adobe Analytics資料，您可能會發現一些差異。 在轉換為Experience Data Model(XDM)架構期間，Analytics來源連接器可能會放置列。 整列不適合轉換的原因可能有多種，包括遺失時間戳、遺失personID、無效或大人員ID、無效的分析值等。

如需詳細資訊和範例，請造訪 [比較Adobe Analytics和Customer Journey Analytics資料](https://www.adobe.com/go/compare-aa-data-to-cja-data). 本文旨在協助您診斷並解決這些差異，讓您和您的團隊能不受資料完整性疑慮的影響，將Adobe Experience Platform資料用於智慧服務。

在Adobe Experience Platform Query Services中，依channel.typeAtSource查詢執行下列開始和結束時間戳記之間的記錄總數，以依行銷管道尋找計數。

```SELECT channel.typeAtSource as typeAtSource,
       Count(_id) AS Records 
FROM  df_hotel
WHERE timestamp>=from_utc_timestamp('2021-05-15','UTC')
        AND timestamp<from_utc_timestamp('2022-01-10','UTC')
        AND timestamp IS NOT NULL
        AND enduserids._experience.aaid.id IS NOT NULL
GROUP BY channel.typeAtSource
```

>[!IMPORTANT]
>
>Adobe Analytics連接器最多需要四周時間來回填資料。 如果您最近設定了連線，應確認資料集擁有客戶或Attribution AI所需的最小資料長度。 請參閱 [Customer AI](./customer-ai/input-output.md#data-requirements) 或 [Attribution AI](./attribution-ai/input-output.md#data-requirements)，並驗證您有足夠的資料用於預測目標。

### Adobe Audience Manager資料準備（僅限客戶AI） {#AAM-data}

Customer AI原生支援Adobe Audience Manager資料。 若要使用Audience Manager資料，請依照檔案中概述的步驟，設定 [Audience Manager源連接器](../sources/tutorials/ui/create/adobe-applications/audience-manager.md).

在來源連接器將您的資料串流至Experience Platform後，您就可以在Customer AI設定期間，選取Adobe Audience Manager作為資料來源，接著再選取資料集。 連接設定期間會自動建立所有架構欄位群組和個別欄位。 您不需要將資料集（擷取、轉換、載入）ETL為CEE格式。

>[!IMPORTANT]
>
>如果您最近設定了連接器，應確認資料集具有所需的最小資料長度。 請參閱 [輸入/輸出檔案](./customer-ai/input-output.md) 針對Customer AI，並確認您有足夠的資料用於您的預測目標。

### [!DNL Experience Platform] 資料準備

如果您的資料已儲存在 [!DNL Platform] 而非透過Adobe Analytics或Adobe Audience Manager（僅限Customer AI）來源連接器串流，請遵循下列步驟。 仍建議您了解CEE架構。

1. 檢閱 [消費者體驗事件結構](#cee-schema) 並判斷資料是否可對應至其欄位。
2. 請連絡Adobe諮詢服務，協助您將資料對應至結構並內嵌至 [!DNL Intelligent Services]，或 [請依照本指南中的步驟操作](#mapping) 如果您想要自行對應資料。

## 了解CEE架構 {#cee-schema}

消費者體驗事件結構描述個人的行為，因為它與數位行銷事件（網頁或行動裝置）以及線上或離線商務活動相關。 此架構的使用 [!DNL Intelligent Services] 因為其語義上定義良好的欄位（欄），所以可以避免任何未知名稱，否則會讓資料較不清楚。

與所有XDM ExperienceEvent結構一樣，CEE結構會在發生事件（或一組事件）時，擷取系統以時間序列為基礎的狀態，包括時間點和相關主體的身分。 體驗事件是已發生的事實記錄，因此它們不可變，不經匯總或解釋即代表已發生的事件。

[!DNL Intelligent Services] 利用此結構中的數個關鍵欄位，從行銷事件資料產生深入分析，所有這些資料都可在根層級找到，並展開以顯示其必要的子欄位。

![](./images/data-preparation/schema-expansion.gif)

與所有XDM結構一樣，CEE結構欄位群組也可擴充。 換言之，CEE欄位組中可以添加其他欄位，如有必要，多個結構中可以包含不同的變化。

如需欄位群組的完整範例，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md). 此外，您還可以檢視並複製下列項目 [JSON檔案](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) 例如，如何根據CEE架構來建構資料。 請參閱這兩個範例，以了解下節中概述的關鍵欄位，以決定如何將您自己的資料對應至結構。

## 索引鍵欄位

CEE欄位組中有幾個關鍵欄位，應按順序使用 [!DNL Intelligent Services] 來產生有用的深入分析。 本節說明這些欄位的使用案例和預期資料，並提供參考檔案的連結以取得進一步範例。

### 必填欄位

雖然強烈建議使用所有關鍵欄位，但有兩個欄位 **必填** 為 [!DNL Intelligent Services] 若要運作：

* [主要身分欄位](#identity)
* [xdm:timestamp](#timestamp)
* [xdm:channel](#channel) (僅Attribution AI強制)

#### 主要身分 {#identity}

架構中的其中一個欄位必須設定為主要身分欄位，這可允許 [!DNL Intelligent Services] 將時間序列資料的每個例項連結至個別人員。

您必鬚根據資料的來源和性質，決定要用作主要身分的最佳欄位。 身分欄位必須包含 **身分命名空間** 表示欄位預期的身分資料類型為值。 一些有效的命名空間值包括：

>[!NOTE]
>
>Experience CloudID(ECID)也稱為MCID，會繼續用於命名空間。

* &quot;電子郵件&quot;
* &quot;phone&quot;
* &quot;mcid&quot;(適用於Adobe Audience Manager ID)
* &quot;aaid&quot;(適用於Adobe Analytics ID)

如果您不確定應將哪個欄位作為主要身分，請聯絡Adobe諮詢服務以決定最佳解決方案。 如果未設定主身份，智慧服務應用程式將使用以下預設行為：

| 預設 | Attribution AI | Customer AI |
| --- | --- | --- |
| 身分欄 | `endUserIDs._experience.aaid.id` | `endUserIDs._experience.mcid.id` |
| 命名空間 | AAID | ECID |

若要設定主要身分，請從 **[!UICONTROL 結構]** 頁簽，然後選擇架構名稱超連結以開啟 **[!DNL Schema Editor]**.

![導覽至結構](./images/data-preparation/navigate_schema.png)

接下來，導覽至您要作為主要身分的欄位，並加以選取。 此 **[!UICONTROL 欄位屬性]** 的子菜單。

![選取欄位](./images/data-preparation/find_field.png)

在 **[!UICONTROL 欄位屬性]** 菜單，向下滾動直到找到 **[!UICONTROL 身分]** 核取方塊。 核取方塊後，將選取的身分設定為 **[!UICONTROL 主要身分]** 框。 也選擇此框。

![選取核取方塊](./images/data-preparation/set_primary_identity.png)

接下來，您必須提供 **[!UICONTROL 身分命名空間]** 從下拉式清單中預先定義的命名空間清單。 在此範例中，自Adobe Audience Manager ID起即會選取ECID命名空間 `mcid.id` 正在使用。 選擇 **[!UICONTROL 套用]** 若要確認更新，請選取 **[!UICONTROL 儲存]** 的子句。

![儲存變更](./images/data-preparation/select_namespace.png)

#### xdm:timestamp {#timestamp}

此欄位表示事件發生的日期時間。 此值必須按照ISO 8601標準提供為字串。

#### xdm:channel {#channel}

>[!NOTE]
>
>此欄位僅在使用Attribution AI時為必填欄位。

此欄位代表與ExperienceEvent相關的行銷管道。 欄位包含通道類型、媒體類型和位置類型的相關資訊。

![](./images/data-preparation/channel.png)

**範例結構**

```json
{
  "@id": "https://ns.adobe.com/xdm/channels/facebook-feed",
  "@type": "https://ns.adobe.com/xdm/channel-types/social",
  "xdm:mediaType": "earned",
  "xdm:mediaAction": "clicks"
}
```

如需 `xdm:channel`，請參閱 [體驗管道結構](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) 規格。 如需某些範例對應，請參閱 [下表](#example-channels).

#### 通道對應範例 {#example-channels}

下表提供對應至 `xdm:channel` 方案：

| Channel | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| 付費搜尋 | https:/<span>/ns.adobe/com/xdm/channel-types/search | 付款 | 點按 |
| 社交 — 行銷 | https:/<span>/ns.adobe/com/xdm/channel-types/social | 掙 | 點按 |
| 顯示 | https:/<span>/ns.adobe/com/xdm/channel-types/display | 付款 | 點按 |
| 電子郵件 | https:/<span>/ns.adobe/com/xdm/channel-types/email | 付款 | 點按 |
| 內部反向連結 | https:/<span>/ns.adobe/com/xdm/channel-types/direct | 自有 | 點按 |
| 顯示視圖 | https:/<span>/ns.adobe/com/xdm/channel-types/display | 付款 | 曝光數 |
| QR碼重新導向 | https:/<span>/ns.adobe/com/xdm/channel-types/direct | 自有 | 點按 |
| 行動 | https:/<span>/ns.adobe/com/xdm/channel-types/mobile | 自有 | 點按 |

### 建議欄位

本節將概述其餘關鍵欄位。 雖然這些欄位不一定是 [!DNL Intelligent Services] 為了有效運作，強烈建議您盡可能使用其中的多個，以獲得更豐富的見解。

#### xdm:productListItems

此欄位是代表客戶所選產品的項目陣列，包括產品SKU、名稱、價格和數量。

![](./images/data-preparation/productListItems.png)

**範例結構**

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

如需 `xdm:productListItems`，請參閱 [商務詳細資訊方案](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) 規格。

#### xdm:commerce

此欄位包含ExperienceEvent的商務專屬資訊，包括採購訂單編號和付款資訊。

![](./images/data-preparation/commerce.png)

**範例結構**

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

如需 `xdm:commerce`，請參閱 [商務詳細資訊方案](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) 規格。

#### xdm:web

此欄位代表與ExperienceEvent相關的網頁詳細資料，例如互動、頁面詳細資料和反向連結。

![](./images/data-preparation/web.png)

**範例結構**

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

如需 `xdm:productListItems`，請參閱 [ExperienceEvent網頁詳細資料結構](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) 規格。

#### xdm:marketing

此欄位包含與接觸點作用中之行銷活動相關的資訊。

![](./images/data-preparation/marketing.png)

**範例結構**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

如需 `xdm:productListItems`，請參閱 [行銷部門](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md) 規格。

## 對應和擷取資料 {#mapping}

在您判斷行銷事件資料是否可對應至CEE架構後，下一步就是決定要將哪些資料帶入 [!DNL Intelligent Services]. 中使用的所有歷史資料 [!DNL Intelligent Services] 必須落在4個月資料的最短時間範圍內，加上預計做為回顧期間的天數。

決定您要傳送的資料範圍後，請連絡Adobe諮詢服務，協助將您的資料對應至結構並將其擷取至服務。

如果您有 [!DNL Adobe Experience Platform] 訂閱，並想要自行對應及內嵌資料，請遵循下節所述的步驟。

### 使用Adobe Experience Platform

>[!NOTE]
>
>下列步驟需要訂閱Experience Platform。 如果您沒有Platform的存取權，請跳至 [後續步驟](#next-steps) 區段。

本節概述將資料對應及擷取至Experience Platform以用於 [!DNL Intelligent Services]，包括教學課程的連結，以取得詳細步驟。

#### 建立CEE架構和資料集

當您準備好開始準備擷取資料時，第一步是建立採用CEE欄位群組的新XDM架構。 下列教學課程會逐步說明如何在UI或API中建立新結構描述的程式：

* [在UI中建立結構](../xdm/tutorials/create-schema-ui.md)
* [在API中建立結構](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>上述教學課程會遵循一般工作流程來建立結構。 為架構選擇類時，必須使用 **XDM ExperienceEvent類別**. 選擇此類後，您就可以將CEE欄位組添加到架構中。

將CEE欄位組添加到架構後，您可以根據需要添加其他欄位組，以便在資料中添加其他欄位。

建立並儲存結構後，您就可以根據該結構建立新的資料集。 下列教學課程會逐步說明如何在UI或API中建立新資料集的程式：

* [在UI中建立資料集](../catalog/datasets/user-guide.md#create) （依照工作流程使用現有結構）
* [在API中建立資料集](../catalog/datasets/create.md)

建立資料集後，您可以在 **[!UICONTROL 資料集]** 工作區。

![](images/data-preparation/dataset-location.png)

#### 將身分欄位新增至資料集

如果您要從 [!DNL Adobe Audience Manager], [!DNL Adobe Analytics]、或其他外部來源，則您可以選擇將結構欄位設為身分欄位。 若要將結構欄位設為身分欄位，請檢視 [UI教學課程](../xdm/tutorials/create-schema-ui.md#identity-field) 或 [API教學課程](../xdm/tutorials/create-schema-api.md#define-an-identity-descriptor) 來建立結構。

如果您要從本機CSV檔案擷取資料，可跳至 [對應和擷取資料](#ingest).

#### 對應及內嵌資料 {#ingest}

建立CEE架構和資料集後，您可以開始將資料表對應至架構，並將該資料內嵌至Platform。 請參閱 [將CSV檔案對應至XDM結構](../ingestion/tutorials/map-a-csv-file.md) 以取得在UI中執行此動作的步驟。 您可以使用下列項目 [範例JSON檔案](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) 以在使用您自己的資料之前測試擷取程式。

填入資料集後，即可使用相同的資料集內嵌其他資料檔案。

如果您的資料儲存在支援的協力廠商應用程式中，您也可以選擇建立 [來源連接器](../sources/home.md) 將行銷事件資料內嵌至 [!DNL Platform] 即時。

## 後續步驟 {#next-steps}

本檔案提供準備資料以用於 [!DNL Intelligent Services]. 如果您需要根據您的使用案例進行其他諮詢，請聯絡Adobe諮詢支援。

在您成功填入客戶體驗資料的資料集後，即可使用 [!DNL Intelligent Services] 以產生深入分析。 請參閱下列檔案以開始使用：

* [Attribution AI 概述](./attribution-ai/overview.md)
* [Customer AI 概述](./customer-ai/overview.md)
