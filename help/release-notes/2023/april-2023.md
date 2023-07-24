---
title: Adobe Experience Platform 發行說明 (2023 年 4 月)
description: Adobe Experience Platform 2023 年 4 月版發行說明。
exl-id: 8b8fa810-d301-43c1-98df-10d3903f3147
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '2084'
ht-degree: 100%

---

# Adobe Experience Platform 發行說明

>[!IMPORTANT]
>
>從 2023 年 5 月 15 日起，`Existing` 狀態會從區段會籍地圖中淘汰，以消除區段會籍生命週期中的冗餘。進行此變更後，區段中合格的設定檔會以 `Realized` 表示，而喪失資格的設定檔則會繼續以 `Exited` 表示。如需有關此變更的更多詳細資料，請詳閱[「Segmentation Service」一節](#segmentation)。

**發行日期：2023 年 4 月 26 日**

Adobe Experience Platform 現有功能的更新：

- [儀表板](#dashboards)
- [資料準備](#data-prep)
- [資料集合](#data-collection)
- [目的地](#destinations)
- [體驗資料模式](#xdm)
- [Real-Time Customer Data Platform](#rtcdp)
- [即時客戶設定檔](#profile)
- [Segmentation Service](#segmentation)
- [來源](#sources)

## 儀表板 {#dashboards}

Adobe Experience Platform 提供了多個儀表板，您可以透過這些儀表板檢視每日快照期間擷取的有關組織資料的重要分析。

**新功能或更新功能** {#dashboards-new-updated-features}

| 功能 | 說明 |
| --- | --- |
| 使用者定義的儀表板 | 您現在可以在您的 Widget 分析中&#x200B;**篩選歷史資料**，並使用最近的資料或自訂分析期間。如需詳細資訊，請參閱[使用者定義的儀表板指南](../../dashboards/user-defined-dashboards.md#filter-historical-data)。<br>您現在也可以&#x200B;**複製您現有的 Widget**。藉由自訂複本並編輯其屬性，您可以避免在建立新的唯一 Widget 時從頭開始重新啟動。若要了解詳細資訊，請詳閱 [Widget 複本指南](../../dashboards/user-defined-dashboards.md#duplicate-a-widget)。 |

{style="table-layout:auto"}

如需有關儀表板的詳細資訊，包括如何授予存取權限和建立自訂 Widget，請先詳閱[儀表板概觀](../../dashboards/home.md)。

## 資料準備 {#data-prep}

「資料準備」讓資料工程師可在體驗資料模式 (XDM) 之間對應、轉換和驗證資料。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 非生產沙箱中 Adob&#x200B;&#x200B;e Analytics 回填期間的更新 | 非生產沙箱中 Adob&#x200B;&#x200B;e Analytics 的回填期間已縮短至三個月。生產沙箱的回填將維持為 13 個月。此變更僅適用於新流程，不會影響現有流程。如需詳細資訊，請詳閱 [Adobe Analytics 概觀](../../sources/connectors/adobe-applications/analytics.md)。 |
| 新的對應工具功能可將 FPID 字串轉換為 ECID | 使用 `fpid_to_ecid` 功能將 FPID 字串轉換為 ECID，以用於 Experience Platform 和 Experience Cloud 應用程式。如需詳細資訊，請詳閱[「資料準備」功能指南](../../data-prep/functions.md)。 |

{style="table-layout:auto"}

如需有關「資料準備」的詳細資訊，請詳閱[「資料準備」概觀](../../data-prep/home.md)。

## 資料集合 {#data-collection}

Adobe Experience Platform 提供了一套技術，讓您可收集用戶端客戶體驗資料並將其傳送到 Adob&#x200B;&#x200B;e Experience Platform Edge Network，在其中可擴充、轉換資料並將其分送至 Adob&#x200B;&#x200B;e 或非 Adob&#x200B;&#x200B;e 目的地。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 資料流的 IP 位址模糊化 | 您現在可以在[資料流設定 UI](../../datastreams/configure.md) 中定義部分或完整的資料流層級 IP 模糊化選項。<br><br>該資料流層級 IP 模糊化設定會優先於在 Adob&#x200B;&#x200B;e Target 和 Audience Manager 中設定的任何 IP 模糊化。<br><br>傳送到 Adob&#x200B;&#x200B;e Analytics 的資料不會受資料流層級 [!UICONTROL IP 模糊化]設定的影響。Adobe Analytics 目前會接收未模糊化的 IP 位址。若要讓 Analytics 接收模糊化的 IP 位址，您必須在 Adob&#x200B;&#x200B;e Analytics 中單獨設定 IP 模糊化。此行為會在未來版本中更新。<br><br>如需有關 IP 模糊化的更多詳細資料以及如何進行設定的說明，請參閱[資料流設定文件](../../datastreams/configure.md#advanced-options)。 |
| [資料流設定覆寫](../../datastreams/overrides.md) | 您現在可以定義資料流的其他設定選項，您可將這些選項用於覆寫特定的設定，例如事件資料集、Target 屬性權杖、ID 同步容器以及 Analytics 報表套裝。<br><br>覆寫資料流設定的流程包含兩個步驟： <ol><li>首先，您必須在[資料流設定頁面](../../datastreams/configure.md)中定義您的資料流設定覆寫。</li><li>接著，您必須透過 Web SDK 命令或使用 Web SDK [標記擴充功能](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md)將覆寫傳送至 Edge Network。</li></ol> |
| OAuth JWT Secret | 此 [OAuth JWT Secret](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/secrets.html?lang=en) 可讓客戶使用 Adob&#x200B;&#x200B;e 和 Google 服務權杖支援「事件轉送」中伺服器和伺服器的互動。 |
| [!DNL Pinterest Conversions API] 擴充功能 | 此 [[!DNL Pinterest Conversions API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/pinterest/overview.html)  事件轉送擴充功能可讓您利用在 Adob&#x200B;&#x200B;e Experience Platform Edge Network 中擷取的資料並將其傳送到 [!DNL Pinterest] (使用 [!DNL Pinterest Conversions API] 並以伺服器端事件的形式)。 |

{style="table-layout:auto"}

## 目的地 {#destinations}

[!DNL Destinations] 是預先建立的和目標平台的整合，可讓來自 Adob&#x200B;&#x200B;e Experience Platform 的資料順暢啟動。您可使用目的地啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新目的地** {#new-destinations}

| 目的地 | 說明 |
| ----------- | ----------- |
| [[!DNL Salesforce Marketing Cloud Account Engagement] 連線](../../destinations/catalog/email-marketing/salesforce-marketing-cloud-account-engagement.md) | 使用 Salesforce Marketing Cloud Account Engagement (之前稱之為 Pardot) 目的地以擷取、追蹤銷售機會並對其進行評分和分級。將此目的地用於包含多個部門和決策者且需要較長銷售和決策週期的 B2B 使用案例。 |

{style="table-layout:auto"}

**新功能或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| ----------- | ----------- |
| [!DNL Custom Personalization] 和 [!DNL Adobe Commerce] 目的地的資料流監控 | <p> 您現在可以查看 [Adobe Commerce](/help/destinations/catalog/personalization/adobe-commerce.md) 的啟動量度、[自訂個人化](../../destinations/catalog/personalization/custom-personalization.md)和[具有屬性的自訂個人化](../../destinations/catalog/personalization/custom-personalization.md)連線。 </p> <p>![Adobe Commerce 影像](/help/destinations/assets/common/adobe-commerce-metrics.png "Adobe Commerce 量度"){width="100" zoomable="yes"}</p>  如需更多詳細資料，請參閱[監控目的地工作區中的資料流](../../dataflows/ui/monitor-destinations.md#monitor-dataflows-in-the-destinations-workspace)。 |
| 新的&#x200B;**[!UICONTROL 附加區段 ID 至區段名稱]**&#x200B;欄位適用於 [!DNL Google Ad Manager] 和 [!DNL Google Ad Manager 360] 目的地 | <p>現在您可讓 [[!DNL Google Ad Manager]](/help/destinations/catalog/advertising/google-ad-manager.md#parameters) 和 [[!DNL Google Ad Manager 360]](/help/destinations/catalog/advertising/google-ad-manager-360-connection.md#destination-details) 中的區段名稱包括來自 Experience Platform 的區段 ID，例如：`Segment Name (Segment ID)`。</p><p>![附加區段 ID 影像](/help/destinations/assets/common/append-segment-id-to-segment-name.png "新的附加區段 ID 至區段名稱欄位 "){width="100" zoomable="yes"}</p> |
| 已排程的對象回填 | <p>對於 [[!DNL Google Display & Video 360]](/help/destinations/catalog/advertising/google-dv360.md#specifics) 目的地，對象回填至目的地的啟動會排程在首次將區段對應至目的地連線後的 24 至 48 小時。此更新是為了回應 Google 的政策，即需等待 24 小時直到擷取資料為止，並可提高 Real-time CDP 和 [!DNL Google Display & Video 360] 之間的匹配率。</p> <p>請注意，這是僅適用於此目的地的後端設定，並且和 UI 中任何客戶可設定的排程選項不相關。</p> |

{style="table-layout:auto"}

**修正和增強功能** {#destinations-fixes-and-enhancements}

- 我們已經解決了用於檔案型目的地匯出的&#x200B;**排除的身分**&#x200B;報表量度中出現的問題。客戶依預期收到了來自已啟動的匯出的所有已匯出 ID。但是，UI 中的&#x200B;**排除的身分**&#x200B;報表量度由於錯誤地計入決不應匯出的身分，而錯誤地顯示了大量已排除的身分。(PLAT-149774)
- 我們已經解決了啟動工作流程的&#x200B;**排程**&#x200B;步驟中的問題。對於需要對應 ID 的目的地，客戶無法為新增到現有目的地連線的區段新增對應 ID。(PLAT-148808)

<!--
- We have fixed an issue with the beta SFTP destination where the port number was previously hardcoded to 22. The port is now configurable for this destination. 

-->

如需有關目的地的詳細一般資訊，請參閱[目的地概觀](../../destinations/home.md)。

## 體驗資料模式 (XDM) {#xdm}

XDM 是一種開放原始碼的規格，可為帶到 Adob&#x200B;&#x200B;e Experience Platform 中的資料提供通用結構和定義 (綱要)。若遵守 XDM 標準，即可將所有客戶體驗資料合併到一個常用表述中，以更快速、更整合的方式傳遞分析。您可以從客戶行為中獲得有價值的分析，透過區段定義客戶對象，並使用客戶屬性實現個人化的目的。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 顯示名稱切換 | 綱要編輯器現在可提供切換功能，在原始欄位名稱和人類更易於理解的顯示名稱之間進行變更。<br>![顯示名稱切換反白顯示的綱要編輯器。](../../xdm/images/ui/resources/schemas/display-name-toggle.png "綱要編輯器顯示名稱切換"){width="100" zoomable="yes"}<br>這種靈活性可提高欄位易尋性和綱要的編輯。標準欄位群組的顯示名稱由系統產生，但如有必要，也可透過 UI 自訂。若要了解詳細資訊，請閱讀[顯示名稱切換文件](https://experienceleague.adobe.com/docs/experience-platform/xdm/ui/resources/schemas.html#display-name-toggle)。 |

{style="table-layout:auto"}

**新的 XDM 元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 綱要 | [[!UICONTROL Adobe Target 分類欄位]](https://github.com/adobe/xdm/pull/1719/files) | Target 分類資料集的新 XDM 綱要包含一組中繼資料欄位，用於將 Target 活動和體驗進行分類。 |

{style="table-layout:auto"}

**已更新的 XDM 元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 欄位群組 | [[!UICONTROL Adobe 統一設定檔服務帳戶聯合擴充功能]](https://github.com/adobe/xdm/pull/1696/files) | 新增即時客戶設定檔的帳戶擴充功能欄位群組，讓使用者可在帳戶聯合上新增區段會籍。 |
| 綱要 | [[!UICONTROL 已計算的屬性系統綱要]](https://github.com/adobe/xdm/pull/1696/files) | 即時客戶設定檔所使用的已計算的屬性欄位群組已更新為系統唯讀全域綱要。 |
| 欄位群組 | 多個 | 已將幾個事件新增為[[!UICONTROL 時間序列綱要]](https://github.com/adobe/xdm/pull/1718/files)的欄位。 |
| 欄位群組 | 設定檔忠誠度詳細資料 | [已修正 ](https://github.com/adobe/xdm/pull/1717/files)`xdm:upgradeDate` 的標題，從「方案名稱」變成「升級日期」。 |
| 欄位群組 | 多個 | [[!UICONTROL 決策項目]](https://github.com/adobe/xdm/pull/1714/files)中有幾個欄位已更新，移除了雙重巢狀階層。 |

{style="table-layout:auto"}

如需有關 Platform 中 XDM 的詳細資訊，請閱讀 [XDM 系統概觀](../../xdm/home.md)。

## Real-Time Customer Data Platform

建置在 Experience Platform、Real-Time Customer Data Platform ([!DNL Real-Time CDP]) 上有助於公司匯集已知和未知的資料，以使用整個客戶歷程中的智慧型決策啟動客戶設定檔。[!DNL Real-Time CDP] 會結合多個企業資料來源以即時建立客戶設定檔。然後，根據這些設定檔建置的區段即可傳送到下游目的地，以便在所有管道和裝置上提供一對一的個人化客戶體驗。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 經過美化的 Real-Time CDP 首頁 | 此 [Real-Time CDP 首頁](https://experience.adobe.com)已經過美化，具有煥然一新的外觀和提升的效能。此主頁現在具有權限感知功能，並會顯示和您有權存取的功能相關的 Widget。如需詳細資訊，請閱讀 [Real-Time CDP 首頁儀表板概觀](../../rtcdp/home-page-dashboards.md)。 |
| 自我識別調查 | 自我識別調查是 Adob&#x200B;&#x200B;e Experience Platform UI 首頁中提供的簡短問卷。可使用此自我識別調查建置您的 Experience Platform 個人設定檔，並根據您的選擇接收訂製的準則。如需詳細資訊，請閱讀[自我識別調查概觀](../../landing/self-identification.md)。 |

如需有關 [!DNL Real-Time CDP] 的詳細資訊，請參閱 [[!DNL Real-Time CDP]  概觀](../../rtcdp/overview.md)。

## 即時客戶設定檔 {#profile}

Adobe Experience Platform 讓您能夠為客戶提供一致且相關的協調體驗，無論他們何時何地與您的品牌互動。透過即時客戶設定檔，您可查看每個個別客戶合併了多個管道的資料 (包括線上、離線、CRM 和協力廠商資料) 的整體檢視。 設定檔可讓您將客戶資料合併成統一的檢視畫面，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

**更新的功能**

| 功能 | 說明 |
| ------- | ----------- |
| 匿名設定檔資料到期 | 匿名設定檔資料到期現在正式推出！啟用後，此版本會從您的 Experience Platform 執行個體中持續移除過期的匿名設定檔。若要了解有關此功能和匿名設定檔的詳細資訊，請閱讀[匿名設定檔資料到期指南](../../profile/pseudonymous-profiles.md)。 |

{style="table-layout:auto"}

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷的一群人的標準，從而定義設定檔的特定子集。區段的基礎可能是記錄資料 (例如人口統計資訊) 或表示客戶與您的品牌互動的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 區段會籍地圖 | 作為之前在 2 月份的公告的後續措施，在 2023 年 5 月 15 日，`Existing` 狀態會從區段會籍地圖中淘汰，以消除區段會籍生命週期中的冗餘。進行此變更後，區段中合格的設定檔會以 `Realized` 表示，而喪失資格的設定檔則會繼續以 `Exited` 表示。<br/><br/>如果您正在使用[企業目的地](../../destinations/destination-types.md#streaming-profile-export) (Amazon Kinesis、Azure 事件中樞、HTTP API)，此變更可能會對您造成影響，並可能根據 `Existing` 狀態就地自動化下游流程。如果您屬於這種情況，請檢閱您的下游整合。如果您有興趣在特定時間之後識別新的合格設定檔，請考慮在您的區段會籍地圖中使用 `Realized` 狀態和 `lastQualificationTime` 的組合。如需詳細資訊，請聯絡您的 Adobe 代表。 |

{style="table-layout:auto"}

如需有關 [!DNL Segmentation Service] 的詳細資訊，請參閱[分段概觀](../../segmentation/home.md)。

## 來源 {#sources}

Adobe Experience Platform 可從外部來源擷取資料，並讓您使用 Platform 服務建構、標示和強化該資料。您可以從各種來源擷取資料，例如 Adob&#x200B;&#x200B;e 應用程式、雲端型儲存空間、協力廠商軟體和 CRM 系統。

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 用於篩選 Salesforce CRM 來源之列層級資料的 API 支援。 | 使用邏輯和比較運算子篩選 Salesforce CRM 來源的列層級資料。如需詳細資訊，請至「[使用 API 篩選來源的資料](../../sources/tutorials/api/filter.md)」詳閱指南。 |
| Shopify Streaming 推出 Beta 版 | 此 [Shopify Streaming 來源](../../sources/connectors/ecommerce/shopify-streaming.md)現在推出 Beta 版。使用 Shopify Streaming 來源將資料從您的 Shopify 合作夥伴帳戶串流至 Experience Platform。 |
| OneTrust Integration 正式推出 | 此 [OneTrust Integration 來源](../../sources/connectors/consent-and-preferences/onetrust.md)現在正式推出。使用 OneTrust Integration 來源將同意和偏好資料從您的 OneTrust Integration 帳戶帶到 Experience Platform。 |
| Oracle Service Cloud 正式推出 | 此 [Oracle Service Cloud 來源](../../sources/connectors/customer-success/oracle-service-cloud.md)現在正式推出。使用 Oracle Service Cloud 來源將您的 Oracle Service Cloud 資料帶到 Experience Platform。 |

{style="table-layout:auto"}

若要了解有關來源的詳細資訊，請閱讀[來源概觀](../../sources/home.md)。