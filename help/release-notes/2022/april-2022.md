---
title: Adobe Experience Platform發行說明2022年4月
description: 2022年4月Adobe Experience Platform發行說明。
exl-id: 39233787-3089-4469-8363-b006ae41ae21
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '2916'
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
- [Experience Data Model(XDM)](#xdm)
- [Real-Time Customer Data Platform B2B 版本](#B2B)
- [來源](#sources)

## [!DNL Dashboards] {#dashboards}

Platform提供多個控制面板，您可以透過這些控制面板檢視有關組織資料的重要資訊，如每日快照時所擷取。

控制面板提供組織資料的預先設定報表選項，並直接內建在Platform內的行銷人員工作流程中。 這些儀表板無需額外的IT支援，也無需花費時間和精力，即可通過額外的資料倉庫設計和實施導出和處理資料。

以下介面工具集可透過其個別控制面板的介面工具集資料庫取得。 如需詳細資訊，請參閱本檔案 [如何透過介面工具集資料庫新增介面工具集](../../dashboards/customize/widget-library.md).

**新介面工具集**

| 介面工具集 | 控制面板 | 說明 |
| ------ | --------- | ----------- |
| [!UICONTROL 新增的設定檔趨勢] | 設定檔 | 此介面工具集使用折線圖來說明過去30天、90天或12個月內，每天新增至設定檔存放區的合併設定檔總數。 |
| [!UICONTROL 對應至目的地狀態的對象] | 設定檔 | 此Widget會在單一量度中顯示已對應和未對應對象的總數，並使用甜甜圈圖來說明其總數之間的比例差異。 |
| [!UICONTROL 對象大小] | 設定檔 | 此介面工具集提供兩欄的表格，列出最多20個區段，以及每個區段中包含的對象總數。 此清單取決於套用的合併原則，並根據對象總數從高到低排序。 |
| [!UICONTROL 設定檔計數趨勢] | 設定檔 | 此介面工具集使用折線圖來說明系統包含的設定檔總數在一段時間內的趨勢。 資料可在30天、90天和12個月期間內視覺化。 |
| [!UICONTROL 依身分的單一身分設定檔] | 設定檔 | 此介面工具集使用長條圖來說明僅以單一唯一識別碼識別的設定檔總數。 介面工具集最多可支援5種最常發生的身分識別。 |
| [!UICONTROL 目標狀態] | 目的地 | 此Widget會以單一量度顯示已啟用目的地的總數，並使用環圈圖來說明已啟用和已停用目的地之間的比例差異。 |
| [!UICONTROL 依目的地平台的作用中目的地] | 目的地 | 此介面工具集使用兩欄的表格，來顯示作用中目的地平台的清單以及每個目的地平台的作用中目的地總數。 |
| [!UICONTROL 所有目的地的啟用對象] | 目的地 | 此介面工具集提供在單一量度中啟用所有目的地的受眾總數。 |
| [!UICONTROL 對象啟動順序] | 區段 | 此介面工具集提供三欄的表格，列出對象的目的地名稱、平台和啟用日期。 |
| [!UICONTROL 對象大小趨勢] | 區段 | 此介面工具集提供折線圖插圖，說明在30天、90天和12個月期間內，符合任何區段定義條件的設定檔總數。 |
| [!UICONTROL 對象大小變更趨勢] | 區段 | 此介面工具集提供折線圖圖示，說明在最近的每日快照中符合指定區段資格的設定檔總數之間的差異。 趨勢分析的期間可以視覺化為30天、90天和12個月期間。 |
| [!UICONTROL 受眾規模（依身分）趨勢] | 區段 | 此介面工具集根據選取的身分類型，說明特定區段的受眾大小趨勢。 趨勢分析的期間可以視覺化為30天、90天和12個月期間。 |

**新功能** {#new-features}

| 功能 | 控制面板 | 說明 |
| ------- | --------- | ----------- |
| 孤立的設定檔區段成員資格清除 | 設定檔和授權使用 | 設定檔服務現在會每天移除剩餘的區段成員，以更精確地呈現您在系統中的設定檔。 指定設定檔的所有設定檔片段都被刪除後，就會進行此清除。 這可能會在授權使用控制面板中顯示「可定址的受眾」量度下降，也可能在設定檔控制面板中顯示「設定檔計數」量度下降，因為這些量度包含此版本之前剩餘的區段片段。 |

{style=&quot;table-layout:auto&quot;}

如需詳細資訊，請參閱本檔案 [[!DNL Profiles]](../../dashboards/guides/profiles.md), [[!DNL Destinations]](../../dashboards/guides/destinations.md)，和 [[!DNL Segments]](../../dashboards/guides/segments.md) 控制面板。

## 資料流 {#dataflows}

在Platform中，會從許多不同來源擷取資料、在系統內進行分析，並啟動至各種目的地。 Platform借由提供資料流的透明度，讓追蹤此潛在非線性資料流的程式更輕鬆。

資料流是跨平台移動資料的作業的表示。 這些資料流是在不同服務間配置的，有助於將資料從源連接器移動到目標資料集，然後由Identity Service和即時客戶配置檔案使用，最終激活到目標。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 區段控制面板 | 您現在可以使用監控控制面板來監控區段的資料流。 若要進一步了解，請參閱 [在UI中監控區段](../../dataflows/ui/monitor-segments.md) |

有關資料流的更一般資訊，請參閱 [資料流概述](../../dataflows/home.md). 若要進一步了解分段，請參閱 [細分概述](../../segmentation/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] 可讓資料工程師將資料對應、轉換及驗證至Experience Data Model(XDM)。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 支援Adobe Analytics來源 | Adobe Analytics來源現在支援資料準備功能，可讓您在建立資料流時，將Analytics報表套裝資料對應至目標XDM架構。 請參閱 [建立Analytics來源連線](../../sources/tutorials/ui/create/adobe-applications/analytics.md) 以取得更多資訊。 |
| 支援匯入現有對應規則 | 您現在可以從現有資料流導入映射規則，以加速資料流配置並限制錯誤。 請參閱 [導入現有映射規則](../../data-prep/ui/mapping.md) 以取得更多資訊。 |

如需 [!DNL Data Prep]，請參閱 [[!DNL Data Prep] 概述](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 預先建置與目的地平台的整合，可順暢地從Adobe Experience Platform啟動資料。 您可以使用目的地來針對跨通路行銷活動、電子郵件行銷活動、目標廣告和其他許多使用案例，啟用已知和未知的資料。

**新功能或更新功能**

| 功能 | 說明 |
| ----------- | ----------- |
| 進階企業目的地連接器 | 現已正式提供三個企業目標連接器： [[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md), [[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md)，和 [[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md). <br> 企業目標連接器的全面推出包含先前測試階段提供的所有功能，以及更多功能： <ul><li>新的驗證功能，包括 [Azure事件中心中的共用訪問簽名](../../destinations/catalog/cloud-storage/azure-event-hubs.md#sas-authentication) 更多 [驗證類型](../../destinations/catalog/streaming/http-destination.md#authentication-information) （持有權杖、OAuth 2）;</li><li>[回填歷史設定檔資料](../../destinations/catalog/streaming/http-destination.md#historical-data-backfill) （首次啟動時傳送符合區段資格的歷史設定檔）;</li><li>這些目的地現在支援資料流執行量度；</li><li>[其他區段中繼資料](../../destinations/catalog/streaming/http-destination.md#destination-details) 包含在資料裝載中，包括區段名稱和區段時間戳記；</li><li>支援 [靜態IP位址](/help/destinations/catalog/streaming/ip-address-allow-list.md) 適用於需要允許清單Experience Platform的客戶。</li></ul> |
| 目標資料流的上下文內警報 | 您現在可以 [訂閱警報](../../destinations/ui/alerts.md) 建立目標資料流時，要接收有關資料流運行的狀態、成功或失敗的警報消息。 您可以選擇在Experience PlatformUI或透過電子郵件接收警報。 |

### 進階企業目的地連接器的發行程式 {#release-process-enterprise-destinations}

若為Amazon Kinesis、Azure事件中樞和HTTP API目的地，在發行程式期間（從4月27日開始），您會在目的地目錄中看到先前的測試版目的地卡，以及新的一般可用(GA)目的地卡。 使用測試版目的地的客戶所設定的任何資料流，將在未來幾天內移轉至相同目的地的GA版本。 此移轉作業最終應於4月29日星期五當天結束前完成。 在這段短時間內，測試版目的地仍會持續顯示，並標示為 **已棄用**.

如果您已在測試階段中使用這些目的地，請注意下列事項：

- 若先前已測試過3個目的地中的任何一個，則不需要採取任何動作。 在測試版中設定的所有資料流都將繼續正常工作，並將遷移到GA版本。
- 如果您想從4月27日開始設定這些目的地，請使用新的GA版目的地。
- 一旦發行作業完成，標示為已過時的測試版卡片即會移除，預計在4月29日星期五當天結束前完成。 Experience Platform工程團隊正密切監控是否成功發行。

**新目的地**

| 目的地 | 說明 |
| ----------- | ----------- |
| [!DNL Criteo] | 將資料連線並啟動至 [[!DNL Criteo]](../../destinations/catalog/advertising/criteo.md) 廣告平台。 |
| [!DNL Sendgrid] | 將資料連線並啟動至 [[!DNL Sendgrid]](../../destinations/catalog/email-marketing/sendgrid.md) 交易和行銷電子郵件平台。 |

如需目的地的詳細一般資訊，請參閱 [目的地概述](../../destinations/home.md).

## Experience Data Model(XDM) {#xdm}

XDM是開放原始碼規格，可針對匯入Adobe Experience Platform的資料提供通用結構和定義（結構）。 遵循XDM標準，所有客戶體驗資料皆可整合至通用表示法，以更快速、更整合的方式提供深入分析。 您可以從客戶動作中獲得寶貴的深入分析、透過區段定義客戶受眾，以及將客戶屬性用於個人化目的。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 新增或移除結構的個別標準欄位 | 結構編輯器UI現在可讓您將標準欄位群組的部分新增至結構，為您選擇加入的欄位提供更大彈性，而無須從頭建立自訂資源。<br><br>您現在也可以直接在架構結構中定義臨機自訂欄位，並將它們指派給新的或現有的自訂欄位群組，而不需要事先建立或編輯欄位群組。<br><br>請參閱 [在UI中建立和編輯結構](../../xdm/ui/resources/schemas.md) 以取得這些新工作流程的詳細資訊。 |

{style=&quot;table-layout:auto&quot;}

**新XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 全局架構 | [[!UICONTROL 資料衛生操作請求]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | 擷取資料清除請求的詳細資訊，以刪除或修改指定資料集或沙箱中的記錄。 |
| 描述符 | [[!UICONTROL 時間序列粒度描述符]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | 指出時間序列和摘要資料的粒度。 套用至結構時，結構的 `timestamp` 欄位是此詳細程度期間中的第一個時間戳記。 |
| 類別 | [[!UICONTROL XDM摘要量度]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | 提供具有分組維的預匯總度量，如具有GROUP BY的SQL SELECT的結果。 |
| 欄位群組 | [[!UICONTROL 同意策略評估結果映射]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResults.schema.json) | 擷取個人的同意政策評估結果。 |
| 欄位群組 | [[!UICONTROL 網站搜尋]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | 擷取網站搜尋的相關資訊，例如搜尋查詢、篩選和排序。 |
| 欄位群組 | [[!UICONTROL 合併銷售機會]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | 擷取合併兩個或多個銷售機會之事件的詳細資訊。 |
| 欄位群組 | [[!UICONTROL 已傳送電子郵件]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | 擷取傳送電子郵件給收件者之事件的詳細資訊。 |
| 欄位群組 | [[!UICONTROL 匯整欄位]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | 擷取透過事件的身分拼接程式計算的值。 |
| 欄位群組 | [[!UICONTROL 審核的輔助收件人詳細資訊]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | Adobe Journey Optimizer欄位群組，可擷取稽核的次要收件者詳細資料。 |
| 欄位群組 | [[!UICONTROL XDM業務帳戶人員關係詳細資訊]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | 擷取與帳戶與人員關係相關的詳細資訊。 |
| 欄位群組 | [[!UICONTROL 帳戶人員詳細資訊]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | 擷取與帳戶與人員關係相關的詳細資訊。 |
| 資料類型 | [[!UICONTROL 購物車]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | 擷取電子商務購物車的相關資訊。 |
| 資料類型 | [[!UICONTROL 裝運]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | 擷取一或多項產品的運送資訊。 |
| 資料類型 | [[!UICONTROL 網站搜尋]](https://github.com/adobe/xdm/blob/master/components/datatypes/sitesearch.schema.json) | 擷取網站搜尋活動的相關資訊。 |
| 擴充功能(Workfront) | [[!UICONTROL 操作任務屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | 捕獲與操作任務相關的詳細資訊。 |
| 擴充功能(Workfront) | [[!UICONTROL 工作Portfolio屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | 捕獲與工作組合相關的詳細資訊。 |
| 擴充功能(Workfront) | [[!UICONTROL 工作計畫屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | 捕獲與工作程式相關的詳細資訊。 |
| 擴充功能(Workfront) | [[!UICONTROL 工作項目屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | 擷取與工作專案相關的詳細資訊。 |

{style=&quot;table-layout:auto&quot;}

**更新XDM元件**

| 元件類型 | 名稱 | 更新說明 |
| --- | --- | --- |
| 全局架構 | [[!UICONTROL 目的地]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | 新的枚舉值 `destinationCategory`. |
| 描述符 | [[!UICONTROL 友好名稱描述符]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | 新增移除建議值的支援(`meta:enum`)，而不是標準欄位中所需的。 |
| 欄位群組 | [[!UICONTROL 用戶登錄過程]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile` 欄位。 |
| 資料類型 | [[!UICONTROL 商務]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | 已新增數個購物車相關欄位。 |
| 資料類型 | [[!UICONTROL 產品清單項目]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | 為選取的選項和折扣金額新增欄位。 |
| 擴充功能(Intelligent Services) | [[!UICONTROL Intelligent Services JourneyAI傳送時間最佳化]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | 針對傳送時間分數最佳化儲存格式。 |
| 擴充功能(Workfront) | [[!UICONTROL Workfront變更事件]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | 以 `workfront:customData` 欄位。 |
| 擴充功能(Workfront) | [[!UICONTROL 工作任務屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | 新增數個欄位。 |
| 擴充功能(Workfront) | [[!UICONTROL 工作對象]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | 父對象類型和自定義表單欄位的新欄位。 |

{style=&quot;table-layout:auto&quot;}

如需Platform中XDM的詳細資訊，請參閱 [XDM系統概觀](../../xdm/home.md).

## [!DNL Artificial Intelligence/Machine Learning services] {#ai/ml-services}

AI/ML服務讓行銷分析師和從業人員能夠在客戶體驗使用案例中運用人工智慧和機器學習的強大功能。 這可讓行銷分析人員利用業務層級設定，針對公司需求設定專屬預測，而無需資料科學的專業知識。

### Attribution AI

Attribution AI 可將點數歸因到促成轉換事件的接觸點。 行銷人員可善用此工具，協助量化客戶歷程中各個獨立行銷接觸點對行銷的影響。

**更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 支援多資料集 | 「多資料集」功能現在支援所有「體驗事件」資料集，以及以身分對應形式選取「身分對應」。 只要資料集之間有共同的身分命名空間，客戶就可以選取「身分對應」和任何相關的ID。 Attribution AI支援下列結構：Adobe Analytics、體驗事件、消費者體驗事件。 如需Attribution AI中多資料集支援的詳細資訊，請參閱 [Attribution AI使用指南](../../intelligent-services/attribution-ai/user-guide.md). |

如需 [!DNL Intelligent Services]，請參閱 [[!DNL Intelligent Services] 概述](../../intelligent-services/home.md).

### Customer AI

Real-time Customer Data Platform提供的Customer AI可產生自訂傾向分數，例如大規模個別設定檔的流失和轉換。 不必將企業需求轉換為機器學習問題、挑選演算法、培訓或部署，就能達成上述目的。

**更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 支援多資料集 | 「多資料集」功能現在支援所有「體驗事件」資料集，以及以身分對應形式選取「身分對應」。 只要資料集之間有共同的身分命名空間，客戶就可以選取「身分對應」和任何相關的ID。 Customer AI支援下列結構：Adobe Analytics、體驗事件、消費者體驗事件和Adobe Audience Manager結構。 如需Customer AI中多資料集支援的詳細資訊，請參閱 [Customer AI使用手冊](../../intelligent-services/customer-ai/user-guide/configure.md). |
| Customer AI中的新模型評估量度 | Customer AI中的「新增收益」圖表可讓行銷人員根據其預算和ROI目標，決定要鎖定的群組大小。 新的提升度圖可測量模型的品質，讓您更清楚掌握其超越隨機鎖定目標的提升度。 如需詳細資訊，請參閱 [透過Customer AI探索見解](../../intelligent-services/customer-ai/user-guide/discover-insights.md) 檔案。 |

如需 [!DNL Intelligent Services]，請參閱 [[!DNL Intelligent Services] 概述](../../intelligent-services/home.md).

## Real-Time Customer Data Platform B2B 版本 {#B2B}

Real-Time CDP B2B Edition以Real-time Customer Data Platform(Real-Time CDP)為基礎，專為以企業對企業服務模式運作的行銷人員所打造。 它匯集了來自多個來源的資料，並將其結合為人員和帳戶設定檔的單一檢視。 此統一的資料可讓行銷人員精確鎖定特定對象，並參與所有可用管道中的這些對象。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 支援 `isDeleted` 功能 | 全部 [!DNL Marketo] 資料集 `Activities` 現在支援 `isDeleted` 對應。 新的對應會自動新增至您現有的B2B資料流。 您可以使用 `isDeleted` 對應以篩選已刪除的記錄，以便您的資料 [!DNL Data Lake] 與來源資料一致。 請參閱 [[!DNL Marketo] 對應欄位指南](../../sources/connectors/adobe-applications/mapping/marketo.md) 如需詳細資訊，請參閱 `isDeleted`. |

若要進一步了解Real-time Customer Data Platform B2B版，請參閱 [B2B概述](../../rtcdp/b2b-overview.md).

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 支援 [!DNL OneTrust Integration] | 您現在可以使用 [!DNL OneTrust Integration] 來源： [!DNL OneTrust] 帳戶至Platform。 請參閱 [建立 [!DNL OneTrust Integration] 源連接](../../sources/connectors/consent-and-preferences/onetrust.md) 以取得更多資訊。 |
| 支援 [!DNL Square] | 您現在可以使用 [!DNL Square] 來源：從 [!DNL Square] 帳戶至Platform。 |
| 支援刪除客戶屬性資料流 | 您現在可以刪除使用客戶屬性來源連接器建立的資料流。 |

若要進一步了解來源，請參閱 [來源概觀](../../sources/home.md).
