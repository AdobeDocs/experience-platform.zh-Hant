---
title: Adobe Experience Platform發行說明2023年3月
description: 2023年3月為Adobe Experience Platform發佈的說明。
exl-id: 3f4d764a-77cd-4e4a-ae11-e97a23006a53
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '2206'
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

Adobe Experience Platform提供了多個儀表板，您可以通過這些儀表板查看有關組織資料的重要見解，如在每日快照中捕獲的。

**新增或更新的功能** {#dashboards-new-updated-features}

| 功能 | 說明 |
| --- | --- |
| 用戶定義的儀表板 | 你現在可以 **示例屬性值** 將屬性添加到用戶定義的儀表板小部件合成器中的小部件之前。 建立小部件時，該屬性列中的幾個示例值可用於單個屬性。<br>你現在可以 **交換X和Y軸** 在小部件上的交換軸按鈕。 這可節省時間，並在向小部件添加屬性時提供更符合人體工學的體驗。 這樣，需要從「屬性」面板中再次查找兩個屬性。<br> 你現在可以 **更改圖例的位置和標題** 在小部件里。 在小部件上出現圖例後，可以將圖例重新定位到圖表的任意位置，還可以重新命名圖例標題，就像使用軸標籤和小部件標題一樣。 |

{style="table-layout:auto"}

有關儀表板的詳細資訊，包括如何授予訪問權限和建立自定義小部件，請從讀取 [儀表板概述](../../dashboards/home.md)。

## 資料收集 {#data-collection}

Adobe Experience Platform公司提供了一套技術，使您能夠收集客戶端客戶體驗資料並將其發送到Adobe Experience Platform邊緣網路，在該網路中，資料可以得到豐富、轉換並分發到Adobe或非Adobe目的地。

**新增或更新的功能**

| 功能 | 說明 |
| --- | --- |
| 新的Meta Conversions API快速啟動工作流(Beta) | 從「資料收集」主螢幕訪問「入門」下的新快速啟動工作流！ 的 [元轉換API的快速啟動工作流](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start) 使客戶能夠快速收集和轉發事件資料，從伺服器端到Meta，只需幾個簡單的步驟即可進行廣告轉換。 |
| Mobile SDK（測試版）的新快速啟動工作流 | 從「資料收集」主螢幕訪問「入門」下的新快速啟動工作流！ 的 [移動SDK的快速啟動工作流](https://developer.adobe.com/client-sdks/documentation/) 使您能夠快速實施移動SDK，並只需幾個簡單的步驟即可驗證基本的移動事件。 |
| [!DNL Braze] 事件轉發擴展 | 的 [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 事件轉發擴展允許您利用在Adobe Experience Platform邊緣網路中捕獲的資料並將其發送到 [!DNL Braze] 以伺服器端事件的形式使用 [!DNL Braze] 用戶跟蹤API。 |
| [!DNL Epsilon] 事件轉發擴展 | 的 [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/overview.html) 擴展允許您利用事件轉發來捕獲Adobe Experience Platform邊緣網路中的事件資訊並將其發送到 [!DNL Epsilon] 使用 [!DNL Epsilon] 事件API。 |
| [!DNL Mixpanel] 事件轉發擴展 | 的 [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) 擴展使客戶能夠利用事件轉發來捕獲Adobe Experience Platform邊緣網路中的事件資訊，並使用跟蹤事件API將其發送到Mixpanel。 |

{style="table-layout:auto"}

## 資料準備 {#data-prep}

資料準備允許資料工程師將資料映射到體驗資料模型(XDM)並驗證資料。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 對Adobe Analytics資料進行篩選的一般可用性 | 現在，您可以使用資料準備功能應用規則和條件來篩選分析資料，然後再將它們插入即時客戶配置檔案。 有關詳細資訊，請閱讀上的指南 [篩選分析資料以接收配置檔案](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile)。 |
| 編碼和解碼URL字串的新函式 | <ul><li>的 `get_url_encoded` 函式以URL為輸入，用ASCII字元替換或編碼特殊字元。</li><li>的 `get_url_decoded` 函式將URL作為輸入，並將ASCII字元解碼為特殊字元。</li></ul> 有關詳細資訊，請閱讀 [資料準備功能指南](../../data-prep/functions.md)。 有關保留字元及其相應編碼字元的綜合清單，請閱讀上的指南 [特殊字元](../../data-prep/functions.md#special-characters)。 |

有關資料準備的詳細資訊，請閱讀 [資料準備概述](../../data-prep/home.md)。

## 目的地 {#destinations}

[!DNL Destinations] 是預先構建的與目標平台的整合，允許無縫激活來自Adobe Experience Platform的資料。 您可以使用目標來激活跨渠道市場營銷活動、電子郵件活動、目標廣告和許多其他使用案例的已知和未知資料。

**新目標** {#new-destinations}

| 目的地 | 說明 |
| ----------- | ----------- |
| [[!DNL Adobe Commerce] 連接GA](../../destinations/catalog/personalization/adobe-commerce.md) | 的 [!DNL Adobe Commerce] 目標連接器（現在通常可用）允許您選擇一個或多個Real-Time CDP受眾以激活到您的 [!DNL Adobe Commerce] 為購物者提供動態個性化體驗。 |
| [[!DNL Snap Inc] 連接GA](../../destinations/catalog/advertising/snap-inc.md) | 的 [!DNL Snap Inc] 目標連接器（現在通常可用）允許商家將在Experience Platform中建立的用戶段導入 [!DNL Snapchat Ads] 用它們來瞄準廣告。 |
| [(API)OracleEloqua連接](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | 使用基於API的連接到 [!DNL Oracle Eloqua] 計畫和執行市場活動，同時為潛在客戶提供個性化的客戶體驗 [!DNL Oracle Eloqua]。 |
| [(Beta) [!DNL Amazon Ads] 連接](../../destinations/catalog/advertising/amazon-ads.md) | 的 [!DNL Amazon Ads] 與Adobe Experience Platform的整合提供轉鍵整合， [!DNL Amazon Ads] 產品，包括 [!DNL Amazon DSP (ADSP)]。 使用 [!DNL Amazon Ads] 目的地在Adobe Experience Platform，用戶能夠定義廣告客戶群，以便在其上進行目標和激活 [!DNL Amazon DSP]。 |
| [[!DNL Marketo Measure Ultimate] 連接](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] （前稱Bizbile）讓營銷人員瞭解哪些營銷努力在推動收入和最大化公司投資回報方面最有效。 目的地使業務對業務(B2B)資料從Adobe Experience Platform流到 [!DNL Marketo Measure]。 該卡僅可用於 [!DNL Marketo Measure Ultimate] 客戶。 |
| [TikTok](../../destinations/catalog/social/tiktok.md) | 利用您的資料在TikTok建立自定義受眾，以針對您的廣告活動。 |
| [Zendesk連接](../../destinations/catalog/crm/zendesk.md) | 使用此目標可建立和更新段內的標識作為段內的聯繫人 [!DNL Zendesk]。 |

{style="table-layout:auto"}

**新增或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| ----------- | ----------- |
| 目標的新訪問控制權限： [[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | 新權限使用戶能夠激活到現有目標的段，而不顯示 [映射步驟](../../destinations/ui/activate-batch-profile-destinations.md#mapping)。 用戶可以在激活工作流中添加和刪除段，但不能添加或刪除映射的屬性或標識。 |

{style="table-layout:auto"}

**修復和增強** {#destinations-fixes-and-enhancements}

我們將在基於檔案的目標中發佈PGP/GPG加密的錯誤修復程式，用於即時CDP。 通過此更改，當前使用加密的現有基於檔案的目標將生成副檔名與以前不同的檔案名。

- 使用加密時的當前擴展： `filename.csv`
- 將來使用加密時的擴展： `filename.csv.gpg`

有關目標的更多一般資訊，請參閱 [目標概述](../../destinations/home.md)。

## 體驗資料模型(XDM) {#xdm}

XDM是一種開源規範，它為傳入Adobe Experience Platform的資料提供通用結構和定義（架構）。 通過遵守XDM標準，所有客戶體驗資料都可以納入到共同的表示形式中，以更快、更整合的方式提供見解。 您可以從客戶操作中獲得有價值的見解，通過細分市場定義客戶受眾，並將客戶屬性用於個性化目的。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| CSV到架構建議 | 現在，您可以上載本地檔案以建立機器學習生成的架構，從而無需手動建立架構。 從 [!UICONTROL 源] 工作區、上載示例CSV檔案和Adobe機器學習算法將根據目標欄位為您建議一個模式。 查看 [文檔](../../ingestion/tutorials/map-csv/recommendations.md) 的子菜單。」 |

{style="table-layout:auto"}

**新的XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 類別 | [[!UICONTROL 優惠項目]](https://github.com/adobe/xdm/pull/1678/files) | 表示優惠的類。 |
| 類別 | [[!UICONTROL 決策項]](https://github.com/adobe/xdm/pull/1678/files) | 可進行判定的項目。 決策過程的輸出是一個或多個決策項。 |
| 類別 | [[!UICONTROL 媒體會話伺服器超時]](https://github.com/adobe/xdm/pull/1676/files) | 這表示在用戶的上次已知交互和會話關閉時之間經過的時間（秒）。 |
| 欄位組 | [[!UICONTROL XDM配置檔案計算屬性]](https://github.com/adobe/xdm/pull/1686/files) | 這會將內部Adobe服務的計算屬性添加到傳入的客戶資料。 客戶不應使用此功能來接收資料。 |
| 資料類型 | [[!UICONTROL 退款項]](https://github.com/adobe/xdm/pull/1685/files) | 指示退款是否與訂單關聯並定義退款類型、金額和關聯幣種。 |
| 資料類型 | [[!UICONTROL 類別資料]](https://github.com/adobe/xdm/pull/1677/files) | 此新資料類型表示產品的類別。 |
| 方案 | [[!UICONTROL Adobe Target分類欄位]](https://github.com/adobe/xdm/pull/1682/files) | 為目標分類資料集建立了新的XDM架構。 它包含一組元資料欄位，用於對目標活動和體驗進行分類。 |

{style="table-layout:auto"}

**更新的XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 欄位組 | [[!UICONTROL 內容元件詳細資訊]](https://github.com/adobe/xdm/pull/1674/files) | `uri-reference` 已從 [!UICONTROL 內容元件詳細資訊] |
| 欄位組 | [[!UICONTROL AJO實體標籤]](https://github.com/adobe/xdm/pull/1672/files) | 已將AJO實體標籤添加到 [!UICONTROL AJO實體欄位]，對應於Journey或Campaign |
| 欄位組 | （多個） | 添加了幾個欄位 [[!UICONTROL Journey Orchestration步驟事件公用欄位]](https://github.com/adobe/xdm/pull/1671/files) |
| 欄位組 | （多個） | [已為添加多個XDM事件類型 [!UICONTROL 媒體報告]](https://github.com/adobe/xdm/pull/1670/files)。 |
| 欄位群組 | [!UICONTROL Workfront變革事件] | 的 `Full Record` 和 `Accessor Employee Ids` 已添加欄位組。 |
| 資料類型 | [[!UICONTROL 產品清單項]](https://github.com/adobe/xdm/pull/1685/files) | 的 [!UICONTROL 退款金額] 增加，以指明該項目的退款額（如有）。 |
| 資料類型 | [[!UICONTROL 訂單 ]](https://github.com/adobe/xdm/pull/1685/files) | [!UICONTROL 退款清單] 已添加到此訂單的退款清單中。 |
| 資料類型 | [[!UICONTROL 產品清單項 ]](https://github.com/adobe/xdm/pull/1677/files) | 產品類別已添加到此產品的類別資料清單中。 |
| 資料類型 | [!UICONTROL 會話詳細資訊資訊] | 已添加 `pev3` 字串欄位 [指示用於報告的媒體流的類型](https://github.com/adobe/xdm/pull/1676/files)。 還添加了 `pccr` 屬性指示是否發生重定向。 |
| 資料類型 | [!UICONTROL 申請清單] | 提供 [申請清單屬性](https://github.com/adobe/xdm/pull/1675/files)。 包括名稱、ID和說明。 |
| 資料類型 | [!UICONTROL Commerce] | 的 [已更新商務資料類型](https://github.com/adobe/xdm/pull/1675/files) 包括 `requisitionListOpens`。 `requisitionListAdds`。 `requisitionListRemovals`, `requisitionList`。 |

{style="table-layout:auto"}

有關平台中XDM的詳細資訊，請閱讀 [XDM系統概述](../../xdm/home.md)。

## 查詢服務 {#query-service}

查詢服務允許您使用標準SQL查詢Adobe Experience Platform的資料 [!DNL Data Lake]。 您可以加入資料湖中的任何資料集，並將查詢結果捕獲為新資料集，以用於報告、Data Science Workspace或接收到即時客戶配置檔案。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 基於屬性的加速儲存訪問控制 | 使用基於屬性的訪問控制與資料Distiller來定義加速儲存上所有資料集的訪問控制。 這控制對用戶建立並儲存在加速儲存上的自定義資料模型的訪問，以便為自定義儀表板提供動力。 |

{style="table-layout:auto"}

有關查詢服務的詳細資訊，請參閱 [查詢服務概述](../../query-service/home.md)。

## Real-Time Customer Data Platform B2B 版本 {#b2b}

Real-Time CDPB2B版本以Real-time Customer Data Platform(Real-Time CDP)為基礎，專門為以企業對企業服務模式運營的營銷人員而設計。 它將來自多個來源的資料匯集在一起，並將其合併到人員和帳戶配置檔案的單個視圖中。 此統一資料使營銷人員能夠精確地瞄準特定受眾，並跨所有可用渠道接觸這些受眾。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 錯誤修復 | 為了在系統中提供更準確的配置檔案表示，系統不再在Real-time Customer Data PlatformB2B版的配置檔案總數或可定址的受眾度量中包含內部配置檔案。 從今天開始，您可能會看到配置檔案總數/可定址受眾度量的一次性下降。 您的資料未被擦除，這只是對計數的更改。 請與您的Adobe主管聯繫，以瞭解您可能有的任何顧慮 |

{style="table-layout:auto"}

要瞭解有關Real-Time CDPB2B版的更多資訊，請閱讀 [Real-Time CDPB2B版概述](../../rtcdp/overview.md)。

## 分段服務 {#segmentation}

[!DNL Segmentation Service] 通過描述區分客戶群中可銷售人員組的標準來定義特定配置檔案子集。 段可以基於記錄資料（如人口統計資訊）或表示客戶與您品牌的交互的時間序列事件。

**新增或更新的功能**

| 功能 | 說明 |
| ------- | ----------- |
| 配置檔案度量 | 為了更準確地表示配置檔案度量，將合併成員資格細分和流失度量，現在將在24小時內計算。 有關詳細資訊，請參閱 [分段UI指南](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

有關 [!DNL Segmentation Service]，請參閱 [分段概述](../../segmentation/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，並允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| Beta可用性 [!DNL Chatlio] | 的 [!DNL Chatlio] 「源」現在在beta中可用。 使用 [!DNL Chatlio] 源流 [!DNL Chatlio] 事件資料到Experience Platform。 有關詳細資訊，請閱讀 [[!DNL Chatlio] 概述](../../sources/connectors/marketing-automation/chatlio-webhook.md)。 |
| Beta可用性 [!DNL Customer.io] | 的 [!DNL Customer.io] 「源」現在在beta中可用。 使用 [!DNL Customer.io] 源，用於將客戶事件資料流化到Experience Platform。 有關詳細資訊，請閱讀 [[!DNL Customer.io] 概述](../../sources/connectors/marketing-automation/customerio-webhook.md)。 |
| Beta可用性 [!DNL Pendo] | 的 [!DNL Pendo] 「源」現在在beta中可用。 使用 [!DNL Pendo] 源以將產品分析資料流化到Experience Platform。 有關詳細資訊，請閱讀 [[!DNL Pendo] 概述](../../sources/connectors/analytics/pendo-webhook.md)。 |
| 支援草稿資料流 | 現在，您可以使用流服務API將資料流設定為草稿狀態。 起草的資料流稍後可以更新並發佈新資訊。 有關詳細資訊，請閱讀上的指南 [將源資料流設定為草稿](../../sources/tutorials/api/draft.md)。 |

{style="table-layout:auto"}

要瞭解有關源的詳細資訊，請閱讀 [源概述](../../sources/home.md)。
