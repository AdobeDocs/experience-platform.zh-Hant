---
keywords: Experience Platform；家庭；智慧服務；熱門主題；智慧服務；智慧服務
solution: Experience Platform
title: 準備資料以在智慧服務中使用
description: 為了讓智慧服務能夠從您的營銷事件資料中發現洞見，資料必須語義豐富並以標準結構進行維護。 智慧服務採用經驗資料模型(XDM)模式來實現。
exl-id: 17bd7cc0-da86-4600-8290-cd07bdd5d262
source-git-commit: 87a8ad253abb219662034652b5f8c4fabfa40484
workflow-type: tm+mt
source-wordcount: '2936'
ht-degree: 0%

---

# 準備資料以供使用 [!DNL Intelligent Services]

為了 [!DNL Intelligent Services] 要從營銷活動資料中發現洞見，資料必須語義豐富並以標準結構進行維護。 [!DNL Intelligent Services] 槓桿 [!DNL Experience Data Model] (XDM)模式來實現。 具體來說，所有在 [!DNL Intelligent Services] 必須符合Consumer ExperienceEvent(CEE)XDM架構或使用Adobe Analytics連接器。 此外，客戶AI支援Adobe Audience Manager連接器。

本文檔提供有關將營銷事件資料從多個渠道映射到CEE架構的一般指導，概述有關架構中重要欄位的資訊，以幫助您確定如何有效地將資料映射到其架構。 如果您計畫使用Adobe Analytics資料，請查看 [Adobe Analytics資料準備](#analytics-data)。 如果您計畫使用Adobe Audience Manager資料（僅限客戶AI），請查看 [Adobe受眾管理器資料準備](#AAM-data)。

## 資料要求

[!DNL Intelligent Services] 根據您建立的目標，需要不同數量的歷史資料。 無論如何，您準備的資料 **全部** [!DNL Intelligent Services] 必須同時包括正向和負向客戶行程/事件。 同時具有負事件和正事件可提高模型精度和準確性。

例如，如果您使用客戶AI來預測購買產品的傾向，則客戶AI的模型需要成功購買路徑的實例和失敗路徑的實例。 這是因為在模型培訓期間，客戶AI希望瞭解哪些事件和行程會導致購買。 這還包括未購買的客戶所採取的操作，例如在將物料添加到購物車時停止行程的個人。 但是，這些客戶可能表現出類似的行為，客戶AI可以提供洞察力並深入分析導致傾向得分較高的主要差異和因素。 同樣，Attribution AI需要事件和行程兩種類型，以便按觸點位置顯示諸如觸點效能、頂級轉換路徑和故障等指標。

有關歷史資料要求的更多示例和資訊，請訪問 [客戶AI](./customer-ai/data-requirements.md#data-requirements) 或 [Attribution AI](./attribution-ai/input-output.md#data-requirements) 輸入/輸出文檔中的歷史資料要求部分。

### 資料拼接准則

建議您盡可能將用戶的事件縫製到公共ID上。 例如，您可能有10個事件中帶有&quot;id1&quot;的用戶資料。 之後，同一用戶刪除了Cookie ID，並在接下來的20個事件中記錄為「id2」。 如果您知道id1和id2對應於同一用戶，最佳做法是使用通用id編寫所有30個事件。

如果不可能，則在建立模型輸入資料時應將每組事件視為不同的用戶。 這樣可確保在模型培訓和評分期間取得最佳結果。

## 工作流摘要

準備過程因資料是儲存在Adobe Experience Platform還是外部而異。 本部分概述了在兩種情況下需要採取的必要步驟。

### 外部資料準備

如果您的資料儲存在Experience Platform之外，則需要將資料映射到 [使用者體驗事件架構](#cee-schema)。 此模式可以與自定義欄位組一起增強，以便更好地捕獲客戶資料。 映射後，您可以使用Consumer ExperienceEvent架構和 [將資料傳輸到平台](../ingestion/home.md)。 然後，在配置 [!DNL Intelligent Service]。

取決於 [!DNL Intelligent Service] 您希望使用，可能需要不同的欄位。 請注意，如果您有可用資料，則最好將資料添加到欄位。 要瞭解有關必填欄位的詳細資訊，請訪問 [Attribution AI](./attribution-ai/input-output.md) 或 [客戶AI](./customer-ai/data-requirements.md) 資料要求指南。

### Adobe Analytics資料準備 {#analytics-data}

客戶AI和Attribution AI本機支援Adobe Analytics資料。 要使用Adobe Analytics資料，請按照文檔中概述的步驟設定 [分析源連接器](../sources/tutorials/ui/create/adobe-applications/analytics.md)。

在源連接器將資料流式傳輸到Experience Platform中後，您可以在實例配置期間選擇Adobe Analytics作為資料源，然後選擇資料集。 在連接設定期間，將自動建立所有必需的架構欄位組和各個欄位。 您不需要將資料集ETL（提取、轉換、載入）轉換為CEE格式。

如果你將通過Adobe Analytics源連接器傳輸到Adobe Experience Platform的資料與Adobe Analytics資料進行比較，你可能會注意到一些差異。 分析源連接器可能會在轉換到體驗資料模型(XDM)架構期間丟棄行。 整行不適合轉換可能有多種原因，包括缺少時間戳、缺少personID、無效或較大的人員ID、無效的分析值等。

有關詳細資訊和示例，請訪問文檔 [比較Adobe Analytics和Customer Journey Analytics資料](https://www.adobe.com/go/compare-aa-data-to-cja-data)。 本文旨在幫助您診斷和解決這些差異，以便您和您的團隊可以不受資料完整性問題的影響，將Adobe Experience Platform資料用於智慧服務。

在Adobe Experience Platform查詢服務中，按channel.typeAtSource查詢運行以下開始時間戳和結束時間戳之間的總記錄，以按市場營銷渠道查找計數。

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
>Adobe Analytics連接器最多需要四周時間來回填資料。 如果您最近設定了連接，則應驗證資料集是否具有客戶或Attribution AI所需的最小資料長度。 請查看中的歷史資料部分 [客戶AI](./customer-ai/data-requirements.md#data-requirements) 或 [Attribution AI](./attribution-ai/input-output.md#data-requirements)，並驗證是否有足夠的資料用於預測目標。

### Adobe Audience Manager資料準備（僅限客戶AI） {#AAM-data}

客戶AI本機支援Adobe Audience Manager資料。 要使用Audience Manager資料，請按照文檔中概述的步驟設定 [Audience Manager源連接器](../sources/tutorials/ui/create/adobe-applications/audience-manager.md)。

一旦源連接器將資料流式傳輸到Experience Platform中，您就可以在客戶AI配置期間選擇Adobe Audience Manager作為資料源，然後選擇資料集。 所有架構欄位組和各個欄位都會在連接設定期間自動建立。 您不需要將資料集ETL（提取、轉換、載入）轉換為CEE格式。

>[!IMPORTANT]
>
>如果最近設定了連接器，則應驗證資料集是否具有所需的最小資料長度。 請查看中的歷史資料部分 [輸入/輸出文檔](./customer-ai/data-requirements.md) 對於客戶AI，並驗證您有足夠的資料用於預測目標。

### [!DNL Experience Platform] 資料準備

如果資料已儲存在 [!DNL Platform] 不通過Adobe Analytics或Adobe Audience Manager（僅限客戶AI）源連接器流式傳輸，請執行以下步驟。 仍建議您瞭解CEE架構。

1. 查看 [使用者體驗事件架構](#cee-schema) 並確定資料是否可以映射到其欄位。
2. 聯繫Adobe咨詢服務，幫助將資料映射到架構並將其插入 [!DNL Intelligent Services]或 [按照本指南中的步驟操作](#mapping) 來映射資料。

## 瞭解CEE架構 {#cee-schema}

消費者體驗事件模式描述個人的行為，因為它與數字營銷事件（Web或移動）以及線上或離線商務活動相關。 此架構的使用是 [!DNL Intelligent Services] 由於其語義上定義得很好的欄位（列），因此避免了任何未知名稱，否則這些名稱會使資料變得不那麼清晰。

與所有XDM ExperienceEvent架構一樣，CEE架構在發生事件（或事件集）時捕獲基於時間序列的系統狀態，包括所涉及的時間點和主題的標識。 「體驗事件」是事實記錄，因此它們是不可改變的，並代表所發生的事件，而不進行聚合或解釋。

[!DNL Intelligent Services] 利用此架構中的幾個關鍵欄位來根據您的市場營銷事件資料生成洞見，所有這些資訊都可以在根級別找到並展開以顯示其必需的子欄位。

![](./images/data-preparation/schema-expansion.gif)

與所有XDM架構一樣，CEE架構欄位組是可擴展的。 換句話說，可以將附加欄位添加到CEE欄位組，並且如有必要，可以將不同的變體包括到多個方案中。

在 [公共XDM儲存庫](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md)。 此外，您還可以查看和複製以下內容 [JSON檔案](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) 例如，如何構建資料以符合CEE模式。 在瞭解下節中概述的關鍵欄位時，請參閱這兩個示例，以確定如何將您自己的資料映射到架構。

## 關鍵欄位

CEE欄位組中有幾個關鍵欄位應用於 [!DNL Intelligent Services] 以生成有用的見解。 本節介紹這些欄位的使用案例和預期資料，並提供指向參考文檔的連結以獲取更多示例。

### 必填欄位

儘管強烈建議使用所有關鍵欄位，但有兩個欄位 **要求** 為了 [!DNL Intelligent Services] 要工作：

* [主標識欄位](#identity)
* [xdm:timestamp](#timestamp)
* [xdm：通道](#channel) (僅對Attribution AI強制)

#### 主要身分識別 {#identity}

必須將架構中的一個欄位設定為主標識欄位，這允許 [!DNL Intelligent Services] 將時間序列資料的每個實例連結到單個人。

您必鬚根據資料的來源和性質確定用作主標識的最佳欄位。 標識欄位必須包括 **標識命名空間** 表示欄位需要的標識資料的類型。 某些有效的命名空間值包括：

>[!NOTE]
>
>Experience CloudID(ECID)也稱為MCID，繼續用於命名空間。

* &quot;電子郵件&quot;
* &quot;phone&quot;
* &quot;mcid&quot;(用於Adobe Audience ManagerID)
* &quot;aaid&quot;(用於Adobe AnalyticsID)

如果您不確定應將哪個欄位用作主要身份，請與Adobe咨詢服務聯繫以確定最佳解決方案。 如果未設定主標識，則智慧服務應用程式使用以下預設行為：

| 預設 | Attribution AI | 客戶AI |
| --- | --- | --- |
| 標識列 | `endUserIDs._experience.aaid.id` | `endUserIDs._experience.mcid.id` |
| 命名空間 | AAID | ECID |

要設定主標識，請從 **[!UICONTROL 架構]** 頁籤，然後選擇模式名稱超連結以開啟 **[!DNL Schema Editor]**。

![導航到架構](./images/data-preparation/navigate_schema.png)

接下來，導航到要作為主標識的欄位並選擇它。 的 **[!UICONTROL 欄位屬性]** 的子菜單。

![選擇欄位](./images/data-preparation/find_field.png)

在 **[!UICONTROL 欄位屬性]** 菜單，向下滾動直到找到 **[!UICONTROL 身份]** 複選框。 選中該框後，將選定標識設定為 **[!UICONTROL 主標識]** 的子菜單。 也選擇此框。

![選中複選框](./images/data-preparation/set_primary_identity.png)

接下來，必須提供 **[!UICONTROL 標識命名空間]** 從下拉清單中的預定義命名空間清單中。 在此示例中，ECID名稱是自Adobe Audience ManagerID以來選擇的 `mcid.id` 正在使用。 選擇 **[!UICONTROL 應用]** 確認更新，然後選擇 **[!UICONTROL 保存]** 的子菜單。

![保存更改](./images/data-preparation/select_namespace.png)

#### xdm:timestamp {#timestamp}

此欄位表示事件發生的日期時間。 此值必須按照ISO 8601標準以字串形式提供。

#### xdm：通道 {#channel}

>[!NOTE]
>
>此欄位僅在使用Attribution AI時是必需的。

此欄位表示與ExperienceEvent相關的市場營銷渠道。 該欄位包括有關頻道類型、媒體類型和位置類型的資訊。

![](./images/data-preparation/channel.png)

**示例架構**

```json
{
  "@id": "https://ns.adobe.com/xdm/channels/facebook-feed",
  "@type": "https://ns.adobe.com/xdm/channel-types/social",
  "xdm:mediaType": "earned",
  "xdm:mediaAction": "clicks"
}
```

有關的每個子欄位的完整資訊 `xdm:channel`，請參閱 [體驗通道模式](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) 規範 有關某些示例映射，請參見 [下表](#example-channels)。

#### 通道映射示例 {#example-channels}

下表提供了映射到 `xdm:channel` 架構：

| Channel | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| 付費搜尋 | https:/<span>/ns.adobe.com/xdm/channel types/search | 付 | 點擊 |
| 社交 — 營銷 | https:/<span>/ns.adobe.com/xdm/渠道類型/社交 | 掙 | 點擊 |
| 顯示 | https:/<span>/ns.adobe.com/xdm/channel types/display | 付 | 點擊 |
| 電子郵件 | https:/<span>/ns.adobe.com/xdm/channel types/email | 付 | 點擊 |
| 內部引用者 | https:/<span>/ns.adobe.com/xdm/channel types/direct | 自 | 點擊 |
| 顯示查看方式 | https:/<span>/ns.adobe.com/xdm/channel types/display | 付 | 印象 |
| QR碼重定向 | https:/<span>/ns.adobe.com/xdm/channel types/direct | 自 | 點擊 |
| 行動 | https:/<span>/ns.adobe.com/xdm/channel types/mobile | 自 | 點擊 |

### 推薦欄位

本節概述了其餘的關鍵欄位。 雖然這些欄位不一定是 [!DNL Intelligent Services] 為了工作，強烈建議您盡可能多地使用這些工具，以獲得更豐富的見解。

#### xdm:productListItems

此欄位是表示客戶選擇的產品的一組項目，包括產品SKU、名稱、價格和數量。

![](./images/data-preparation/productListItems.png)

**示例架構**

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

有關的每個子欄位的完整資訊 `xdm:productListItems`，請參閱 [商務詳細資訊架構](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) 規範

#### xdm：商業

此欄位包含有關ExperienceEvent的特定於商業的資訊，包括採購訂單編號和付款資訊。

![](./images/data-preparation/commerce.png)

**示例架構**

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

有關的每個子欄位的完整資訊 `xdm:commerce`，請參閱 [商務詳細資訊架構](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) 規範

#### xdm:web

此欄位表示與ExperienceEvent相關的Web詳細資訊，如交互、頁面詳細資訊和引用者。

![](./images/data-preparation/web.png)

**示例架構**

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

有關的每個子欄位的完整資訊 `xdm:productListItems`，請參閱 [ExperienceEvent Web詳細資訊架構](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) 規範

#### xdm：市場營銷

此欄位包含與與觸點活動的市場營銷活動相關的資訊。

![](./images/data-preparation/marketing.png)

**示例架構**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

有關的每個子欄位的完整資訊 `xdm:productListItems`，請參閱 [營銷](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md) 規範

## 映射和接收資料 {#mapping}

一旦確定是否可以將營銷事件資料映射到CEE架構，下一步就是確定要將哪些資料引入 [!DNL Intelligent Services]。 使用的所有歷史資料 [!DNL Intelligent Services] 必須在4個月資料的最短時間窗口內，加上要作為回望期的天數。

在確定要發送的資料範圍後，請與Adobe咨詢服務部門聯繫，以幫助將您的資料映射到架構並將其插入服務。

如果你有 [!DNL Adobe Experience Platform] 訂閱並想自己映射和接收資料，請按照下面一節中介紹的步驟操作。

### 使用Adobe Experience Platform

>[!NOTE]
>
>以下步驟需要訂閱Experience Platform。 如果您沒有訪問平台的權限，請跳到 [後續步驟](#next-steps) 的子菜單。

本節概述了將資料映射和插入Experience Platform以用於的工作流 [!DNL Intelligent Services]，包括指向教程的連結，以瞭解詳細步驟。

#### 建立CEE架構和資料集

當您準備開始準備接收資料時，第一步是建立一個使用CEE欄位組的新XDM架構。 以下教程將介紹在UI或API中建立新架構的過程：

* [在UI中建立架構](../xdm/tutorials/create-schema-ui.md)
* [在API中建立架構](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>上述教程遵循建立架構的通用工作流。 為架構選擇類時，必須使用 **XDM ExperienceEvent類**。 選擇此類後，可將CEE欄位組添加到架構。

將CEE欄位組添加到方案後，您可以根據資料中其他欄位的需要添加其他欄位組。

建立並保存架構後，可以基於該架構建立新資料集。 以下教程將介紹在UI或API中建立新資料集的過程：

* [在UI中建立資料集](../catalog/datasets/user-guide.md#create) （按照工作流使用現有架構）
* [在API中建立資料集](../catalog/datasets/create.md)

建立資料集後，您可以在以下位置的平台UI中找到它： **[!UICONTROL 資料集]** 工作區。

![](images/data-preparation/dataset-location.png)

#### 向資料集添加標識欄位

如果要從 [!DNL Adobe Audience Manager]。 [!DNL Adobe Analytics]，或另一個外部源，則可以選擇將架構欄位設定為標識欄位。 要將架構欄位設定為標識欄位，請查看在 [UI教程](../xdm/tutorials/create-schema-ui.md#identity-field) 或 [API教程](../xdm/tutorials/create-schema-api.md#define-an-identity-descriptor) 建立架構。

如果要從本地CSV檔案中接收資料，可跳到上的下一節 [映射和接收資料](#ingest)。

#### 映射和攝取資料 {#ingest}

建立CEE模式和資料集後，可以開始將資料表映射到模式，並將資料接收到平台。 請參閱上的教程 [將CSV檔案映射到XDM架構](../ingestion/tutorials/map-csv/overview.md) 有關如何在UI中執行此操作的步驟。 可以使用以下 [示例JSON檔案](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) test攝取過程，然後使用您自己的資料。

一旦填充了資料集，就可以使用同一資料集來接收其他資料檔案。

如果資料儲存在受支援的第三方應用程式中，您還可以選擇建立 [源連接器](../sources/home.md) 將營銷活動資料 [!DNL Platform] 即時。

## 後續步驟 {#next-steps}

本文檔提供了有關準備資料以供使用的一般指導 [!DNL Intelligent Services]。 如果您需要根據您的使用案例進行其他咨詢，請聯繫Adobe咨詢支援。

一旦您成功地使用客戶體驗資料填充了資料集，您就可以使用 [!DNL Intelligent Services] 來生成洞見。 請參閱以下文檔以開始：

* [Attribution AI 概述](./attribution-ai/overview.md)
* [Customer AI 概述](./customer-ai/overview.md)
