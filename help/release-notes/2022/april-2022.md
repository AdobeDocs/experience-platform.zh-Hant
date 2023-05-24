---
title: Adobe Experience Platform發行說明2022年4月
description: 2022年4月為Adobe Experience Platform發行的說明。
exl-id: 39233787-3089-4469-8363-b006ae41ae21
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2904'
ht-degree: 6%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 4 月 27 日**

Adobe Experience Platform 現有功能更新：

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [[!DNL Dashboards]](#dashboards)
- [資料流](#dataflows)
- [[!DNL Data Prep]](#data-prep)
- [目的地](#destinations)
- [體驗資料模型(XDM)](#xdm)
- [Real-Time Customer Data Platform B2B 版本](#B2B)
- [來源](#sources)

## [!DNL Dashboards] {#dashboards}

平台提供了多個儀表板，您可以通過這些儀表板查看有關組織資料的重要資訊，這些資訊在每日快照期間捕獲。

控制面板為您的組織的資料提供預先配置的報告選項，並直接內置到平台內的營銷員工作流中。 這些控制板可用，無需額外的IT支援，也無需花費額外的時間和精力，通過額外的資料倉庫設計和實施來導出和處理資料。

以下小部件可通過它們各自的儀表板上的小部件庫獲得。 有關 [如何通過小部件庫添加小部件](../../dashboards/customize/widget-library.md)。

**新小部件**

| 小部件 | 控制面板 | 說明 |
| ------ | --------- | ----------- |
| [!UICONTROL 配置檔案添加趨勢] | 設定檔 | 此小部件使用線形圖來說明過去30天、90天或12個月中每天添加到配置檔案儲存的合併配置檔案總數。 |
| [!UICONTROL 映射到目標狀態的受眾] | 設定檔 | 此小部件在單個度量中顯示映射的和未映射的受眾的總數，並使用圓環圖來說明它們的合計之間的比例差異。 |
| [!UICONTROL 觀眾大小] | 設定檔 | 此小部件提供一個雙清單，其中列出最多20個段以及每個段中包含的受眾總數。 該清單取決於所應用的合併策略，並根據受眾總數從高到低排序。 |
| [!UICONTROL 配置檔案計數趨勢] | 設定檔 | 此小部件使用線形圖來說明一段時間內系統中包含的配置檔案總數的趨勢。 資料可以在30天、90天和12個月期間進行可視化。 |
| [!UICONTROL 單個身份配置檔案（按身份）] | 設定檔 | 此小部件使用條形圖來說明僅使用單個唯一標識符標識的配置檔案總數。 該小部件最多支援五種最常見的身份。 |
| [!UICONTROL 目標狀態] | 目的地 | 此小部件將啟用的目標總數顯示為單個度量，並使用圓環圖來說明啟用和禁用的目標之間的比例差異。 |
| [!UICONTROL 按目標平台列出的活動目標] | 目的地 | 此小部件使用雙清單來顯示活動目標平台的清單以及每個目標平台的活動目標總數。 |
| [!UICONTROL 已激活所有目標的受眾] | 目的地 | 此小部件提供單個度量中所有目標上激活的受眾總數。 |
| [!UICONTROL 受眾激活順序] | 區段 | 此小部件提供一個三清單，其中列出了訪問群體的目標名稱、平台和激活日期。 |
| [!UICONTROL 對象規模趨勢] | 區段 | 此小部件提供了線形圖圖，說明在30天、90天和12個月期間內滿足任何段定義條件的配置檔案總數。 |
| [!UICONTROL 受眾大小變化趨勢] | 區段 | 此小部件提供線形圖圖，說明在最近的每日快照之間限定給定段的配置檔案總數之間的差異。 趨勢分析期可以在30天、90天和12個月期間顯示。 |
| [!UICONTROL 按身份分類的受眾規模趨勢] | 區段 | 此小部件基於所選標識類型說明特定段的受眾大小趨勢。 趨勢分析期可以在30天、90天和12個月期間顯示。 |

**新功能** {#new-features}

| 功能 | 控制面板 | 說明 |
| ------- | --------- | ----------- |
| 孤立的配置檔案段成員身份清除 | 配置檔案和許可證使用 | 配置檔案服務現在每天刪除剩餘的段成員，以便更準確地表示您在系統中的配置檔案。 在刪除給定配置檔案的所有配置檔案片段後，將進行此清理。 這可能顯示許可證使用儀表板中「可定址受眾」度量的下降，也可能顯示配置檔案儀表板中「配置檔案計數」度量的下降，因為這些度量包括此版本之前剩餘的段片段。 |

{style="table-layout:auto"}

有關 [[!DNL Profiles]](../../dashboards/guides/profiles.md)。 [[!DNL Destinations]](../../dashboards/guides/destinations.md), [[!DNL Segments]](../../dashboards/guides/segments.md) 儀表板。

## 資料流 {#dataflows}

在平台中，資料被從許多不同的源中攝取，在系統內進行分析，並被激活到各種目的地。 通過向資料流提供透明性，平台使跟蹤這種潛在的非線性資料流的過程變得更容易。

資料流是跨平台移動資料的作業的表示形式。 這些資料流是跨不同的服務配置的，可幫助將資料從源連接器移動到目標資料集，然後由Identity Service和Real-Time Customer Profile利用，最終激活到目標。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 段操控板 | 現在，您可以使用監視儀表板監視段的資料流。 要瞭解更多資訊，請閱讀上的指南 [監視UI中的段](../../dataflows/ui/monitor-segments.md) |

有關資料流的詳細資訊，請參閱 [資料流概述](../../dataflows/home.md)。 要瞭解有關分段的詳細資訊，請參閱 [分段概述](../../segmentation/home.md)。

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 允許資料工程師將資料映射到體驗資料模型(XDM)並驗證資料。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 支援Adobe Analytics來源 | Adobe Analytics源現在支援資料準備功能，允許您在建立資料流時將分析報告套件資料映射到目標XDM架構。 請參閱上的教程 [建立分析源連接](../../sources/tutorials/ui/create/adobe-applications/analytics.md) 的子菜單。 |
| 支援導入現有映射規則 | 現在，您可以從現有資料流導入映射規則，以加快資料流配置並限制錯誤。 請參閱上的教程 [導入現有映射規則](../../data-prep/ui/mapping.md) 的子菜單。 |

有關 [!DNL Data Prep]，請參閱 [[!DNL Data Prep] 概述](../../data-prep/home.md)。

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是預先構建的與目標平台的整合，允許無縫激活來自Adobe Experience Platform的資料。 您可以使用目標來激活跨渠道市場營銷活動、電子郵件活動、目標廣告和許多其他使用案例的已知和未知資料。

**新增或更新的功能**

| 功能 | 說明 |
| ----------- | ----------- |
| 高級企業目標連接器 | 現在，三個企業目標連接器已正式提供： [[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md)。 [[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md), [[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md)。 <br> 企業目標連接器的一般可用性包括以前在測試階段提供的所有功能，以及更多功能： <ul><li>新的身份驗證功能，包括 [Azure事件中心中的共用訪問簽名](../../destinations/catalog/cloud-storage/azure-event-hubs.md#sas-authentication) 更多 [驗證類型](../../destinations/catalog/streaming/http-destination.md#authentication-information) （承載令牌，OAuth 2）;</li><li>[回填歷史配置檔案資料](../../destinations/catalog/streaming/http-destination.md#historical-data-backfill) （在首次激活時發送符合段的歷史配置檔案）;</li><li>現在，這些目標支援資料流運行度量；</li><li>[其他段元資料](../../destinations/catalog/streaming/http-destination.md#destination-details) 包括在資料負載中，包括段名稱和段時間戳；</li><li>支援 [靜態IP地址](/help/destinations/catalog/streaming/ip-address-allow-list.md) 允許客戶Experience Platform。</li></ul> |
| 目標資料流的上下文警報 | 你現在可以 [訂閱警報](../../destinations/ui/alerts.md) 建立目標資料流時，接收有關資料流運行狀態、成功或失敗的警報消息。 您可以選擇在Experience PlatformUI中或通過電子郵件接收警報。 |

### 高級企業目標連接器的發佈流程 {#release-process-enterprise-destinations}

對於AmazonKinesis、Azure事件中心和HTTP API目標，在發佈過程（從4月27日開始）中，您將看到以前的Beta目標卡以及目標目錄中新的通用可用(GA)目標卡。 使用測試目標的客戶配置的任何資料流將在接下來的幾天內遷移到同一目標的GA版本。 這次遷移最終應在4月29日星期五結束前完成。 Beta目標在此短時間窗口內將繼續可見，並標籤為 **已棄用**。

如果您在測試階段使用了這些目標，請注意：

- 如果以前在Beta中與3個目的地中的任何一個一起使用，則不需要採取任何操作。 作為Beta的一部分設定的所有資料流將繼續正常工作，並將遷移到GA版本。
- 如果要從4月27日開始設定這些目標，請使用新的GA版目標。
- 在發佈操作完成後，將刪除標籤為已棄用的Beta卡，估計該操作將在4月29日星期五結束。 Experience Platform工程團隊正在密切監控成功的發佈操作。

**新目標**

| 目的地 | 說明 |
| ----------- | ----------- |
| [!DNL Criteo] | 將資料連接並激活到 [[!DNL Criteo]](../../destinations/catalog/advertising/criteo.md) 廣告平台。 |
| [!DNL Sendgrid] | 將資料連接並激活到 [[!DNL Sendgrid]](../../destinations/catalog/email-marketing/sendgrid.md) 用於交易和營銷電子郵件的平台。 |

有關目標的更多一般資訊，請參閱 [目標概述](../../destinations/home.md)。

## 體驗資料模型(XDM) {#xdm}

XDM是一種開源規範，它為傳入Adobe Experience Platform的資料提供通用結構和定義（架構）。 通過遵守XDM標準，所有客戶體驗資料都可以納入到共同的表示形式中，以更快、更整合的方式提供見解。 您可以從客戶操作中獲得有價值的見解，通過細分市場定義客戶受眾，並將客戶屬性用於個性化目的。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 添加或刪除架構的單個標準欄位 | 現在，通過架構編輯器UI，您可以將標準欄位組的部分添加到您的架構中，從而為您選擇包括的欄位提供了更大的靈活性，而無需從頭構建自定義資源。<br><br>現在，您還可以直接在架構結構中定義即席自定義域，並將它們分配給新的或現有的自定義域組，而無需事先建立或編輯域組。<br><br>請參閱上的指南 [在UI中建立和編輯架構](../../xdm/ui/resources/schemas.md) 的子菜單。 |

{style="table-layout:auto"}

**新的XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 全局架構 | [[!UICONTROL 資料衛生操作請求]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | 捕獲資料清除請求的詳細資訊，以刪除或修改指定資料集或沙盒中的記錄。 |
| 描述符 | [[!UICONTROL 時間序列粒度描述符]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | 指示時間序列和摘要資料的粒度。 應用到架構時，架構 `timestamp` 欄位是此粒度週期中的第一個時間戳。 |
| 類別 | [[!UICONTROL XDM摘要度量]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | 提供具有分組維的預匯總度量，如具有GROUP BY的SQL SELECT的結果。 |
| 欄位群組 | [[!UICONTROL 同意策略評估結果圖]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResults.schema.json) | 捕獲個人的同意策略評估結果。 |
| 欄位群組 | [[!UICONTROL 站點搜索]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | 捕獲與站點搜索相關的資訊，如搜索查詢、篩選和排序。 |
| 欄位群組 | [[!UICONTROL 合併銷售線索]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | 捕獲合併兩個或多個銷售線索的事件的詳細資訊。 |
| 欄位群組 | [[!UICONTROL 已傳送電子郵件]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | 捕獲將電子郵件發送到收件人的事件的詳細資訊。 |
| 欄位群組 | [[!UICONTROL 拼接欄位]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | 捕獲通過事件的標識拼接過程計算的值。 |
| 欄位群組 | [[!UICONTROL 審核的輔助收件人詳細資訊]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | Adobe Journey Optimizer欄位組，用於捕獲審核的輔助收件人詳細資訊。 |
| 欄位群組 | [[!UICONTROL XDM業務帳戶人員關係詳細資訊]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | 捕獲與帳戶 — 人員關係相關的詳細資訊。 |
| 欄位群組 | [[!UICONTROL 帳戶人員詳細資訊]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | 捕獲與帳戶 — 人員關係相關的詳細資訊。 |
| 資料類型 | [[!UICONTROL 購物車]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | 捕獲有關電子商務購物車的資訊。 |
| 資料類型 | [[!UICONTROL 裝運]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | 捕獲一個或多個產品的發運資訊。 |
| 資料類型 | [[!UICONTROL 站點搜索]](https://github.com/adobe/xdm/blob/master/components/datatypes/sitesearch.schema.json) | 捕獲有關站點搜索活動的資訊。 |
| 分機(Workfront) | [[!UICONTROL 操作任務屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | 捕獲與操作任務相關的詳細資訊。 |
| 分機(Workfront) | [[!UICONTROL 工作Portfolio屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | 捕獲與工作組合相關的詳細資訊。 |
| 分機(Workfront) | [[!UICONTROL 工作計畫屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | 捕獲與工作程式相關的詳細資訊。 |
| 分機(Workfront) | [[!UICONTROL 工作項目屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | 捕獲與工作項目相關的詳細資訊。 |

{style="table-layout:auto"}

**更新的XDM元件**

| 元件類型 | 名稱 | 更新說明 |
| --- | --- | --- |
| 全局架構 | [[!UICONTROL 目的地]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | 新的枚舉值 `destinationCategory`。 |
| 描述符 | [[!UICONTROL 友好名稱描述符]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | 增加了對刪除建議值的支援(`meta:enum`)。 |
| 欄位群組 | [[!UICONTROL 用戶登錄過程]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile` 的下界。 |
| 資料類型 | [[!UICONTROL 商務]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | 已添加幾個與購物車相關的欄位。 |
| 資料類型 | [[!UICONTROL 產品清單項]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | 為所選選項和折扣金額添加的新欄位。 |
| 擴展（智慧服務） | [[!UICONTROL 智慧服務JourneyAI發送時間優化]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | 優化發送時間分數的儲存格式。 |
| 分機(Workfront) | [[!UICONTROL Workfront變革事件]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | 幾個欄位替換為 `workfront:customData` 的子菜單。 |
| 分機(Workfront) | [[!UICONTROL 工作任務屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | 添加了幾個欄位。 |
| 分機(Workfront) | [[!UICONTROL 工作對象]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | 父對象類型和自定義表單域的新欄位。 |

{style="table-layout:auto"}

有關平台中XDM的詳細資訊，請參見 [XDM系統概述](../../xdm/home.md)。

## [!DNL Artificial Intelligence/Machine Learning services] {#ai/ml-services}

AI/ML服務使營銷分析員和從業人員能夠利用人工智慧和機器學習在客戶體驗使用案例中的力量。 這可讓行銷分析人員利用業務層級設定，針對公司需求設定專屬預測，而無需資料科學的專業知識。

### Attribution AI

Attribution AI 可將點數歸因到促成轉換事件的接觸點。 行銷人員可善用此工具，協助量化客戶歷程中各個獨立行銷接觸點對行銷的影響。

**已更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 支援多資料集 | 多資料集功能現在支援所有體驗事件資料集以及選擇身份映射作為身份。 只要跨資料集有一個通用的標識命名空間，客戶就可以選擇標識映射和任何關聯的ID。 Attribution AI支援以下架構：Adobe Analytics，體驗活動，消費者體驗活動。 有關Attribution AI中多資料集支援的詳細資訊，請參閱 [Attribution AI使用手冊](../../intelligent-services/attribution-ai/user-guide.md)。 |

有關 [!DNL Intelligent Services]，請參閱 [[!DNL Intelligent Services] 概述](../../intelligent-services/home.md)。

### 客戶AI

在Real-time Customer Data Platform提供的客戶AI用於生成定制傾向得分，如按比例對單個配置檔案進行流失和轉換。 不必將企業需求轉換為機器學習問題、挑選演算法、培訓或部署，就能達成上述目的。

**已更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 支援多資料集 | 多資料集功能現在支援所有體驗事件資料集以及選擇身份映射作為身份。 只要跨資料集有一個通用的標識命名空間，客戶就可以選擇標識映射和任何關聯的ID。 客戶AI支援以下架構：Adobe Analytics、體驗事件、消費者體驗事件和Adobe Audience Manager架構。 有關客戶AI中多資料集支援的詳細資訊，請參閱 [客戶AI使用手冊](../../intelligent-services/customer-ai/user-guide/configure.md)。 |
| 客戶人工智慧中的新模型評價指標 | 客戶人工智慧中的「新增收益」圖表使營銷人員能夠根據其預算和ROI目標確定要瞄準的組大小。 新的升程圖可以衡量模型的質量，從而更好地瞭解它們將超越隨機目標的升程。 有關詳細資訊，請參見 [瞭解客戶AI的見解](../../intelligent-services/customer-ai/user-guide/discover-insights.md) 的子菜單。 |

有關 [!DNL Intelligent Services]，請參閱 [[!DNL Intelligent Services] 概述](../../intelligent-services/home.md)。

## Real-Time Customer Data Platform B2B 版本 {#B2B}

Real-Time CDPB2B版本以Real-time Customer Data Platform(Real-Time CDP)為基礎，專門為以企業對企業服務模式運營的營銷人員而設計。 它將來自多個來源的資料匯集在一起，並將其合併到人員和帳戶配置檔案的單個視圖中。 此統一資料使營銷人員能夠精確地瞄準特定受眾，並跨所有可用渠道接觸這些受眾。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 支援 `isDeleted` 功能 | 全部 [!DNL Marketo] 資料集 `Activities` 現在支援 `isDeleted` 映射。 新映射將自動添加到現有B2B資料流中。 您可以使用 `isDeleted` 映射以過濾已刪除的記錄，以便 [!DNL Data Lake] 與源資料一致。 查看 [[!DNL Marketo] 映射欄位指南](../../sources/connectors/adobe-applications/mapping/marketo.md) 的 `isDeleted`。 |

要瞭解有關Real-time Customer Data PlatformB2B版的詳細資訊，請參閱 [B2B概述](../../rtcdp/b2b-overview.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 支援 [!DNL OneTrust Integration] | 您現在可以使用 [!DNL OneTrust Integration] 從您的 [!DNL OneTrust] 帳戶到平台。 請參閱 [建立 [!DNL OneTrust Integration] 源連接](../../sources/connectors/consent-and-preferences/onetrust.md) 的子菜單。 |
| 支援 [!DNL Square] | 您現在可以使用 [!DNL Square] 從您的 [!DNL Square] 帳戶到平台。 |
| 支援刪除客戶屬性資料流 | 現在，您可以刪除使用「客戶屬性」源連接器建立的資料流。 |

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。
