---
title: Adobe Experience Platform 發行說明
description: Adobe Experience Platform的最新發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 4addf64a819cd302b514334ce9cd949e96d0e698
workflow-type: tm+mt
source-wordcount: '1864'
ht-degree: 5%

---

# Adobe Experience Platform 發行說明

**發行日期：2022 年 6 月 22 日**

Adobe Experience Platform 現有功能更新：

- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations]](#destinations)
- [資料收集](#data-collection)
- [體驗資料模型(XDM)](#xdm)
- [查詢服務](#query-service)
- [來源](#sources)

## [!DNL Data Science Workspace] {#dsw}

Data Science Workspace使用機器學習和人工智慧從資料中釋放洞見。 整合到Adobe Experience Platform的Data Science Workspace可幫助您跨Adobe解決方案使用內容和資料資產進行預測。 Data Science Workspace的一種實現方法是使用JupyterLab。 JupyterLab是一個基於Web的用戶介面，用於 <a href="https://jupyter.org/" target="_blank">朱佩特工程</a> 並且緊密融入Adobe Experience Platform。 它為資料科學家提供了互動式開發環境，以便他們與Jupyter筆記本、代碼和資料一起工作。

| 功能 | 說明 |
| --- | --- |
| JupyterLab啟動程式 | JupyterLab Launcher現在包括Spark 3.2筆記型電腦的啟動器。 Spark 2.4筆記型電腦啟動器現在由Spark 3.2筆記型電腦取代，並將成為此版本的一部分。 |
| 火花3.2 | 新的Scala(Spark)和PySpark配方現在使用Spark 3.2 |
| 核 | Scala(Spark)筆記本現在通過Scala內核編寫。 PySpark筆記本現在通過Python Kernel編寫。 Spark和PySpark內核已棄用，並設定為在後續版本中刪除。 |
| 食譜 | 新的PySpark和Spark配方現在遵循與Python和R配方類似的Docker工作流。 |

{style=&quot;table-layout:auto&quot;}

有關資料科學工作區的更多一般資訊，請參見 [概述文檔](../../data-science-workspace/home.md)。

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是預先構建的與目標平台的整合，允許無縫激活來自Adobe Experience Platform的資料。 您可以使用目標來激活跨渠道市場營銷活動、電子郵件活動、目標廣告和許多其他使用案例的已知和未知資料。

**新增或更新的功能**

| 功能 | 說明 |
| ----------- | ----------- |
| (Beta)Destination SDK支援 [[!DNL Google Cloud Storage]](../../destinations/destination-sdk/server-and-file-configuration.md#gcs-example) 基於檔案的目標和 [可配置檔案名](../../destinations/destination-sdk/file-based-destination-configuration.md#file-name-configuration)。 | 現在，您可以使用該Destination SDK通過檔案名宏建立Google雲儲存目標並為導出的檔案定義自定義檔案名。 <br><br> Adobe Experience Platform Destination SDK中基於檔案的目標支援當前處於測試版中。 文檔和功能可能會更改。 |
| 資料流中的段列運行到批處理目標 | 對於向批處理目標運行的資料流，UI現在顯示與每個資料流運行關聯的段的名稱。 閱讀有關 [資料流運行到批處理目標](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations)。 |

{style=&quot;table-layout:auto&quot;&quot;

**新目標**

| 目的地 | 說明 |
| ----------- | ----------- |
| [(Beta)Google廣告經理360](../../destinations/catalog/advertising/google-ad-manager-360-connection.md) | 的 [!DNL Google Ad Manager 360] 連接啟用批處理上載 [!DNL publisher provided identifiers] (PPID)到 [!DNL Google Ad Manager 360]，通過 [!DNL Google Cloud Storage] <br><br>此目標目前為Beta版，僅對有限數量的客戶可用。 請求訪問 [!DNL Google Ad Manager 360] 連接，請與您的Adobe代表聯繫，並 [!DNL IMS Organization ID]。 |
| [[!DNL Medallia]](/help/destinations/catalog/voice/medallia-connector.md) | 激活針對Medallia調查和反饋收集的配置檔案，以便更好地瞭解客戶需求和期望。 |
| [[!DNL Adobe Advertising Cloud DSP]](../../destinations/catalog/advertising/adobe-advertising-cloud-connection.md) | Adobe Advertising Cloud [!DNL Demand-Side Platform] (DSP)目標允許您與經認證的廣告商和用戶共用經過身份驗證的第一方段，以便與他們一起激活活DSP動。 |

{style=&quot;table-layout:auto&quot;&quot;

有關目標的更多一般資訊，請參閱 [目標概述](../../destinations/home.md)。

## 資料收集 {#data-collection}

Adobe Experience Platform公司提供了一套技術，使您能夠收集客戶端客戶體驗資料並將其發送到Adobe Experience Platform邊緣網路，在該網路中，資料可以得到豐富、轉換並分發到Adobe或非Adobe目的地。

**新功能**

| 功能 | 說明 |
| --- | --- |
| [資料流的訪問類型配置](../../edge/datastreams/overview.md#create) | 建立新資料流時，現在可以選擇希望邊緣網路接受的請求類型： <ul><li>**[!UICONTROL 混合身份驗證]**:選中此選項後，邊緣網路將接受經過身份驗證的請求和未經身份驗證的請求。 當您計畫使用Web SDK或 [移動SDK](https://aep-sdks.gitbook.io/docs/)，以及 [伺服器API](../../server-api/overview.md)。 </li><li>**[!UICONTROL 僅經過身份驗證]**:選中此選項後，邊緣網路僅接受經過身份驗證的請求。 當您計畫僅使用伺服器API並希望阻止任何未經驗證的請求由 [!DNL Edge Network]。 </li></ul> |
| [呈現命題](../../edge/personalization/rendering-personalization-content.md#applypropositions) 在單頁應用程式中，不增加度量。 | 新添加的 `applyPropositions` 命令允許您呈現或執行命題陣列 [!DNL Target] 到單頁應用程式，而不增加 [!DNL Analytics] 和 [!DNL Target] 度量。 這提高了報告的準確性。 |
| [移動到Web和跨域ID共用](../../edge/identity/id-sharing.md) | Adobe Experience PlatformWeb SDK現在支援訪問者ID共用功能，使您能夠更準確地在移動應用和移動Web內容之間以及跨域提供個性化體驗。 |
| [Google資料層標籤擴展](../../tags/extensions/web/google-data-layer/overview.md) | Google資料層擴展允許您在標籤實現中使用Google資料層。 |
| [Google廣告增強轉換事件轉發擴展](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html) | Google廣告增強轉換擴展允許您即時增強Google廣告轉換。 |
| [Mailchimp事件轉發擴展](../../tags/extensions/web/mailchimp/overview.md) | Mailchimp事件轉發擴展將事件發送到Mailchimp市場營銷API，該API可觸發Mailchimp市場營銷活動、旅程或交易的電子郵件。 |

有關詳細資訊，請參閱 [資料收集概述](../../collection/home.md)。

## 體驗資料模型(XDM) {#xdm}

XDM是一種開源規範，它為傳入Adobe Experience Platform的資料提供通用結構和定義（架構）。 通過遵守XDM標準，所有客戶體驗資料都可以納入到共同的表示形式中，以更快、更整合的方式提供見解。 您可以從客戶操作中獲得有價值的見解，通過細分市場定義客戶受眾，並將客戶屬性用於個性化目的。

**新的XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 類 | [[!UICONTROL 藥物]](https://github.com/adobe/xdm/blob/master/components/classes/medication.schema.json) | 一個醫療保健行業類別，它捕獲用於醫療治療的物質的詳細資訊，尤其是藥物或藥物。 |
| 類 | [[!UICONTROL 計劃]](https://github.com/adobe/xdm/blob/master/components/classes/plan.schema.json) | 一個醫療保健行業類別，它捕獲有關醫療計畫的詳細資訊，如醫療計畫或保險計畫。 |
| 類 | [[!UICONTROL 提供程式]](https://github.com/adobe/xdm/blob/master/components/classes/provider.schema.json) | 一個醫療保健行業類別，可捕獲有關醫療保健提供商的詳細資訊。 |
| 類 | [[!UICONTROL 付款人]](https://github.com/adobe/xdm/blob/master/components/classes/payer.schema.json) | 一個醫療保健行業類別，可捕獲有關保險公司的詳細資訊。 |
| 類 | [[!UICONTROL 即時事件計畫]](https://github.com/adobe/xdm/blob/master/components/classes/live-event-schedule.json) | 一種體育和娛樂行業課程，可捕獲現場活動日程安排的詳細資訊，如巡迴音樂會日程或體育隊日程安排。 |
| 類 | [[!UICONTROL 位置]](https://github.com/adobe/xdm/blob/master/components/classes/location.json) | 一種體育和娛樂行業課程，可捕捉現場活動的位置，如音樂廳或體育場。 |
| 欄位群組 | [[!UICONTROL 一種保健藥物]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/medication/healthcare-medication.schema.json) | 的欄位組 [!UICONTROL 藥物] 類，它捕獲有關藥品的詳細資訊，如品牌名稱、批號和數量。 |
| 欄位群組 | [[!UICONTROL 醫療保健計畫詳細資訊]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/plan/healthcare-plan-details.schema.json) | 的欄位組 [!UICONTROL 計畫] 類，用於捕獲網路、類型和活動狀態等詳細資訊。 |
| 欄位群組 | [[!UICONTROL 醫療保健提供商]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json) | 的欄位組 [!UICONTROL 提供程式] 類，它捕獲個人健康專業人員或獲得提供醫療保健診斷和治療服務許可的健康設施組織的詳細資訊。 |
| 欄位群組 | [[!UICONTROL 醫療保健成員詳細資訊]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/provider/healthcare-provider-details.schema.json) | 的欄位組 [!UICONTROL XDM個人配置檔案] 類，該類捕獲擁有或將接受服務或護理的人員的詳細資訊，如聯繫資訊、初級護理醫生和規劃資訊。 |
| 欄位群組 | [[!UICONTROL 站點工具詳細資訊]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-healthcare-sitetool.schema.json) | 的欄位組 [!UICONTROL XDM體驗事件] 類，它捕獲由sitetools收集的資訊，如查看、調查等。 |
| 欄位群組 | [[!UICONTROL 即時事件票證購買]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-live-event-ticket-purchase.json) | 的欄位組 [!UICONTROL XDM體驗事件] 類，它捕獲現場活動（如音樂會或體育遊戲）門票的購買歷史記錄。 |
| 欄位群組 | [[!UICONTROL 體育和娛樂活動日程]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/live-event-schedule/sports-entertainment-event-schedule.schema.json) | 的欄位組 [!UICONTROL 即時事件計畫] 類，它捕獲有關日程安排的詳細資訊，如吸引力名稱、開門時間等。 |
| 欄位群組 | [[!UICONTROL 體育娛樂活動場]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/location/sports-entertainment-event-venue.schema.json) | 的欄位組 [!UICONTROL 位置] 類，它捕獲有關活動地點的詳細資訊，如座位容量和指定市場區域(DMA)。 |
| 全局架構 | （幾個） | RTCDP Insights的目標度量提供了新的全局架構。 請參閱以下內容 [拉式請求](https://github.com/adobe/xdm/pull/1560) 的子菜單。 |

{style=&quot;table-layout:auto&quot;&quot;

**更新的XDM元件**

| 元件類型 | 名稱 | 更新說明 |
| --- | --- | --- |
| 行為 | [[!UICONTROL 時間序列架構]](https://github.com/adobe/xdm/blob/master/components/behaviors/time-series.schema.json) | 已添加媒體狀態更新事件類型。 |
| 欄位群組 | [[!UICONTROL 住宿預訂]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/industry-verticals/experienceevent-lodging-reservation.schema.json) | 已添加住宿結帳屬性。 |
| 資料類型 | [[!UICONTROL 媒體資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/media.schema.json) | 已添加狀態啟動和狀態結束欄位。 |
| 擴充功能 | [[!UICONTROL Workfront變革事件]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/changeevent.schema.json) | 添加了兩個欄位，用於儲存屬性以幫助標識用戶和建立事件的時間。 |
| 擴充功能 | [[!UICONTROL AdobeCJM ExperienceEvent — 消息交互詳細資訊]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/message-interaction.schema.json) | 在登錄頁對象中添加訂閱、同意、自定義電子郵件和其他資料資訊。 |

{style=&quot;table-layout:auto&quot;&quot;

有關平台中XDM的詳細資訊，請參見 [XDM系統概述](../../xdm/home.md)。

## 查詢服務 {#query-service}

查詢服務允許您使用標準SQL查詢Adobe Experience Platform的資料 [!DNL Data Lake]。 您可以加入來自 [!DNL Data Lake] 並將查詢結果捕獲為新資料集，用於報告、Data Science Workspace或用於接收到即時客戶概要檔案。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 即席架構標籤 | 通過將標籤應用於通過查詢服務CTAS查詢自動生成的即席架構的資料欄位，管理對敏感資料的訪問。 您可以限制特定架構的某些欄位或資料集的使用，以控制對敏感個人資料和個人身份資訊的訪問。 通過使用基於屬性的訪問控制功能，您可以通過平台UI為ad hoc架構欄位添加標籤。 |
| `FLATTEN` 設定 | 通過第三方BI工具連接到資料庫時， `FLATTEN` 設定會將嵌套的資料結構拼合到單獨的列中，其中屬性名稱將成為保存行值的列名。 這提高了即席模式的可用性，並減少了在不支援嵌套資料結構的BI工具中檢索、分析、轉換和報告資料所需的工作量。 |

{style=&quot;table-layout:auto&quot;&quot;

有關查詢服務的詳細資訊，請參閱 [查詢服務概述](../../query-service/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，同時允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

| 功能 | 說明 |
| --- | --- |
| Beta版 [!DNL Mixpanel] 源 | 您現在可以使用 [!DNL Mixpanel] 源：從 [!DNL Mixpanel] 帳戶到Experience Platform。 查看 [[!DNL Mixpanel] 源文檔](../../sources/connectors/analytics/mixpanel.md) 的子菜單。 |

{style=&quot;table-layout:auto&quot;&quot;

要瞭解有關源的詳細資訊，請參閱 [源概述](../../sources/home.md)。
