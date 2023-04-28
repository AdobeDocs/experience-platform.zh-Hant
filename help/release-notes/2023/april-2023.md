---
title: Adobe Experience Platform發行說明2023年4月
description: 2023年4月Adobe Experience Platform發行說明。
exl-id: 8b8fa810-d301-43c1-98df-10d3903f3147
source-git-commit: 3594b20ee495dadf91d745958eac1a06647cae24
workflow-type: tm+mt
source-wordcount: '1662'
ht-degree: 4%

---

# Adobe Experience Platform 發行說明

**發行日期：2023 年 4 月 26 日**

Adobe Experience Platform 現有功能更新：

- [儀表板](#dashboards)
- [資料準備](#data-prep)
- [資料彙集](#data-collection)
- [目的地](#destinations)
- [體驗資料模型](#xdm)
- [即時客戶設定檔](#profile)
- [來源](#sources)

## 儀表板 {#dashboards}

Adobe Experience Platform提供多個控制面板，讓您透過這些控制面板檢視組織資料的重要深入分析（在每日快照中擷取）。

**新功能或更新功能** {#dashboards-new-updated-features}

| 功能 | 說明 |
| --- | --- |
| 使用者定義的控制面板 | 您現在可以 **篩選歷史資料** 從介面工具集分析，並使用最近的資料或自訂分析時段。 請參閱 [使用者定義的控制面板指南](../../dashboards/user-defined-dashboards.md#filter-historical-data) 以取得更多資訊。<br>您現在也可以 **複製現有小工具**. 透過自訂復本並編輯其屬性，您可以避免在建立新、獨特的Widget時從頭重新啟動。 閱讀 [widget複製指南](../../dashboards/user-defined-dashboards.md#duplicate-a-widget) 了解更多。 |

{style="table-layout:auto"}

如需控制面板的詳細資訊，包括如何授與存取權限和建立自訂Widget，請從閱讀 [控制面板概觀](../../dashboards/home.md).

## 資料準備 {#data-prep}

資料準備可讓資料工程師將資料對應、轉換及驗證至Experience Data Model(XDM)。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 更新非生產沙箱中Adobe Analytics的回填期間 | 非生產沙箱中Adobe Analytics的回填期已縮短至三個月。 生產沙箱的回填在13個月內保持不變。 此變更僅適用於新流，不會影響現有流。 如需詳細資訊，請閱讀 [Adobe Analytics概述](../../sources/connectors/adobe-applications/analytics.md). |
| 新的映射程式函式，可將FPID字串轉換為ECID | 使用 `fpid_to_ecid` 函式將FPID字串轉換為ECID，以用於Experience Platform和Experience Cloud應用程式。 如需詳細資訊，請閱讀 [資料準備功能指南](../../data-prep/functions.md). |

{style="table-layout:auto"}

有關資料準備的詳細資訊，請閱讀 [資料準備概述](../../data-prep/home.md).

## 資料彙集 {#data-collection}

Adobe Experience Platform提供一套技術，可讓您收集用戶端客戶體驗資料，並傳送至Adobe Experience Platform Edge Network，以便在中加以擴充、轉換及分發至Adobe或非Adobe目的地。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 資料流的IP位址模糊化 | 您現在可以在 [資料流配置UI](../../edge/datastreams/configure.md). <br><br>資料流層級IP模糊化設定優先於Adobe Target和Audience Manager中設定的任何IP模糊化。 <br><br>傳送至Adobe Analytics的資料不受資料流層級影響 [!UICONTROL IP模糊化] 設定。 Adobe Analytics目前會收到未經過模糊處理的IP位址。 若要讓Analytics接收模糊化的IP位址，您必須在Adobe Analytics中個別設定IP模糊化。 未來發行版本將更新此行為。<br><br> 如需IP模糊化的詳細資訊以及如何設定的指示，請參閱 [datastream配置檔案](../../edge/datastreams/configure.md#advanced-options). |
| [資料流配置覆蓋](../../edge/datastreams/overrides.md) | 您現在可以定義資料流的其他設定選項，以便用來覆寫特定設定，例如事件資料集、Target屬性Token、ID同步容器和Analytics報表套裝。 <br><br>覆寫資料流設定是兩個步驟： <ol><li>首先，您必須在 [datastream配置頁](../../edge/datastreams/configure.md).</li><li>然後，您必須透過Web SDK命令或使用Web SDK將覆寫傳送至邊緣網路 [標籤擴充功能](../../edge/extension/web-sdk-extension-configuration.md).</li></ol> |
| OAuth JWT密碼 | 此 [OAuth JWT密碼](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=en) 可讓客戶使用Adobe和Google服務代號，以支援事件轉送中的伺服器對伺服器互動。 |
| [!DNL Pinterest Conversions API] 擴充功能 | 此 [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) 事件轉送擴充功能可讓您運用Adobe Experience Platform邊緣網路中擷取的資料，並將其傳送至 [!DNL Pinterest] 以伺服器端事件的形式，使用 [!DNL Pinterest Conversions API]. |

{style="table-layout:auto"}

## 目的地 {#destinations}

[!DNL Destinations] 預先建置與目的地平台的整合，可順暢地從Adobe Experience Platform啟動資料。 您可以使用目的地來針對跨通路行銷活動、電子郵件行銷活動、目標廣告和其他許多使用案例，啟用已知和未知的資料。

**新目的地** {#new-destinations}

| 目的地 | 說明 |
| ----------- | ----------- |
| [[!DNL Salesforce Marketing Cloud Account Engagement] 連接](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | 使用SalesforceMarketing Cloud帳戶參與（舊稱Pardot）目的地來擷取、追蹤、分數和等級銷售機會。 此目的地可用於涉及多個部門和決策者（需要較長的銷售和決策週期）的B2B使用案例。 |

{style="table-layout:auto"}

**新功能或更新功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| ----------- | ----------- |
| 資料流監視 [!DNL Custom Personalization] 和 [!DNL Adobe Commerce] 目的地 | <p> 您現在可以看到 [Adobe Commerce](/help/destinations/catalog/personalization/adobe-commerce.md), [自訂個人化](../../destinations/catalog/personalization/custom-personalization.md) 和 [使用屬性的自訂個人化](../../destinations/catalog/personalization/custom-personalization.md) 連線。 </p> <p>![Adobe Commerce影像](/help/destinations/assets/common/adobe-commerce-metrics.png "Adobe Commerce量度"){width="100" zoomable="yes"}</p>  請參閱 [監視目標工作區中的資料流](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace) 以取得更多詳細資訊。 |
| 新增 **[!UICONTROL 將區段ID附加至區段名稱]** 欄位 [!DNL Google Ad Manager] 和 [!DNL Google Ad Manager 360] 目的地 | <p>您現在可以在 [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) 和 [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) 包括來自Experience Platform的區段ID，如下所示： `Segment Name (Segment ID)`.</p><p>![附加區段ID影像](/help/destinations/assets/common/append-segment-id-to-segment-name.png "新增在區段名稱欄位中附加區段ID "){width="100" zoomable="yes"}</p> |
| 排程對象回填 | <p>若 [[!DNL Google Display & Video 360]](/help/destinations/catalog/advertising/google-dv360.md#specifics) 目的地時，系統會排程在區段首次對應至目的地連線後24到48小時，啟用回填至目的地的對象。 此更新是針對Google的政策，即等候24小時，直到擷取資料，並將改善即時CDP與 [!DNL Google Display & Video 360].</p> <p>請注意，這是僅適用於此目的地的後端設定，且與UI中任何客戶可設定的排程選項無關。</p> |

{style="table-layout:auto"}

**修正和增強功能** {#destinations-fixes-and-enhancements}

- 我們已修正 **已排除的身分** 檔案型目的地匯出的報表量度。 客戶會如預期般從啟動的匯出接收所有匯出的ID。 不過， **已排除的身分** UI中的報表量度因為錯誤地計算原本不應匯出的身分，而不正確地顯示大量已排除的身分。 (PLAT-149774)
- 我們已修正 **排程** 啟動工作流程的步驟。 對於需要對應ID的目的地，客戶無法為新增至現有目的地連線的區段新增對應ID。 (PLAT-148808)

<!--
- We have fixed an issue with the beta SFTP destination where the port number was previously hardcoded to 22. The port is now configurable for this destination. 

-->

如需目的地的詳細一般資訊，請參閱 [目的地概述](../../destinations/home.md).

## Experience Data Model(XDM) {#xdm}

XDM是開放原始碼規格，可針對匯入Adobe Experience Platform的資料提供通用結構和定義（結構）。 遵循XDM標準，所有客戶體驗資料皆可整合至通用表示法，以更快速、更整合的方式提供深入分析。 您可以從客戶動作中獲得寶貴的深入分析、透過區段定義客戶受眾，以及將客戶屬性用於個人化目的。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| 顯示名稱切換 | 結構編輯器現在提供切換按鈕，讓您在原始欄位名稱和更容易閱讀的顯示名稱之間進行變更。<br>![以顯示名稱顯示的結構編輯器會切換醒目提示。](../../xdm/images/ui/resources/schemas/display-name-toggle.png "結構編輯器顯示名稱切換"){width="100" zoomable="yes"}<br>此彈性可改善欄位探索能力，以及編輯結構。 標準欄位群組的顯示名稱是系統產生的，但如有需要，也可透過UI自訂。 請閱讀 [顯示名稱切換檔案](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#display-name-toggle) 了解更多。 |

{style="table-layout:auto"}

**新XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 方案 | [[!UICONTROL Adobe Target分類欄位]](https://github.com/adobe/xdm/pull/1719/files) | Target分類資料集的新XDM結構，包含一組可分類Target活動和體驗的中繼資料欄位。 |

{style="table-layout:auto"}

**更新XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 欄位組 | [[!UICONTROL Adobe統一配置檔案服務帳戶聯合擴展]](https://github.com/adobe/xdm/pull/1696/files) | 為「即時客戶設定檔」新增帳戶擴充欄位群組，讓使用者能在「帳戶聯合」中新增區段成員資格。 |
| 方案 | [[!UICONTROL 計算屬性系統架構]](https://github.com/adobe/xdm/pull/1696/files) | 「即時客戶設定檔」使用的「計算屬性」欄位群組已更新為系統唯讀全域架構。 |
| 欄位組 | 多個 | 新增數個事件作為 [[!UICONTROL 時間序列結構]](https://github.com/adobe/xdm/pull/1718/files). |
| 欄位組 | 設定檔忠誠度詳細資料 | [修正標題](https://github.com/adobe/xdm/pull/1717/files) for `xdm:upgradeDate` 從「計畫名稱」到「升級日期」。 |
| 欄位組 | 多個 | 多個欄位來自 [[!UICONTROL 決策項目]](https://github.com/adobe/xdm/pull/1714/files) 已更新，以移除雙重巢狀階層。 |

{style="table-layout:auto"}

如需Platform中XDM的詳細資訊，請參閱 [XDM系統概觀](../../xdm/home.md).

## 即時客戶設定檔 {#profile}

Adobe Experience Platform可讓您為客戶提供協調、一致且相關的體驗，無論客戶在何處或何時與您的品牌互動。 透過即時客戶個人檔案，您可以全面了解各個客戶，其中結合來自多個管道的資料，包括線上、離線、CRM和第三方資料。 設定檔可讓您將客戶資料併入統一檢視中，提供每個客戶互動的可操作、時間戳記帳戶。

**更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 假名的設定檔資料過期 | 現在正式提供匿名的設定檔資料過期！ 啟用後，此版本會持續從您的Experience Platform例項移除過時的匿名設定檔。 若要進一步了解此功能和假名的設定檔，請閱讀 [假名描述檔資料過期指南](../../profile/pseudonymous-profiles.md). |

{style="table-layout:auto"}

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，並可讓您使用Platform服務來建構、加標籤及增強該資料。 您可以內嵌來自各種來源的資料，例如Adobe應用程式、雲端儲存、協力廠商軟體和您的CRM系統。

Experience Platform提供RESTful API和互動式UI，讓您輕鬆為各種資料提供者設定來源連線。 這些源連接允許您驗證並連接到外部儲存系統和CRM服務、設定獲取運行時間以及管理資料獲取吞吐量。

**更新功能**

| 功能 | 說明 |
| --- | --- |
| API支援篩選Microsoft Dynamics、Salesforce CRM和SalesforceMarketing Cloud的列層級資料 | 使用邏輯和比較運算子來篩選Microsoft Dynamics、Salesforce CRM和SalesforceMarketing Cloud來源的列層級資料。 閱讀指南 [使用API篩選來源的資料](../../sources/tutorials/api/filter.md) 以取得更多資訊。 |
| Shopify串流測試版可用性 | 此 [Shopify流源](../../sources/connectors/ecommerce/shopify-streaming.md) 現已提供測試版。 使用Shopify串流來源，將資料從Shopify合作夥伴帳戶串流到Experience Platform。 |
| OneTrust整合的全面推出 | 此 [OneTrust整合源](../../sources/connectors/consent-and-preferences/onetrust.md) 現已正式啟用。 使用OneTrust整合源將OneTrust整合帳戶中的同意和首選項資料帶入Experience Platform。 |
| oracle服務雲端正式發行 | 此 [Oracle服務雲端來源](../../sources/connectors/customer-success/oracle-service-cloud.md) 現已正式啟用。 使用Oracle服務雲端來源將Oracle服務雲端資料帶入Experience Platform。 |

{style="table-layout:auto"}

若要進一步了解來源，請閱讀 [來源概觀](../../sources/home.md).
