---
title: Adobe Experience Platform 發行說明
description: 2023年3月Adobe Experience Platform發行說明。
source-git-commit: 38c3461f1d84fca83fd04eef57aae28de4744e17
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 4%

---

# Adobe Experience Platform 發行說明

**發行日期：2023 年 3 月 29 日**

Adobe Experience Platform 現有功能更新：

- [資料收集](#data-collection)
- [資料準備](#data-prep)
- [目的地](#destinations)
- [細分服務](#segmentation)
- [來源](#sources)

## 資料收集 {#data-collection}

Adobe Experience Platform提供一套技術，可讓您收集用戶端客戶體驗資料，並傳送至Adobe Experience Platform Edge Network，以便在中加以擴充、轉換及分發至Adobe或非Adobe目的地。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 中繼轉換API（測試版）的全新快速入門工作流程 | 從資料收集主畫面存取「快速入門」底下的全新快速入門工作流程！ 此 [中繼轉換API的快速入門工作流程](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) 讓客戶只需幾個簡單步驟，即可快速收集和轉送事件資料（從伺服器端轉送至中繼），以進行廣告轉換。 |
| [!DNL Braze] 事件轉送擴充功能 | 此 [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 事件轉送擴充功能可讓您運用Adobe Experience Platform邊緣網路中擷取的資料，並將其傳送至 [!DNL Braze] 以伺服器端事件的形式，使用 [!DNL Braze] 使用者追蹤API。 |
| [!DNL Mixpanel] 事件轉送擴充功能 | 此 [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 擴充功能可讓客戶運用事件轉送功能，擷取Adobe Experience Platform邊緣網路中的事件資訊，並使用追蹤事件API將其傳送至Mixpanel。 |

{style="table-layout:auto"}

## 資料準備 {#data-prep}

資料準備可讓資料工程師將資料對應、轉換及驗證至Experience Data Model(XDM)。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 編碼和解碼URL字串的新函式 | <ul><li>此 `get_url_encoded` 函式會以URL作為輸入，並以ASCII字元取代或編碼特殊字元。</li><li>此 `get_url_decoded` 函式會將URL當作輸入，並將ASCII字元解碼為特殊字元。</li></ul> 如需詳細資訊，請閱讀 [資料準備功能指南](../../data-prep/functions.md). 如需保留字元及其對應編碼字元的完整清單，請閱讀指南，位於 [特殊字元](../../data-prep/functions.md#special-characters). |

有關資料準備的詳細資訊，請閱讀 [資料準備概述](../../data-prep/home.md).

## 目的地 {#destinations}

[!DNL Destinations] 預先建置與目的地平台的整合，可順暢地從Adobe Experience Platform啟動資料。 您可以使用目的地來針對跨通路行銷活動、電子郵件行銷活動、目標廣告和其他許多使用案例，啟用已知和未知的資料。

**新目的地** {#new-destinations}

| 目的地 | 說明 |
| ----------- | ----------- |
| [[!DNL Adobe Commerce] 連接GA](../../destinations/catalog/personalization/adobe-commerce.md) | 此 [!DNL Adobe Commerce] 目的地連接器（現已正式推出）可讓您選取一或多個Real-Time CDP對象以啟用至您的 [!DNL Adobe Commerce] 帳戶，為購物者提供動態的個人化體驗。 |
| [[!DNL Snap Inc] 連接GA](../../destinations/catalog/advertising/snap-inc.md) | 此 [!DNL Snap Inc] 目的地連接器（現已正式推出）可讓行銷人員將Experience Platform中建立的使用者區段匯入 [!DNL Snapchat Ads] 並用來鎖定其廣告。 |
| [(API)OracleEloqua連線](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | 使用API型連線至 [!DNL Oracle Eloqua] 在為潛在客戶提供個人化客戶體驗的同時，規劃及執行行銷活動，於 [!DNL Oracle Eloqua]. |
| [（測試版） [!DNL Amazon Ads] 連接](../../destinations/catalog/advertising/amazon-ads.md) | 此 [!DNL Amazon Ads] 與Adobe Experience Platform的整合提供與 [!DNL Amazon Ads] 產品，包括 [!DNL Amazon DSP (ADSP)]. 使用 [!DNL Amazon Ads] Adobe Experience Platform中的目的地，使用者可以定義廣告商對象，以便鎖定和啟用 [!DNL Amazon DSP]. |
| [[!DNL Marketo Measure Ultimate] 連接](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] （前身為Bizible）可讓行銷人員深入了解哪些行銷工作最能有效促進收入，並為公司創造最大的投資報酬率。 目的地可讓企業對企業(B2B)資料從Adobe Experience Platform流至 [!DNL Marketo Measure]. 此卡只能用於 [!DNL Marketo Measure Ultimate] 客戶。 |
| [TikTok連線](../../destinations/catalog/social/tiktok.md) | 使用您的資料在TikTok上建立自訂對象，以便透過您的廣告促銷活動鎖定目標。 |
| [Zendesk連接](../../destinations/catalog/crm/zendesk.md) | 使用此目的地可建立和更新區段內的身分識別，作為內的聯絡人 [!DNL Zendesk]. |

{style="table-layout:auto"}

**新功能或更新功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| ----------- | ----------- |
| 目的地的新存取控制權限： [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | 新權限可讓使用者啟動區段至現有目的地，而不顯示 [對應步驟](../../destinations/ui/activate-batch-profile-destinations.md#mapping). 使用者可以在啟用工作流程中新增和移除區段，但無法新增或移除已對應的屬性或身分。 |

{style="table-layout:auto"}

**修正和增強功能** {#destinations-fixes-and-enhancements}

我們正在針對即時CDP的檔案式目的地發行PGP/GPG加密的錯誤修正。 經過此變更後，目前使用加密的現有檔案型目的地將產生副檔名與先前不同的檔案名稱。

- 使用加密時的當前擴展： `filename.csv`
- 未來使用加密時的擴充功能： `filename.csv.gpg`

如需目的地的詳細一般資訊，請參閱 [目的地概述](../../destinations/home.md).

## 分段服務 {#segmentation}

[!DNL Segmentation Service] 會透過說明區分客戶群中可行銷人員群組的條件，來定義特定設定檔子集。 區段可以根據記錄資料（例如人口統計資訊）或代表客戶與您品牌互動的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 設定檔量度 | 為了讓您更精確地呈現設定檔量度，系統會結合成員劃分和流失量度，現在會在24小時內計算。 如需詳細資訊，請參閱 [區段UI指南](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

如需 [!DNL Segmentation Service]，請參閱 [區段概觀](../../segmentation/home.md).

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，並可讓您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 測試版可用性 [!DNL Chatlio] | 此 [!DNL Chatlio] 來源現在可在測試版中取得。 使用 [!DNL Chatlio] 源流 [!DNL Chatlio] 事件資料Experience Platform。 如需詳細資訊，請閱讀 [[!DNL Chatlio] 概述](../../sources/connectors/marketing-automation/chatlio-webhook.md). |
| 測試版可用性 [!DNL Customer.io] | 此 [!DNL Customer.io] 來源現在可在測試版中取得。 使用 [!DNL Customer.io] 來源來串流客戶事件資料至Experience Platform。 如需詳細資訊，請閱讀 [[!DNL Customer.io] 概述](../../sources/connectors/marketing-automation/customerio-webhook.md). |
| 測試版可用性 [!DNL Pendo] | 此 [!DNL Pendo] 來源現在可在測試版中取得。 使用 [!DNL Pendo] 來源，將您的產品分析資料串流至Experience Platform。 如需詳細資訊，請閱讀 [[!DNL Pendo] 概述](../../sources/connectors/analytics/pendo-webhook.md). |
| 支援草稿資料流 | 您現在可以使用流程服務API將資料流設定為草稿狀態。 之後可更新草稿的資料流，並發佈新資訊。 如需詳細資訊，請參閱 [將源資料流設定為草稿](../../sources/tutorials/api/draft.md). |

{style="table-layout:auto"}

若要進一步了解來源，請閱讀 [來源概觀](../../sources/home.md).
