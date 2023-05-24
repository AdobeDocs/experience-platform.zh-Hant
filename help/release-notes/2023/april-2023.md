---
title: Adobe Experience Platform發行說明2023年4月
description: 2023年4月為Adobe Experience Platform發佈的說明。
exl-id: 8b8fa810-d301-43c1-98df-10d3903f3147
source-git-commit: 963fc5e31e1728a8a1a7e94bc0cc47d010347325
workflow-type: tm+mt
source-wordcount: '2084'
ht-degree: 4%

---

# Adobe Experience Platform 發行說明

>[!IMPORTANT]
>
>自2023年5月15日起， `Existing` 將從段成員關係圖中棄用狀態，以消除段成員關係生命週期中的冗餘。 此更改後，段中限定的配置檔案將表示為 `Realized` 取消資格的配置檔案將繼續作為 `Exited`。 有關此更改的詳細資訊，請閱讀 [分段服務部分](#segmentation)。

**發行日期：2023 年 4 月 26 日**

Adobe Experience Platform 現有功能更新：

- [儀表板](#dashboards)
- [資料準備](#data-prep)
- [資料彙集](#data-collection)
- [目的地](#destinations)
- [體驗資料模型](#xdm)
- [Real-Time Customer Data Platform](#rtcdp)
- [即時客戶設定檔](#profile)
- [細分服務](#segmentation)
- [來源](#sources)

## 儀表板 {#dashboards}

Adobe Experience Platform提供了多個儀表板，您可以通過這些儀表板查看有關組織資料的重要見解，如在每日快照中捕獲的。

**新增或更新的功能** {#dashboards-new-updated-features}

| 功能 | 說明 |
| --- | --- |
| 用戶定義的儀表板 | 你現在可以 **篩選歷史資料** 從小部件的透視中，使用最近的資料或自定義分析期間。 查看 [用戶定義的儀表板指南](../../dashboards/user-defined-dashboards.md#filter-historical-data) 的子菜單。<br>您現在也可以 **複製您現有的小部件**。 通過自定義複製件並編輯其屬性，可以避免在建立新的唯一構件時從頭開始重新啟動。 閱讀 [構件複製指南](../../dashboards/user-defined-dashboards.md#duplicate-a-widget) 來瞭解更多資訊。 |

{style="table-layout:auto"}

有關儀表板的詳細資訊，包括如何授予訪問權限和建立自定義小部件，請從讀取 [儀表板概述](../../dashboards/home.md)。

## 資料準備 {#data-prep}

資料準備允許資料工程師將資料映射到體驗資料模型(XDM)並驗證資料。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 非生產沙箱中Adobe Analytics回填期的更新 | 非生產砂箱中Adobe Analytics的回填期已縮短至三個月。 生產砂箱的回填量在13個月內保持不變。 此更改僅適用於新流，不會影響現有流。 有關詳細資訊，請閱讀 [Adobe Analytics概述](../../sources/connectors/adobe-applications/analytics.md)。 |
| 將FPID字串轉換為ECID的新映射器函式 | 使用 `fpid_to_ecid` 函式，用於將FPID字串轉換為ECID，以用於Experience Platform和Experience Cloud應用程式。 有關詳細資訊，請閱讀 [資料準備功能指南](../../data-prep/functions.md)。 |

{style="table-layout:auto"}

有關資料準備的詳細資訊，請閱讀 [資料準備概述](../../data-prep/home.md)。

## 資料彙集 {#data-collection}

Adobe Experience Platform公司提供了一套技術，使您能夠收集客戶端客戶體驗資料並將其發送到Adobe Experience Platform邊緣網路，在該網路中，資料可以得到豐富、轉換並分發到Adobe或非Adobe目的地。

**新增或更新的功能**

| 功能 | 說明 |
| --- | --- |
| 資料流的IP地址混淆 | 現在，您可以在 [資料流配置UI](../../edge/datastreams/configure.md)。 <br><br>資料流級別的IP混淆設定優先於在Adobe Target和Audience Manager中配置的任何IP混淆。 <br><br>發送到Adobe Analytics的資料不受資料流級別的影響 [!UICONTROL IP混淆] 的子菜單。 Adobe Analytics目前接收未混淆的IP地址。 要使Analytics接收模糊IP地址，必須在Adobe Analytics單獨配置IP模糊。 此行為將在以後的版本中更新。<br><br> 有關IP混淆的詳細資訊以及如何配置它的說明，請參見 [資料流配置文檔](../../edge/datastreams/configure.md#advanced-options)。 |
| [資料流配置覆蓋](../../edge/datastreams/overrides.md) | 現在，您可以為資料流定義其他配置選項，您可以使用這些選項覆蓋特定設定，如事件資料集、目標屬性令牌、ID同步容器和分析報告套件。 <br><br>覆蓋資料流配置是兩個步驟： <ol><li>首先，必須在 [資料流配置頁](../../edge/datastreams/configure.md)。</li><li>然後，您必須通過Web SDK命令或使用Web SDK將替代發送到邊緣網路 [標籤擴展](../../edge/extension/web-sdk-extension-configuration.md)。</li></ol> |
| OAuth JWT密碼 | 的 [OAuth JWT密碼](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=en) 允許客戶使用Adobe和Google服務令牌支援事件轉發中的伺服器到伺服器交互。 |
| [!DNL Pinterest Conversions API] 擴充功能 | 的 [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html) 事件轉發擴展允許您利用在Adobe Experience Platform邊緣網路中捕獲的資料並將其發送到 [!DNL Pinterest] 以伺服器端事件的形式使用 [!DNL Pinterest Conversions API]。 |

{style="table-layout:auto"}

## 目的地 {#destinations}

[!DNL Destinations] 是預先構建的與目標平台的整合，允許無縫激活來自Adobe Experience Platform的資料。 您可以使用目標來激活跨渠道市場營銷活動、電子郵件活動、目標廣告和許多其他使用案例的已知和未知資料。

**新目標** {#new-destinations}

| 目的地 | 說明 |
| ----------- | ----------- |
| [[!DNL Salesforce Marketing Cloud Account Engagement] 連接](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | 使用SalesforceMarketing Cloud帳戶項目（以前稱為Pardot）目標來捕獲、跟蹤、得分和級別線索。 將此目標用於涉及多個部門和決策者的B2B使用案例，這些部門和決策者需要更長的銷售和決策週期。 |

{style="table-layout:auto"}

**新增或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| ----------- | ----------- |
| 資料流監視 [!DNL Custom Personalization] 和 [!DNL Adobe Commerce] 目的地 | <p> 現在，您可以查看 [Adobe Commerce](/help/destinations/catalog/personalization/adobe-commerce.md)。 [自定義個性化](../../destinations/catalog/personalization/custom-personalization.md) 和 [具有屬性的自定義個性化](../../destinations/catalog/personalization/custom-personalization.md) 連接。 </p> <p>![Adobe Commerce影像](/help/destinations/assets/common/adobe-commerce-metrics.png "Adobe Commerce度量"){width="100" zoomable="yes"}</p>  請參閱 [監視目標工作區中的資料流](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace) 的子菜單。 |
| 新建 **[!UICONTROL 將段ID追加到段名稱]** 的 [!DNL Google Ad Manager] 和 [!DNL Google Ad Manager 360] 目的地 | <p>現在，您可以在 [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) 和 [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) 包括來自Experience Platform的段ID，如下所示： `Segment Name (Segment ID)`。</p><p>![追加段ID影像](/help/destinations/assets/common/append-segment-id-to-segment-name.png "「將段ID附加到段名稱」欄位 "){width="100" zoomable="yes"}</p> |
| 計畫的受眾回填 | <p>對於 [[!DNL Google Display & Video 360]](/help/destinations/catalog/advertising/google-dv360.md#specifics) 目的地，預定在段首次映射到目標連接後24-48小時激活對目標的回填。 此更新是為了響應Google的策略，即等待24小時，直到接收資料，並將提高即時CDP與 [!DNL Google Display & Video 360]。</p> <p>請注意，這是僅適用於此目標的後端配置，與UI中任何可由客戶配置的計畫選項無關。</p> |

{style="table-layout:auto"}

**修復和增強** {#destinations-fixes-and-enhancements}

- 我們已解決 **排除的身份** 報告基於檔案的目標導出的度量。 客戶正在按預期從激活的導出接收所有導出的ID。 然而， **排除的身份** UI中的報告度量錯誤地顯示了大量排除的標識，因為錯誤地計數了從來不應導出的標識。 (PLAT-149774)
- 我們已解決 **計畫** 的子菜單。 對於需要映射ID的目標，客戶無法為添加到現有目標連接的段添加映射ID。 (PLAT-148808)

<!--
- We have fixed an issue with the beta SFTP destination where the port number was previously hardcoded to 22. The port is now configurable for this destination. 

-->

有關目標的更多一般資訊，請參閱 [目標概述](../../destinations/home.md)。

## 體驗資料模型(XDM) {#xdm}

XDM是一種開源規範，它為傳入Adobe Experience Platform的資料提供通用結構和定義（架構）。 通過遵守XDM標準，所有客戶體驗資料都可以納入到共同的表示形式中，以更快、更整合的方式提供見解。 您可以從客戶操作中獲得有價值的見解，通過細分市場定義客戶受眾，並將客戶屬性用於個性化目的。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| 顯示名稱切換 | 架構編輯器現在提供切換功能，以在原始欄位名稱和更易人讀的顯示名稱之間進行更改。<br>![顯示名稱的架構編輯器突出顯示。](../../xdm/images/ui/resources/schemas/display-name-toggle.png "架構編輯器顯示名稱切換"){width="100" zoomable="yes"}<br>這種靈活性允許改進欄位可發現性並編輯您的架構。 標準欄位組的顯示名稱是系統生成的，但如果需要，也可以通過UI自定義。 請閱讀 [顯示名稱切換文檔](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#display-name-toggle) 來瞭解更多資訊。 |

{style="table-layout:auto"}

**新的XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 方案 | [[!UICONTROL Adobe Target分類欄位]](https://github.com/adobe/xdm/pull/1719/files) | 一種新的目標分類資料集XDM模式，包含一組元資料欄位以對目標活動和體驗進行分類。 |

{style="table-layout:auto"}

**更新的XDM元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 欄位組 | [[!UICONTROL Adobe統一配置檔案服務帳戶聯合擴展]](https://github.com/adobe/xdm/pull/1696/files) | 已為即時客戶配置檔案添加帳戶擴展欄位組，使用戶能夠在帳戶聯合中添加段成員資格。 |
| 方案 | [[!UICONTROL 計算屬性系統架構]](https://github.com/adobe/xdm/pull/1696/files) | Real-Time Customer Profile使用的「計算屬性」欄位組已更新為系統只讀全局架構。 |
| 欄位組 | 多重 | 添加多個事件作為 [[!UICONTROL 時間序列架構]](https://github.com/adobe/xdm/pull/1718/files)。 |
| 欄位組 | 配置檔案會員詳細資訊 | [已修復標題](https://github.com/adobe/xdm/pull/1717/files) 為 `xdm:upgradeDate` 從「程式名稱」到「升級日期」。 |
| 欄位組 | 多重 | 幾個欄位 [[!UICONTROL 決策項]](https://github.com/adobe/xdm/pull/1714/files) 已更新以刪除雙嵌套層次結構。 |

{style="table-layout:auto"}

有關平台中XDM的詳細資訊，請閱讀 [XDM系統概述](../../xdm/home.md)。

## Real-Time Customer Data Platform

基於Experience Platform,Real-time Customer Data Platform([!DNL Real-Time CDP])幫助公司將已知和未知資料匯集起來，在整個客戶過程中通過智慧決策激活客戶配置檔案。 [!DNL Real-Time CDP] 合併多個企業資料源以即時建立客戶配置檔案。 然後，可以將這些配置檔案構建的資料段發送到下游目的地，以便跨所有渠道和設備提供一對一的個性化客戶體驗。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 增強的Real-Time CDP首頁 | 的 [Real-Time CDP首頁](https://experience.adobe.com) 更新了外觀並改進了效能，從而增強了功能。 首頁現在具有權限意識，並將顯示與您有權訪問的功能相關的小部件。 有關詳細資訊，請閱讀 [Real-Time CDP首頁面板概述](../../rtcdp/home-page-dashboards.md)。 |
| 自我識別調查 | 自我識別調查是Adobe Experience Platform用戶介面首頁上提供的一份簡短問卷。 使用自我識別調查可以構建您的Experience Platform個人個人資料並根據您的選擇接收定製的准則。 有關詳細資訊，請閱讀 [自身身份調查概述](../../landing/self-identification.md)。 |

有關 [!DNL Real-Time CDP]，請參見 [[!DNL Real-Time CDP] 概述](../../rtcdp/overview.md)。

## 即時客戶設定檔 {#profile}

Adobe Experience Platform使您能夠為您的客戶提供協調、一致和相關的體驗，無論客戶在何處或何時與您的品牌進行交互。 使用即時客戶配置檔案，您可以看到每個客戶的整體視圖，該視圖將來自多個渠道的資料組合在一起，包括線上、離線、CRM和第三方資料。 配置檔案允許您將客戶資料整合到一個統一視圖中，為每次客戶交互提供一個可操作且時間戳記的帳戶。

**已更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 假名個人資料資料到期 | 現在通常可以使用假名配置檔案資料到期！ 一旦啟用此版本，將從您的Experience Platform實例中持續刪除過時的假名配置檔案。 要瞭解有關此功能和假名配置檔案的詳細資訊，請閱讀 [假名配置檔案資料過期指南](../../profile/pseudonymous-profiles.md)。 |

{style="table-layout:auto"}

## 分段服務 {#segmentation}

[!DNL Segmentation Service] 通過描述區分客戶群中可銷售人員組的標準來定義特定配置檔案子集。 段可以基於記錄資料（如人口統計資訊）或表示客戶與您品牌的交互的時間序列事件。

**新增或更新的功能**

| 功能 | 說明 |
| ------- | ----------- |
| 段成員資格映射 | 作為2023年2月15日之前公告的後續行動， `Existing` 將從段成員關係圖中棄用狀態，以消除段成員關係生命週期中的冗餘。 此更改後，段中限定的配置檔案將表示為 `Realized` 取消資格的配置檔案將繼續作為 `Exited`。<br/><br/> 此更改可能會影響您，如果您正在 [企業目標](../../destinations/destination-types.md#streaming-profile-export) (AmazonKinesis、Azure事件中心、 HTTP API)，並且可能已根據 `Existing` 狀態。 如果您是這樣，請查看下游整合。 如果您希望確定超過一定時間的新合格配置檔案，請考慮使用 `Realized` 狀態和 `lastQualificationTime` 在段成員關係圖中。 詳情請洽Adobe代表。 |

{style="table-layout:auto"}

有關 [!DNL Segmentation Service]，請參閱 [分段概述](../../segmentation/home.md)。

## 來源 {#sources}

Adobe Experience Platform可以從外部源接收資料，並允許您使用平台服務來構建、標籤和增強資料。 您可以從多種來源(如Adobe應用程式、基於雲的儲存、第三方軟體和您的CRM系統)接收資料。

Experience Platform提供REST風格的API和互動式UI，讓您能夠輕鬆地為各種資料提供程式設定源連接。 通過這些源連接，您可以驗證並連接到外部儲存系統和CRM服務，設定接收運行時間，並管理資料接收吞吐量。

**已更新功能**

| 功能 | 說明 |
| --- | --- |
| API支援篩選Salesforce CRM源的行級資料。 | 使用邏輯運算子和比較運算子篩選Salesforce CRM源的行級資料。 閱讀上的指南 [使用API篩選源的資料](../../sources/tutorials/api/filter.md) 的子菜單。 |
| Shopify流的Beta可用性 | 的 [Shopify流源](../../sources/connectors/ecommerce/shopify-streaming.md) 現在在beta中提供。 使用Shopify流源將資料從Shopify合作夥伴帳戶流到Experience Platform。 |
| OneTrust整合的一般可用性 | 的 [OneTrust整合源](../../sources/connectors/consent-and-preferences/onetrust.md) 現在正式啟用。 使用OneTrust整合源將OneTrust整合帳戶的同意和首選項資料帶到Experience Platform。 |
| oracle服務雲的一般可用性 | 的 [Oracle服務雲源](../../sources/connectors/customer-success/oracle-service-cloud.md) 現在正式啟用。 使用Oracle服務雲源將Oracle服務雲資料Experience Platform。 |

{style="table-layout:auto"}

要瞭解有關源的詳細資訊，請閱讀 [源概述](../../sources/home.md)。