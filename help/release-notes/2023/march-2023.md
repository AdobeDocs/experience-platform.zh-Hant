---
title: Adobe Experience Platform 發行說明 (2023 年 3 月)
description: Adobe Experience Platform 2023 年 3 月的發行說明。
exl-id: 3f4d764a-77cd-4e4a-ae11-e97a23006a53
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2081'
ht-degree: 97%

---

# Adobe Experience Platform 發行說明

**發行日期：2023 年 3 月 29 日**

Adobe Experience Platform 現有功能的更新：

- [儀表板](#dashboards)
- [資料集合](#data-collection)
- [資料準備](#data-prep)
- [目的地](#destinations)
- [體驗資料模式](#xdm)
- [查詢服務](#query-service)
- [Real-Time Customer Data Platform B2B 版本](#b2b)
- [Segmentation Service](#segmentation)
- [來源](#sources)

## 儀表板 {#dashboards}

Adobe Experience Platform 提供了多個儀表板，您可以透過這些儀表板檢視每日快照期間擷取的有關組織資料的重要分析。

**新功能或更新功能** {#dashboards-new-updated-features}

| 功能 | 說明 |
| --- | --- |
| 使用者定義的儀表板 | 你現在可以&#x200B;**對屬性值進行取樣**，然後再於使用者定義的儀表板小工具撰寫器中將屬性新增到小工具。建立小工具時，該屬性欄中的一些範例值可用於個別屬性。<br>您現在可以使用交換軸按鈕，在您的小工具上&#x200B;**將 X 軸和 Y 軸交換**。將屬性新增到您的小工具時，上述步驟可節省時間並提供更符合人體工學的體驗。這讓您無須再次從屬性面板同時找到兩種屬性。<br>您現在可以&#x200B;**變更小工具內圖例的位置和標題**。小工具上顯示圖例後，您即可將該圖例重新放置在圖表周圍的任何位置，還可以將圖例標題重新命名，就像您可對座標軸標籤和小工具標題採取的動作一樣。 |

{style="table-layout:auto"}

如需有關儀表板的詳細資訊，包括如何授予存取權限和建立自訂小工具，請先詳閱[儀表板概觀](../../dashboards/home.md)。

## 資料收集 {#data-collection}

Adobe Experience Platform 提供了一套技術，讓您可收集用戶端客戶體驗資料並將其傳送到 Adobe Experience Platform Edge Network，在其中可擴充、轉換資料並將其分送至 Adobe 或非 Adobe 目標。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 適用於 Meta Conversions API (Beta) 的全新快速入門工作流程 | 從「資料集合」首頁畫面存取「快速入門」下全新的快速入門工作流程！[適用於 Meta Conversions API 的快速入門工作流程](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=zh-Hant#quick-start)讓客戶可快速收集事件資料並將其從伺服器端轉送到 Meta，僅需幾個簡單步驟即可實現廣告轉換。 |
| 適用於 Mobile SDK (Beta) 的全新快速入門工作流程 | 從「資料集合」首頁畫面存取「快速入門」下全新的快速入門工作流程！[適用於 Mobile SDK (Beta) 的全新快速入門工作流程](https://developer.adobe.com/client-sdks/documentation/)讓您僅需幾個簡單步驟即可快速實作 Mobile SDK 並驗證基本的行動事件。 |
| [!DNL Braze] 事件轉送擴充功能 | 此 [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=zh-Hant) 事件轉送擴充功能可讓您利用在 Adob&#x200B;&#x200B;e Experience Platform Edge Network 中擷取的資料並將其傳送到 [!DNL Braze] (使用 [!DNL Braze] User Track API 並以伺服器端事件的形式)。 |
| [!DNL Epsilon] 事件轉送擴充功能 | 此 [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/overview.html?lang=zh-Hant) 事件轉送擴充功能可讓您利用事件轉送在 Adob&#x200B;&#x200B;e Experience Platform Edge Network 中擷取事件資訊並將其傳送到 [!DNL Epsilon] (使用 [!DNL Epsilon] Event API)。 |
| [!DNL Mixpanel] 事件轉送擴充功能 | 此 [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html?lang=zh-Hant) 擴充功能可讓客戶利用事件轉送在 Adob&#x200B;&#x200B;e Experience Platform Edge Network 中擷取事件資訊並使用 Track Events API 將其傳送到 Mixpanel。 |

{style="table-layout:auto"}

## 資料準備 {#data-prep}

「資料準備」讓資料工程師可在體驗資料模式 (XDM) 之間對應、轉換和驗證資料。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| Adobe Analytics 資料的篩選功能正式推出 | 您現在可以使用「資料準備」功能套用規則和條件對 Analytics 資料進行篩選，然後再將其擷取至即時客戶輪廓中。如需詳細資訊，請至「[篩選用於輪廓擷取的 Analytics 資料](../../sources/tutorials/ui/create/adobe-applications/analytics.md#filtering-for-profile)」詳閱指南。 |
| 用於對 URL 字串進行編碼和解碼的新函數 | <ul><li>此 `get_url_encoded` 函數會將 URL 作為輸入，並使用 ASCII 字元取代特殊字元或對其進行編碼。</li><li>此 `get_url_decoded` 函數會將 URL 作為輸入，並將 ASCII 字元解碼成特殊字元。</li></ul> 如需詳細資訊，請詳閱[「資料準備」功能指南](../../data-prep/functions.md)。如需保留字元及其相對應編碼字元的完整清單，請至「[特殊字元](../../data-prep/functions.md#special-characters)」詳閱指南。 |

如需有關「資料準備」的詳細資訊，請詳閱[「資料準備」概觀](../../data-prep/home.md)。

## 目標 {#destinations}

[!DNL Destinations] 是與目標平台的預先建立整合，能夠順暢啟用來自 Adobe Experience Platform 的資料。您可使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新目標** {#new-destinations}

| 目標 | 說明 |
| ----------- | ----------- |
| [[!DNL Adobe Commerce]  連線正式推出](../../destinations/catalog/personalization/adobe-commerce.md) | 此 [!DNL Adobe Commerce] 目的地連接器 (現已正式推出) 可讓您選取一個或多個 Real-Time CDP 客群，以啟動您的 [!DNL Adobe Commerce] 帳戶，為您的購物者提供動態的個人化體驗。 |
| [[!DNL Snap Inc] 連線正式推出](../../destinations/catalog/advertising/snap-inc.md) | 此 [!DNL Snap Inc] 目的地連接器 (現已正式推出) 讓行銷人員能夠將在 Experience Platform 中建立的使用者區段匯入到 [!DNL Snapchat Ads]，並將其用於投放廣告的目標。 |
| [(API) Oracle Eloqua 連線](../../destinations/catalog/email-marketing/oracle-eloqua-api.md) | 以 API 為基礎連線至 [!DNL Oracle Eloqua]，以規劃和執行行銷活動，同時為在 [!DNL Oracle Eloqua] 中的潛在客戶實現個人化的客戶體驗。 |
| [(Beta)  [!DNL Amazon Ads]  連線](../../destinations/catalog/advertising/amazon-ads.md) | [!DNL Amazon Ads] 和 Adobe Experience Platform 的整合提供了現成可用的整合給 [!DNL Amazon Ads] 產品，包括 [!DNL Amazon DSP (ADSP)]。在 Adob&#x200B;&#x200B;e Experience Platform 中使用 [!DNL Amazon Ads] 目的地，使用者即可定義廣告商客群，以便在 [!DNL Amazon DSP] 上進行目標定位和啟動。 |
| [[!DNL Marketo Measure Ultimate] 連線](../../destinations/catalog/adobe/marketo-measure-ultimate.md) | [!DNL Marketo Measure] (之前稱為 Bizible) 可協助行銷人員深入了解哪些行銷手法最能有效提升公司營收並取得最大的投資報酬率。該目的地支援從 Adob&#x200B;&#x200B;e Experience Platform 至 [!DNL Marketo Measure] 的企業對企業 (B2B) 資料流。卡片僅適用於 [!DNL Marketo Measure Ultimate] 客戶。 |
| [TikTok 連線](../../destinations/catalog/social/tiktok.md) | 使用您的資料在 TikTok 上建置自訂客群，以設定您的廣告行銷活動的目標定位。 |
| [Zendesk 連線](../../destinations/catalog/crm/zendesk.md) | 使用此目的地建立和更新區段內的身分識別，以作為 [!DNL Zendesk] 內的聯絡人。 |

{style="table-layout:auto"}

**新功能或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| ----------- | ----------- |
| 目的地的新存取控制權限：[[!DNL Activate Segments without Mapping]](../../access-control/home.md#permissions) | 新的權限讓使用者能夠將區段啟動至現有的目的地，而無需顯示[對應步驟](../../destinations/ui/activate-batch-profile-destinations.md#mapping)。使用者在啟動工作流程中可以新增和移除區段，但無法新增或移除已對應的屬性或身分識別。 |

{style="table-layout:auto"}

**修正和增強功能** {#destinations-fixes-and-enhancements}

我們正在針對Real-Time CDP的檔案型目的地中發行PGP/GPG加密的錯誤修正。 透過此變更，目前使用加密的現有檔案型目的地會產生具有與以往不同之擴充功能的檔案名稱。

- 使用加密時的現行擴充功能：`filename.csv`
- 使用加密時的未來擴充功能：`filename.csv.gpg`

如需有關目的地的詳細一般資訊，請參閱[目的地概觀](../../destinations/home.md)。

## 體驗資料模式 (XDM) {#xdm}

XDM 是一種開放原始碼的規格，可為帶到 Adobe Experience Platform 中的資料提供通用結構和定義 (結構描述)。若遵守 XDM 標準，即可將所有客戶體驗資料合併到一個常用表述中，以更快速、更整合的方式傳遞分析。您可以從客戶行為中獲得有價值的分析，透過區段定義客戶客群，並使用客戶屬性實現個人化的目的。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| CSV 到結構描述推薦 | 您現在可以上傳本機檔案，無須手動建立結構描述即可建立機器學習生成式結構描述。從[!UICONTROL 來源]工作區上傳範例 CSV 檔案，Adobe 機器學習演算法即會根據目標欄位為您建議結構描述。如需詳細資訊，請參閱此[文件](../../ingestion/tutorials/map-csv/recommendations.md)。 |

{style="table-layout:auto"}

**新的 XDM 元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 類別 | [[!UICONTROL 產品建議項目]](https://github.com/adobe/xdm/pull/1678/files) | 代表產品建議的類別。 |
| 類別 | [[!UICONTROL 決策項目]](https://github.com/adobe/xdm/pull/1678/files) | 可以進行決策的項目。決策流程的輸出會是一個或多個決策項目。 |
| 類別 | [[!UICONTROL 媒體工作階段伺服器逾時]](https://github.com/adobe/xdm/pull/1676/files) | 這表示使用者最後一次已知互動和工作階段關閉那一刻之間經過的時間量 (秒數)。 |
| 欄位群組 | [[!UICONTROL XDM 輪廓計算屬性]](https://github.com/adobe/xdm/pull/1686/files) | 這會將內部 Adob&#x200B;&#x200B;e 服務的計算屬性新增到傳入的客戶資料中。客戶不應使用它來擷取資料。 |
| 資料類型 | [[!UICONTROL 退款項目]](https://github.com/adobe/xdm/pull/1685/files) | 這會表示退款是否和訂單有關聯，並定義退款類型、金額和相關貨幣。 |
| 資料類型 | [[!UICONTROL 類別資料]](https://github.com/adobe/xdm/pull/1677/files) | 此新的資料類型代表產品的類別。 |
| 結構描述 | [[!UICONTROL Adobe Target 分類欄位]](https://github.com/adobe/xdm/pull/1682/files) | 建立 Target 分類資料集的新 XDM 結構描述。這會包含一組對 Target 活動和體驗進行分類的中繼資料欄位。 |

{style="table-layout:auto"}

**已更新的 XDM 元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 欄位群組 | [[!UICONTROL 內容元件詳細資料]](https://github.com/adobe/xdm/pull/1674/files) | `uri-reference` 會從[!UICONTROL 內容元件詳細資料]中移除 |
| 欄位群組 | [[!UICONTROL AJO 實體標記]](https://github.com/adobe/xdm/pull/1672/files) | 已將 AJO 實體標記新增至和「歷程」或「行銷活動」對應的 [!UICONTROL AJO 實體欄位] |
| 欄位群組 | (多個) | 已為 [[!UICONTROL Journey Orchestration 步驟事件通用欄位]](https://github.com/adobe/xdm/pull/1671/files)新增幾個欄位 |
| 欄位群組 | (多個) | [已為[!UICONTROL 媒體報表]](https://github.com/adobe/xdm/pull/1670/files)新增幾個 XDM 事件類型。 |
| 欄位群組 | [!UICONTROL Workfront 變更事件] | 已新增 `Full Record` 和 `Accessor Employee Ids` 欄位群組。 |
| 資料類型 | [[!UICONTROL 產品清單項目]](https://github.com/adobe/xdm/pull/1685/files) | 已新增[!UICONTROL 退款金額]，以表示項目的退款金額 (如有)。 |
| 資料類型 | [[!UICONTROL 訂單]](https://github.com/adobe/xdm/pull/1685/files) | 已新增[!UICONTROL 退款清單]至此訂單的退款清單中。 |
| 資料類型 | [[!UICONTROL 產品清單項目]](https://github.com/adobe/xdm/pull/1677/files) | 已將產品類別新增至此產品的類別資料清單中。 |
| 資料類型 | [!UICONTROL 工作階段細節資訊] | 已新增`pev3`字串欄位[以表示用於報表的媒體串流類型](https://github.com/adobe/xdm/pull/1676/files)。另外又新增了 `pccr` 屬性表示是否發生重新導向。 |
| 資料類型 | [!UICONTROL 申請清單] | 提供[申請清單屬性](https://github.com/adobe/xdm/pull/1675/files)。這些屬性包括名稱、ID 和說明。 |
| 資料類型 | [!UICONTROL Commerce] | [Commerce 資料類型已更新](https://github.com/adobe/xdm/pull/1675/files)，以包括 `requisitionListOpens`、`requisitionListAdds`、`requisitionListRemovals` 和 `requisitionList`。 |

{style="table-layout:auto"}

如需Experience Platform中XDM的詳細資訊，請閱讀[XDM系統總覽](../../xdm/home.md)。

## 查詢服務 {#query-service}

查詢服務可讓您使用標準的 SQL 查詢 Adobe Experience Platform 中的資料[!DNL Data Lake]。您可以加入任何資料湖的資料集，並將查詢結果擷取為新資料集，以用於報表、資料科學工作區或擷取至即時客戶輪廓。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 加速存放區的屬性型存取控制 | 將屬性型存取控制和資料蒸餾器搭配使用，以定義對加速存放區中所有資料集的存取控制。這會控制對於由使用者所建立並儲存在加速存放區中的自訂資料模式的存取權，以支援自訂儀表板。 |

{style="table-layout:auto"}

如需有關查詢服務的詳細資訊，請參閱[查詢服務概觀](../../query-service/home.md)。

## Real-Time Customer Data Platform B2B 版本 {#b2b}

在 Real-Time Customer Data Platform (Real-Time CDP) 上建置的 Real-Time CDP B2B 版本是專為採用企業對企業服務模式操作的行銷人員所建置的。它將來自多個來源的資料集中在一起，並將其合併成包含人員和帳戶輪廓的單一檢視。這種統一的資料讓行銷人員可以精確地以特定客群為目標，並在所有可用的管道中和這些客群互動。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 錯誤修正 | 為了更準確地表示系統中的輪廓，系統不再將內部輪廓包含在 Real-Time Customer Data Platform B2B 版本的輪廓總計數或可定址客群量度中。從今天開始，您可能會看到在輪廓總計數/可定址客群量度中出現一次性下降。您沒有任何資料遭到清除，這單純是計數變更。如果您有任何疑慮，請和您的 Adob&#x200B;&#x200B;e 專員聯絡 |

{style="table-layout:auto"}

若要了解 Real-Time CDP B2B 版本的詳細資訊，請閱讀 [Real-Time CDP B2B 版本概觀](../../rtcdp/overview.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷的一群人的標準，從而定義輪廓的特定子集。區段的基礎可能是記錄資料 (例如人口統計資訊) 或表示客戶與您的品牌互動的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 輪廓量度 | 為了向您更準確地表示輪廓量度，我們將會籍劃分和流失量度合併，而且現在會在 24 小時期間計算。如需詳細資訊，請參閱[分段 UI 指南](../../segmentation/ui/overview.md#browse) |

{style="table-layout:auto"}

如需有關 [!DNL Segmentation Service] 的詳細資訊，請參閱[分段概觀](../../segmentation/home.md)。

## 來源 {#sources}

Adobe Experience Platform可從外部來源擷取資料，並允許您使用Experience Platform服務來建構、加標籤及增強這些資料。 您可以從各種來源擷取資料，例如 Adob&#x200B;&#x200B;e 應用程式、雲端型儲存空間、協力廠商軟體和 CRM 系統。

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| [!DNL Chatlio] 推出 Beta 版 | 此 [!DNL Chatlio] 來源現在推出 Beta 版。使用 [!DNL Chatlio] 來源將您的 [!DNL Chatlio] 事件資料串流至 Experience Platform。如需詳細資訊，請閱讀 [[!DNL Chatlio]  概觀](../../sources/connectors/marketing-automation/chatlio-webhook.md)。 |
| [!DNL Customer.io] 推出 Beta 版 | 此 [!DNL Customer.io] 來源現在推出 Beta 版。使用 [!DNL Customer.io] 來源將您的客戶事件資料串流至 Experience Platform。如需詳細資訊，請閱讀 [[!DNL Customer.io]  概觀](../../sources/connectors/marketing-automation/customerio-webhook.md)。 |
| [!DNL Pendo] 推出 Beta 版 | 此 [!DNL Pendo] 來源現在推出 Beta 版。使用 [!DNL Pendo] 來源將您的產品分析資料串流至 Experience Platform。如需詳細資訊，請閱讀 [[!DNL Pendo]  概觀](../../sources/connectors/analytics/pendo-webhook.md)。 |
| 支援草稿資料流 | 您現在可以使用 Flow Service API 將資料流設定為草稿狀態。稍後可使用新資訊將草稿狀態的資料流更新和發佈。如需詳細資訊，請至「[將來源資料流設定為草稿](../../sources/tutorials/api/draft.md)」詳閱指南。 |

{style="table-layout:auto"}

若要了解有關來源的詳細資訊，請閱讀[來源概觀](../../sources/home.md)。
