---
title: Adobe Experience Platform 發行說明
description: 2023年3月Adobe Experience Platform發行說明。
source-git-commit: 5b8dd4b295f9363fd7e848070b1ec21ff519c524
workflow-type: tm+mt
source-wordcount: '2205'
ht-degree: 4%

---

# Adobe Experience Platform 發行說明

**發行日期：2023 年 3 月 29 日**

Adobe Experience Platform 現有功能更新：

- [儀表板](#dashboards)
- [資料收集](#data-collection)
- [資料準備](#data-prep)
- [目的地](#destinations)
- [體驗資料模型](#xdm)
- [查詢服務](#query-service)
- [Real-Time Customer Data Platform B2B 版本](#b2b)
- [細分服務](#segmentation)
- [來源](#sources)

## 儀表板 {#dashboards}

Adobe Experience Platform提供多個控制面板，讓您透過這些控制面板檢視組織資料的重要深入分析（在每日快照中擷取）。

**新功能或更新功能** {#dashboards-new-updated-features}

| 功能 | 說明 |
| --- | --- |
| 使用者定義的控制面板 | 您現在可以 **範例屬性值** 在使用者定義的控制面板工具集撰寫器中，將屬性新增至工具集之前。 建立介面工具集時，該屬性欄中的一些範例值可供個別屬性使用。<br>您現在可以 **交換X軸和Y軸** 帶交換軸按鈕的介面工具集上。 這樣可節省時間，並在將屬性新增至小工具集時提供符合人體工程學的體驗。 這樣，您就無需再從「屬性」面板中尋找這兩個屬性。<br>您現在可以 **更改圖例的位置和標題** 在介面工具集中。 在Widget上出現圖例後，可以將圖例重新定位到圖表的任意位置，並重新命名圖例標題，同樣可以使用軸標籤和Widget標題。 |

{style="table-layout:auto"}

如需控制面板的詳細資訊，包括如何授與存取權限和建立自訂Widget，請從閱讀 [控制面板概觀](../../dashboards/home.md).

## 資料收集 {#data-collection}

Adobe Experience Platform提供一套技術，可讓您收集用戶端客戶體驗資料，並傳送至Adobe Experience Platform Edge Network，以便在中加以擴充、轉換及分發至Adobe或非Adobe目的地。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 中繼轉換API（測試版）的全新快速入門工作流程 | 從資料收集主畫面存取「快速入門」底下的全新快速入門工作流程！ 此 [中繼轉換API的快速入門工作流程](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) 讓客戶只需幾個簡單步驟，即可快速收集和轉送事件資料（從伺服器端轉送至中繼），以進行廣告轉換。 |
| Mobile SDK（測試版）全新快速入門工作流程 | 從資料收集主畫面存取「快速入門」底下的全新快速入門工作流程！ 此 [行動SDK的快速入門工作流程](https://developer.adobe.com/client-sdks/documentation/) 可讓您快速實作行動SDK，並只需幾個簡單步驟即可驗證基本行動事件。 |
| [!DNL Braze] 事件轉送擴充功能 | 此 [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 事件轉送擴充功能可讓您運用Adobe Experience Platform邊緣網路中擷取的資料，並將其傳送至 [!DNL Braze] 以伺服器端事件的形式，使用 [!DNL Braze] 使用者追蹤API。 |
| [!DNL Epsilon] 事件轉送擴充功能 | 此 [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/overview.html) 擴充功能可讓您運用事件轉送功能，擷取Adobe Experience Platform邊緣網路中的事件資訊，並傳送至 [!DNL Epsilon] 使用 [!DNL Epsilon] 事件API。 |
| [!DNL Mixpanel] 事件轉送擴充功能 | 此 [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 擴充功能可讓客戶運用事件轉送功能，擷取Adobe Experience Platform邊緣網路中的事件資訊，並使用追蹤事件API將其傳送至Mixpanel。 |

{style="table-layout:auto"}

## 資料準備 {#data-prep}

資料準備可讓資料工程師將資料對應、轉換及驗證至Experience Data Model(XDM)。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| Adobe Analytics資料篩選的一般可用性 | 您現在可以使用資料準備功能，套用規則和條件，以篩選Analytics資料，再將其擷取至即時客戶設定檔中。 如需詳細資訊，請參閱 [篩選Analytics資料以擷取設定檔](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile). |
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

## Experience Data Model(XDM) {#xdm}

XDM是開放原始碼規格，可針對匯入Adobe Experience Platform的資料提供通用結構和定義（結構）。 遵循XDM標準，所有客戶體驗資料皆可整合至通用表示法，以更快速、更整合的方式提供深入分析。 您可以從客戶動作中獲得寶貴的深入分析、透過區段定義客戶受眾，以及將客戶屬性用於個人化目的。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| CSV結構建議 | 您現在可以上傳本機檔案，以建立機器學習產生的結構，而不需要手動建立結構。 從 [!UICONTROL 來源] 工作區、上傳範例CSV檔案，而Adobe機器學習演算法將根據目標欄位為您建議結構。 請參閱 [檔案](../../ingestion/tutorials/map-csv/recommendations.md) 」。 |

{style="table-layout:auto"}

**新XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 類別 | [[!UICONTROL 選件項目]](https://github.com/adobe/xdm/pull/1678/files) | 代表選件的類別。 |
| 類別 | [[!UICONTROL 決策項目]](https://github.com/adobe/xdm/pull/1678/files) | 可進行決策的項目。 決策過程的輸出是一個或多個決策項。 |
| 類別 | [[!UICONTROL 媒體工作階段伺服器逾時]](https://github.com/adobe/xdm/pull/1676/files) | 這表示使用者上次已知互動與工作階段關閉之間所經過的時間長度（以秒為單位）。 |
| 欄位組 | [[!UICONTROL XDM設定檔計算屬性]](https://github.com/adobe/xdm/pull/1686/files) | 這會將內部Adobe服務的計算屬性新增至傳入的客戶資料。 客戶不應使用此ID擷取資料。 |
| 資料類型 | [[!UICONTROL 退款項目]](https://github.com/adobe/xdm/pull/1685/files) | 指明退款是否與訂單關聯，並定義退款類型、金額和關聯幣種。 |
| 資料類型 | [[!UICONTROL 類別資料]](https://github.com/adobe/xdm/pull/1677/files) | 此新資料類型表示產品的類別。 |
| 方案 | [[!UICONTROL Adobe Target分類欄位]](https://github.com/adobe/xdm/pull/1682/files) | 已為Target分類資料集建立新的XDM結構。 它包含一組可分類Target活動和體驗的中繼資料欄位。 |

{style="table-layout:auto"}

**更新XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 欄位組 | [[!UICONTROL 內容元件詳細資訊]](https://github.com/adobe/xdm/pull/1674/files) | `uri-reference` 已從 [!UICONTROL 內容元件詳細資訊] |
| 欄位組 | [[!UICONTROL AJO實體標籤]](https://github.com/adobe/xdm/pull/1672/files) | 將AJO實體標籤新增至 [!UICONTROL AJO實體欄位]，對應至歷程或行銷活動 |
| 欄位組 | （多個） | 新增數個欄位 [[!UICONTROL Journey Orchestration步驟事件常見欄位]](https://github.com/adobe/xdm/pull/1671/files) |
| 欄位組 | （多個） | [為新增數種XDM事件類型 [!UICONTROL 媒體報表]](https://github.com/adobe/xdm/pull/1670/files). |
| 欄位群組 | [!UICONTROL Workfront變更事件] | 此 `Full Record` 和 `Accessor Employee Ids` 已新增欄位群組。 |
| 資料類型 | [[!UICONTROL 產品清單項目]](https://github.com/adobe/xdm/pull/1685/files) | 此 [!UICONTROL 退款金額] 已新增，以指出該項目所退還的金額（如有）。 |
| 資料類型 | [[!UICONTROL 順序 ]](https://github.com/adobe/xdm/pull/1685/files) | [!UICONTROL 退款清單] 已新增至此訂單的退款清單。 |
| 資料類型 | [[!UICONTROL 產品清單項目 ]](https://github.com/adobe/xdm/pull/1677/files) | 已將產品類別新增至此產品的類別資料清單。 |
| 資料類型 | [!UICONTROL 工作階段詳細資訊] | 新增 `pev3` 字串欄位 [指出用於報告的媒體資料流的類型](https://github.com/adobe/xdm/pull/1676/files). 也新增 `pccr` 屬性會指出是否發生重新導向。 |
| 資料類型 | [!UICONTROL 申請清單] | 提供 [申請清單屬性](https://github.com/adobe/xdm/pull/1675/files). 包括名稱、ID和說明。 |
| 資料類型 | [!UICONTROL Commerce] | 此 [已更新商務資料類型](https://github.com/adobe/xdm/pull/1675/files) 包含 `requisitionListOpens`, `requisitionListAdds`, `requisitionListRemovals`，和 `requisitionList`. |

{style="table-layout:auto"}

如需Platform中XDM的詳細資訊，請參閱 [XDM系統概觀](../../xdm/home.md).

## 查詢服務 {#query-service}

查詢服務可讓您使用標準SQL在Adobe Experience Platform中查詢資料 [!DNL Data Lake]. 您可以加入Data Lake中的任何資料集，並將查詢結果擷取為新資料集，以用於報表、Data Science Workspace或擷取至即時客戶個人檔案。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 基於屬性的加速儲存訪問控制 | 使用「屬性型存取控制與資料Distiller」 ，針對加速存放區上的所有資料集定義存取控制。 這可控制對使用者建立並儲存於加速存放區的自訂資料模型的存取，以支援自訂控制面板。 |

{style="table-layout:auto"}

有關Query Services的詳細資訊，請參閱 [查詢服務概述](../../query-service/home.md).

## Real-Time Customer Data Platform B2B 版本 {#b2b}

Real-Time CDP B2B Edition以Real-time Customer Data Platform(Real-Time CDP)為基礎，專為以企業對企業服務模式運作的行銷人員所打造。 它匯集了來自多個來源的資料，並將其結合為人員和帳戶設定檔的單一檢視。 此統一的資料可讓行銷人員精確鎖定特定對象，並參與所有可用管道中的這些對象。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 錯誤修正 | 為了在您的系統中提供更精確的描述檔，系統不再在Real-time Customer Data Platform B2B版的總設定檔計數或可定址對象量度中包含內部設定檔。 從今天開始，設定檔總計數/可定址對象量度可能會一次性下降。 你的所有資料都沒有被清除，這只是計數的變化。 如有任何疑慮，請連絡您的Adobe主管 |

{style="table-layout:auto"}

若要進一步了解Real-Time CDP B2B版，請閱讀 [Real-Time CDP B2B版概述](../../rtcdp/overview.md).

## 分段服務 {#segmentation}

[!DNL Segmentation Service] 會透過說明區分客戶群中可行銷人員群組的條件，來定義特定設定檔子集。 區段可以根據記錄資料（例如人口統計資訊）或代表客戶與您品牌互動的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
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
