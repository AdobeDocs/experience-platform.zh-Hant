---
title: Adobe Experience Platform 發行說明 (2022 年 4 月)
description: Adobe Experience Platform 2022 年 4 月版發行說明。
exl-id: 39233787-3089-4469-8363-b006ae41ae21
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2679'
ht-degree: 19%

---

# Adobe Experience Platform 發行說明

**發行日期： 2022年4月27日**

Adobe Experience Platform 現有功能的更新：

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai/ml-services)
- [[!DNL Dashboards]](#dashboards)
- [資料流](#dataflows)
- [[!DNL Data Prep]](#data-prep)
- [目標](#destinations)
- [體驗資料模式 (XDM)](#xdm)
- [Real-Time Customer Data Platform B2B 版本](#B2B)
- [來源](#sources)

## [!DNL Dashboards] {#dashboards}

Experience Platform提供多個控制面板，讓您檢視有關組織資料的重要資訊，這些資訊是在每日快照期間擷取的。

儀表板提供組織資料預先設定的報表選項，並直接內建在Experience Platform的行銷人員工作流程中。 這些儀表板不需要額外的IT支援，也不需要透過其他資料倉儲設計與實作匯出及處理資料所需的時間和精力。

下列Widget可透過Widget資料庫使用於其個別儀表板。 請參閱檔案以取得有關[如何透過Widget程式庫](../../dashboards/customize/widget-library.md)新增Widget的詳細資訊。

**新Widget**

| Widget | 控制面板 | 說明 |
| ------ | --------- | ----------- |
| [!UICONTROL 設定檔新增趨勢] | 輪廓 | 此Widget使用線圖來說明過去30天、90天或12個月每日新增至設定檔存放區的合併設定檔總數。 |
| [!UICONTROL 對應到目的地狀態的對象] | 輪廓 | 此Widget會顯示單一量度中已對應和未對應的對象總數，並使用環圈圖來說明總數之間的比例差異。 |
| [!UICONTROL 對象人數] | 輪廓 | 此Widget提供兩欄表格，列出最多20個區段以及每個區段中包含的對象總數。 此清單取決於根據對象總數從高到低套用和排序的合併原則。 |
| [!UICONTROL 設定檔計數趨勢] | 輪廓 | 此Widget使用線圖來說明系統中包含之設定檔總數在一段時間內的趨勢。 您可以視覺化超過30天、90天和12個月期間的資料。 |
| [!UICONTROL 依身分割槽分的單一身分設定檔] | 輪廓 | 此Widget使用長條圖來說明僅以單一唯一識別碼識別的設定檔總數。 Widget最多可支援五種最常發生的身分識別。 |
| [!UICONTROL 目的地狀態] | 目標 | 此Widget會將啟用的目的地總數顯示為單一量度，並使用環圈圖來說明啟用和停用目的地之間的比例差異。 |
| [!UICONTROL 依目的地平台區分的有效目的地] | 目標 | 此Widget使用兩欄表格來顯示作用中目的地平台的清單，以及每個目的地平台的作用中目的地總數。 |
| [!UICONTROL 所有目的地的啟用對象] | 目標 | 此Widget提供在單一量度中跨所有目的地啟用的對象總數。 |
| [!UICONTROL 對象啟用順序] | 區段 | 此Widget提供三欄表格，列出目的地名稱、平台和對象的啟用日期。 |
| [!UICONTROL 對象規模趨勢] | 區段 | 此Widget提供在30天、90天及12個月期間符合任何區段定義條件的設定檔總數的線圖插圖。 |
| [!UICONTROL 對象人數變更趨勢] | 區段 | 此Widget提供最近每日快照之間符合指定區段資格的設定檔總數差異的線圖。 趨勢分析的期間可以視覺化為30天、90天和12個月的期間。 |
| [!UICONTROL 依身分割槽分的對象人數趨勢] | 區段 | 此Widget會根據選取的身分型別，說明特定區段的對象人數趨勢。 趨勢分析的期間可以視覺化為30天、90天和12個月的期間。 |

**新功能** {#new-features}

| 功能 | 控制面板 | 說明 |
| ------- | --------- | ----------- |
| 孤立的設定檔區段會籍清理 | 設定檔與授權使用情況 | 設定檔服務現在會每天移除剩餘的區段成員，以在系統中更準確地呈現您的設定檔。 這種清理會在刪除給定設定檔的所有設定檔片段之後發生。 授權使用儀表板中的「可定址對象」量度可能會下降，而個人資料儀表板中的「個人資料計數」量度可能會下降，因為這些量度包含此版本之前的遺留區段片段。 |

{style="table-layout:auto"}

請參閱檔案以取得有關[[!DNL Profiles]](../../dashboards/guides/profiles.md)、[[!DNL Destinations]](../../dashboards/guides/destinations.md)和[[!DNL Segments]](../../dashboards/guides/audiences.md)儀表板的詳細資訊。

## 資料流 {#dataflows}

在Experience Platform中，資料會從許多不同來源擷取、在系統中分析，並啟用至各種不同的目的地。 Experience Platform透過提供資料流透明度，讓追蹤這種潛在非線性資料流的程式變得更輕鬆。

資料流可呈現跨Experience Platform行動資料的作業。 這些資料流會在不同的服務中設定，有助於將資料從來源聯結器移至目標資料集，然後由身分服務和即時客戶個人檔案使用，最後啟用至目的地。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 區段控制面板 | 您現在可以使用監視儀表板來監視區段的資料流。 若要深入瞭解，請閱讀在UI](../../dataflows/ui/monitor-audiences.md)中監視[區段的指南 |

如需資料流程的詳細一般資訊，請參閱[資料流程概觀](../../dataflows/home.md)。 若要深入瞭解細分，請參閱[細分概觀](../../segmentation/home.md)。

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep]可讓資料工程師對應、轉換及驗證與Experience Data Model (XDM)之間的資料。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 支援Adobe Analytics來源 | Adobe Analytics來源現在支援「資料準備」功能，可讓您在建立資料流時，將Analytics報表套裝資料對應至目標XDM結構描述。 如需詳細資訊，請參閱有關[建立Analytics來源連線](../../sources/tutorials/ui/create/adobe-applications/analytics.md)的教學課程。 |
| 支援匯入現有的對應規則 | 您現在可以從現有的資料流匯入對應規則，以加速資料流設定並限制錯誤。 如需詳細資訊，請參閱有關[匯入現有對應規則](../../data-prep/ui/mapping.md)的教學課程。 |

如需更多有關 [!DNL Data Prep] 的資訊，請參閱[[!DNL Data Prep] 概觀](../../data-prep/home.md)。

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是與目標平台的預先建立整合，能夠順暢啟用來自 Adobe Experience Platform 的資料。您可以使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、定向廣告和其他諸多使用案例。

**新功能或更新功能**

| 功能 | 說明 |
| ----------- | ----------- |
| 進階企業目的地聯結器 | 目前有三種企業目的地聯結器可供一般使用： [[!DNL Amazon Kinesis]](../../destinations/catalog/cloud-storage/amazon-kinesis.md)、[[!DNL Azure Event Hubs]](../../destinations/catalog/cloud-storage/azure-event-hubs.md)和[[!DNL HTTP API]](../../destinations/catalog/streaming/http-destination.md)。 <br> Enterprise Destination Connectors的一般可用性包含先前在Beta階段提供的所有功能及其他： <ul><li>新的驗證功能，包括Azure事件中樞中的[共用存取簽章](../../destinations/catalog/cloud-storage/azure-event-hubs.md#sas-authentication)以及HTTP API目的地中的更多[驗證型別](../../destinations/catalog/streaming/http-destination.md#authentication-information) （持有人權杖、OAuth 2）；</li><li>[正在回填歷史設定檔資料](../../destinations/catalog/streaming/http-destination.md#historical-data-backfill) （第一次啟動時會傳送符合區段資格的歷史設定檔）；</li><li>這些目的地現在支援資料流執行量度；</li><li>[包含在資料裝載中的其他區段中繼資料](../../destinations/catalog/streaming/http-destination.md#destination-details)，包括區段名稱和區段時間戳記；</li><li>需要將Experience Platform加入允許清單的客戶支援[靜態IP位址](/help/destinations/catalog/streaming/ip-address-allow-list.md)。</li></ul> |
| 目的地資料流程的內容中警報 | 您現在可以在建立目的地資料流時[訂閱警示](../../destinations/ui/alerts.md)，以接收有關資料流執行狀態、成功或失敗的警示訊息。 您可以選擇在Experience Platform UI中或透過電子郵件接收警報。 |

### 進階企業目的地聯結器的發行程式 {#release-process-enterprise-destinations}

對於Amazon Kinesis、Azure事件中樞和HTTP API目的地，在發行程式（從4月27日開始）期間，您會在目的地目錄中看到原Beta目的地卡片和新的一般可用(GA)目的地卡。 客戶使用Beta版目的地設定的任何資料流將在未來幾天移轉至相同目的地的GA版本。 此移轉作業應於4月29日星期五當天結束前完成。 在這段短時間內，Beta目的地會繼續顯示，並標示為&#x200B;**已棄用**。

如果您在Beta階段中利用這些目的地，請注意下列事項：

- 如果先前曾使用過Beta中的3個目的地中的任一處，則不需要採取任何動作。 所有在Beta中設定的資料流將繼續運作，並將移轉至GA版本。
- 如果您想從4月27日起設定這些目的地，請使用新版GA目的地進行設定。
- 預計在4月29日星期五當天結束時，發行作業完成後，會移除標示為已過時的Beta版卡片。 Experience Platform工程團隊會密切監控成功的發行作業。

**新目的地**

| 目標 | 說明 |
| ----------- | ----------- |
| [!DNL Criteo] | 連線並啟用資料至[[!DNL Criteo]](../../destinations/catalog/advertising/criteo.md)廣告平台。 |
| [!DNL Sendgrid] | 針對異動和行銷電子郵件，連線並啟用[[!DNL Sendgrid]](../../destinations/catalog/email-marketing/sendgrid.md)平台的資料。 |

如需有關目標的詳細一般資訊，請參閱[目標概觀](../../destinations/home.md)。

## 體驗資料模式 (XDM) {#xdm}

XDM 是一種開放原始碼的規格，可為帶到 Adobe Experience Platform 中的資料提供通用結構和定義 (結構描述)。若遵守 XDM 標準，即可將所有客戶體驗資料合併到一個常用表述中，以更快速、更整合的方式傳遞分析。您可以從客戶行為中獲得有價值的分析，透過區段定義客戶客群，並使用客戶屬性實現個人化的目的。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 新增或移除結構的個別標準欄位 | 結構描述編輯器UI現在可讓您將標準欄位群組的部分新增到結構描述，為您選擇包含的欄位提供更大的靈活性，而無需從頭開始建立自訂資源。<br><br>您現在也可以直接在結構描述結構中定義臨機操作自訂欄位，並將其指派給新的或現有的自訂欄位群組，而不需要預先建立或編輯欄位群組。<br><br>如需這些新工作流程的詳細資訊，請參閱[在UI中建立和編輯結構描述](../../xdm/ui/resources/schemas.md)的指南。 |

{style="table-layout:auto"}

**新的 XDM 元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 全域結構描述 | [[!UICONTROL 資料衛生操作要求]](https://github.com/adobe/xdm/blob/master/schemas/hygiene/aep-hygiene-ops-record.schema.json) | 擷取資料清理請求的詳細資料，以刪除或修改指定資料集或沙箱中的記錄。 |
| 描述項 | [[!UICONTROL 時間序列詳細程度描述項]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/time-series/descriptorTimeSeriesGranularity.schema.json) | 表示時間序列和摘要資料的粒度。 當套用至結構描述時，結構描述的`timestamp`欄位是此詳細程度期間中的第一個時間戳記。 |
| 類別 | [[!UICONTROL XDM摘要量度]](https://github.com/adobe/xdm/blob/master/components/classes/summary_metrics.schema.json) | 提供具有分組維度的預先摘要量度，例如具有GROUP BY的SQL SELECT的結果。 |
| 欄位群組 | [[!UICONTROL 同意原則評估結果對應]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/profile/profile-consentResults.schema.json) | 擷取個人的同意原則評估結果。 |
| 欄位群組 | [[!UICONTROL 網站搜尋]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-site-search.schema.json) | 擷取網站搜尋的相關資訊，例如，搜尋查詢、篩選和訂購。 |
| 欄位群組 | [[!UICONTROL 合併潛在客戶]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/merge-leads.schema.json) | 擷取兩個或多個潛在客戶合併之事件的詳細資訊。 |
| 欄位群組 | [[!UICONTROL 電子郵件已傳送]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/events/emailsent.schema.json) | 擷取傳送電子郵件給收件者之事件的詳細資料。 |
| 欄位群組 | [[!UICONTROL 拼接欄位]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-stitching.schema.json) | 擷取透過事件的身分拼接流程運算出的值。 |
| 欄位群組 | [[!UICONTROL 稽核的次要收件者詳細資料]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/secondary-recipient-detail.schema.json) | 擷取稽核次要收件者詳細資料的Adobe Journey Optimizer欄位群組。 |
| 欄位群組 | [[!UICONTROL XDM商業帳戶個人關係詳細資料]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | 擷取和帳戶 — 個人關係相關的細節。 |
| 欄位群組 | [[!UICONTROL 帳戶個人詳細資料]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/account-person/account-person-details.schema.json) | 擷取和帳戶 — 個人關係相關的細節。 |
| 資料類型 | [[!UICONTROL 購物車]](https://github.com/adobe/xdm/blob/master/components/datatypes/cart.schema.json) | 擷取關於電子商務購物車的資訊。 |
| 資料類型 | [[!UICONTROL 運送]](https://github.com/adobe/xdm/blob/master/components/datatypes/shipping.schema.json) | 擷取一或多個產品的送貨資訊。 |
| 資料類型 | [[!UICONTROL 網站搜尋]](https://github.com/adobe/xdm/blob/master/components/datatypes/sitesearch.schema.json) | 擷取網站搜尋活動的資訊。 |
| 擴充功能(Workfront) | [[!UICONTROL 作業工作屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/opTask.schema.json) | 擷取與作業任務相關的細節。 |
| 擴充功能(Workfront) | [[!UICONTROL 使用Portfolio屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/portfolio.schema.json) | 擷取與工作組合相關的細節。 |
| 擴充功能(Workfront) | [[!UICONTROL 工作計畫屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/program.schema.json) | 擷取與工作方案相關的細節。 |
| 擴充功能(Workfront) | [[!UICONTROL 工作專案屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/project.schema.json) | 擷取與工作專案相關的細節。 |

{style="table-layout:auto"}

**已更新的 XDM 元件**

| 元件類型 | 名稱 | 更新說明 |
| --- | --- | --- |
| 全域結構描述 | [[!UICONTROL 目的地]](https://github.com/adobe/xdm/blob/master/schemas/destinations/destination.schema.json) | `destinationCategory`的新列舉值。 |
| 描述項 | [[!UICONTROL 易記名稱描述項]](https://github.com/adobe/xdm/blob/master/schemas/descriptors/display/alternateDisplayInfo.schema.json) | 新增支援移除標準欄位不需要的建議值(`meta:enum`)。 |
| 欄位群組 | [[!UICONTROL 使用者登入程式]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-user-login-details.schema.json) | `createProfile`欄位已新增。 |
| 資料類型 | [[!UICONTROL Commerce]](https://github.com/adobe/xdm/blob/master/components/datatypes/marketing/commerce.schema.json) | 已新增多個與購物車相關的欄位。 |
| 資料類型 | [[!UICONTROL 產品清單項目]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | 針對選取的選項和折扣金額新增欄位。 |
| 擴充功能（智慧型服務） | [[!UICONTROL Intelligent Services JourneyAI傳送時間最佳化]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/intelligentServices/profile-journeyai-sendtimeoptimization.schema.json) | 針對傳送時間分數最佳化儲存格式。 |
| 擴充功能(Workfront) | [[!UICONTROL Workfront變更事件]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | 自訂表單欄位有數個欄位以`workfront:customData`欄位取代。 |
| 擴充功能(Workfront) | [[!UICONTROL 工作任務屬性]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/task.schema.json) | 新增了數個欄位。 |
| 擴充功能(Workfront) | [[!UICONTROL 工作物件]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobject.schema.json) | 父物件型別和自訂表單欄位的新欄位。 |

{style="table-layout:auto"}

如需Experience Platform中XDM的詳細資訊，請參閱[XDM系統總覽](../../xdm/home.md)。

## [!DNL Artificial Intelligence/Machine Learning services] {#ai/ml-services}

AI/ML服務可讓行銷分析師和從業人員運用客戶體驗使用案例中人工智慧和機器學習的強大功能。 這可讓行銷分析人員利用業務層級設定，針對公司需求設定專屬預測，而無需資料科學的專業知識。

### Attribution AI

Attribution AI 可將點數歸因到促成轉換事件的接觸點。行銷人員可善用此工具，協助量化客戶歷程中各個獨立行銷接觸點對行銷的影響。

**更新的功能**

| 功能 | 說明 |
| ------- | ----------- |
| 支援多個資料集 | 多資料集功能現在支援所有體驗事件資料集，以及選擇「身分對應」作為身分。 只要資料集間有共同的身分名稱空間，客戶就可以選取「身分對應」和任何相關聯的ID。 Attribution AI支援下列結構描述：Adobe Analytics、體驗事件、取用者體驗事件。 如需Attribution AI中多資料集支援的詳細資訊，請參閱[Attribution AI使用手冊](../../intelligent-services/attribution-ai/user-guide.md)。 |

如需更多有關 [!DNL Intelligent Services] 的資訊，請參閱[[!DNL Intelligent Services] 概觀](../../intelligent-services/home.md)。

### Customer AI

Real-Time Customer Data Platform中可用的Customer AI可產生自訂傾向分數，例如大規模個別設定檔的流失和轉換情形。 不必將企業需求轉換為機器學習問題、挑選演算法、訓練或部署，即可達成上述目的。

**更新的功能**

| 功能 | 說明 |
| ------- | ----------- |
| 支援多個資料集 | 多資料集功能現在支援所有體驗事件資料集，以及選擇「身分對應」作為身分。 只要資料集間有共同的身分名稱空間，客戶就可以選取「身分對應」和任何相關聯的ID。 Customer AI支援下列結構描述： Adobe Analytics、體驗事件、取用者體驗事件和Adobe Audience Manager結構描述。 如需Customer AI中多資料集支援的詳細資訊，請參閱[Customer AI使用手冊](../../intelligent-services/customer-ai/user-guide/configure.md)。 |
| Customer AI中的新模型評估量度 | Customer AI中的新收益圖可讓行銷人員根據其預算和ROI目標決定要定位的群組規模。 新的提升圖可測量模型的品質，能更清楚地瞭解隨機鎖定目標後提升的情形。 如需詳細資訊，請參閱[使用Customer AI探索深入分析](../../intelligent-services/customer-ai/user-guide/discover-insights.md)檔案。 |

如需更多有關 [!DNL Intelligent Services] 的資訊，請參閱[[!DNL Intelligent Services] 概觀](../../intelligent-services/home.md)。

## Real-Time Customer Data Platform B2B 版本 {#B2B}

在 Real-Time Customer Data Platform (Real-Time CDP) 上建置的 Real-Time CDP B2B 版本是專為採用企業對企業服務模式操作的行銷人員所建置的。它將來自多個來源的資料集中在一起，並將其合併成包含人員和帳戶輪廓的單一檢視。這種統一的資料讓行銷人員可以精確地以特定客群為目標，並在所有可用的管道中和這些客群互動。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 支援`isDeleted`功能 | 除`Activities`以外的所有[!DNL Marketo]資料集現在都支援`isDeleted`對應。 新對應會自動新增至您現有的B2B資料流。 您可以使用`isDeleted`對應來篩選掉已刪除的記錄，以便[!DNL Data Lake]中的資料與來源資料一致。 請參閱[[!DNL Marketo] 對應欄位指南](../../sources/connectors/adobe-applications/mapping/marketo.md)，瞭解`isDeleted`的詳細資訊。 |

若要進一步瞭解Real-Time Customer Data Platform B2B edition，請參閱[B2B總覽](../../rtcdp/b2b-overview.md)。

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Experience Platform服務來建構、加標籤及增強這些資料。 您可以從各種來源擷取資料，例如 Adob&#x200B;&#x200B;e 應用程式、雲端型儲存空間、協力廠商軟體和 CRM 系統。

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 支援 [!DNL OneTrust Integration] | 您現在可以使用[!DNL OneTrust Integration]來源，從您的[!DNL OneTrust]帳戶將同意和偏好設定資料擷取到Experience Platform。 如需詳細資訊，請參閱有關[建立 [!DNL OneTrust Integration] 來源連線](../../sources/connectors/consent-and-preferences/onetrust.md)的檔案。 |
| 支援 [!DNL Square] | 您現在可以使用[!DNL Square]來源，將您[!DNL Square]帳戶的付款資料擷取到Experience Platform。 |
| 支援刪除客戶屬性資料流 | 您現在可以刪除使用客戶屬性來源聯結器建立的資料流程。 |

若要深入瞭解來源，請參閱[來源概觀](../../sources/home.md)。
