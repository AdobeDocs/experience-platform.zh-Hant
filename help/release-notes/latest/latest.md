---
title: Adobe Experience Platform 發行說明
description: Adobe Experience Platform 2023 年 7 月的發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: d639b0830b88307b249e7da232b3f48b142ad37b
workflow-type: tm+mt
source-wordcount: '1804'
ht-degree: 58%

---

# Adobe Experience Platform 發行說明

**發行日期：2023 年 7 月 26 日**

Adobe Experience Platform 現有功能的更新：

- [目錄服務](#catalog-service)
- [資料集合](#data-collection)
- [資料準備](#data-prep)
- [目的地](#destinations)
- [查詢服務](#query-service)
- [Segmentation Service](#segmentation)
- [來源](#sources)
- [體驗資料模式 (XDM)](#xdm)

## 目錄服務 {#catalog-service}

目錄服務是Adobe Experience Platform中資料位置和譜系的記錄系統。 雖然所有內嵌至Experience Platform的資料都會以檔案和目錄的形式儲存在Data Lake中，但Catalog仍保有這些檔案和目錄的中繼資料和說明，以供查閱和監控之用。

| 功能 | 說明 |
| --- | --- |
| 資料集詳細目錄管理 | 資料集UI現在提供一系列內嵌動作，以便更妥善地管理您的資料集。 進階資料集管理可建立資料夾和標籤，並指派給資料集以進行篩選及改善可發現性，進而提高您的工作效率。 如需有關的詳細資訊，請參閱檔案 [內嵌動作](../../catalog/datasets/user-guide.md#inline-actions)，如何 [搜尋和篩選資料集](../../catalog/datasets/user-guide.md#search-and-filter)、和 [將資料集移至資料夾](../../catalog/datasets/user-guide.md#move-to-folders). |

{style="table-layout:auto"}

如需目錄服務的詳細資訊，請參閱 [目錄服務總覽](../../catalog/home.md).

## 資料集合 {#data-collection}

Adobe Experience Platform 提供了一套技術，讓您可收集用戶端客戶體驗資料並將其傳送到 Adob&#x200B;&#x200B;e Experience Platform Edge Network，在其中可擴充、轉換資料並將其分送至 Adob&#x200B;&#x200B;e 或非 Adob&#x200B;&#x200B;e 目的地。

**新功能或更新功能**

| 類型 | 功能 | 說明 |
| --- | --- | --- |
| 標記和事件轉送 | 資料集合稽核記錄 | 您現在可以在標記和事件轉送中查看執行動作的時間以及執行此動作的人員。這有助於進行產品的疑難排解、適當的控管和內部稽核活動。此稽核資料會透過內容中的滑動選單顯示，其中還會包括快速動作和資源狀態更新。此資料會在下列畫面中的標記和事件轉送 UI 中顯示：<br><ul><li>[屬性概觀](../../tags/ui/event-forwarding/overview.md#properties)</li><li>[規則](../../tags/ui/event-forwarding/overview.md#rules)</li><li>[資料元素](../../tags/ui/event-forwarding/overview.md#data-elements)</li><li>[擴充功能](../../tags/ui/event-forwarding/overview.md#extensions)</li><li>[資料庫檢閱](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-and-publish-a-library.html)</li><li>[資料庫的上一個建置和發佈時間](https://experienceleague.adobe.com/docs/platform-learn/data-collection/tags/build-and-publish-a-library.html)</li></ul> |
| 資料流 | [地理查詢](../../datastreams/configure.md#advanced-options) | 您現在可以設定資料串流的地理位置和網路查閱，以包含下列資訊： <ul><li>國家/地區</li><li>郵遞區號</li><li>州/省</li><li>DMA</li><li>城市</li><li>緯度 </li><li>經度</li><li>電信業者</li><li>網域</li><li>ISP</li></ul> 若要收集、處理和傳輸包括地理位置資訊在內的個人資料，您有責任確保已取得適用法律和法規要求的所有必要權限、同意、許可和授權。<br>您的 IP 位址模糊化選擇並不會影響衍生自 IP 位址並傳送到您設定的 Adob&#x200B;&#x200B;e 解決方案的地理位置資訊的層級。地理位址查詢必須單獨限制或停用。<br> 請參閱 [資料串流檔案](../../datastreams/configure.md#advanced-options) 以取得更多詳細資料。 |

{style="table-layout:auto"}

如需有關資料集合的詳細資訊，請詳閱[資料集合概觀](../../tags/home.md)。

## 資料準備 {#data-prep}

「資料準備」讓資料工程師可在體驗資料模式 (XDM) 之間對應、轉換和驗證資料。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 新的對應工具函數 | 在資料準備中對應物件時，現在可以使用下列函數： <ul><li>`map_get_values`</li><li>`map_has_keys`</li><li>`add_to_map`</li></ul> 如需有關這些函數的詳細資訊，請詳閱[資料準備函數指南](../../data-prep/functions.md#hierarchies---objects)。 |

{style="table-layout:auto"}

如需有關「資料準備」的詳細資訊，請詳閱[「資料準備」概觀](../../data-prep/home.md)。

## 目的地 {#destinations}

[!DNL Destinations] 是預先建立的和目標平台的整合，可讓來自 Adob&#x200B;&#x200B;e Experience Platform 的資料順暢啟動。您可使用目的地啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新目的地或更新的目的地** {#new-updated-destinations}

| 目的地 | 新增或已更新 | 說明 |
| ----------- |----------------|----------- |
| [[!DNL LiveRamp - Onboarding]](../../destinations/catalog/advertising/liveramp-onboarding.md) | 新增 | 將來自Adobe Experience Platform的身分新增至 [!DNL LiveRamp Connect] 這樣您就可以在行動裝置、開放式網頁、社交和網路等平台上 [!DNL CTV] 平台，使用 [!DNL Ramp ID] 識別碼。 |
| [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md) | 新增 | 建立與的即時輸出連線 [!DNL Azure Data Lake Storage Gen2] 以定期從Adobe Experience Platform將資料檔案匯出至您自己的儲存位置。 這個新的目的地提供增強的檔案匯出功能，並支援 [!BADGE 測試版]{type=Informative} |
| [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md) | 新增 | [!DNL Data Landing Zone] 是 [!DNL Azure Blob] 由Adobe Experience Platform布建的儲存體介面，可讓您存取安全的雲端型檔案儲存設施，以將檔案匯出至Platform。 這個新的目的地提供增強的檔案匯出功能，並支援 [!BADGE 測試版]{type=Informative} |
| [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md) | 新增 | 建立與的即時輸出連線 [!DNL Google Cloud Storage] 以定期從Adobe Experience Platform將資料檔案匯出至您自己的貯體。 這個新的目的地提供增強的檔案匯出功能，並支援 [!BADGE 測試版]{type=Informative} |
| [[!DNL Amazon S3] update](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog) | 已更新 | 透過此更新，目的地會提供增強的檔案匯出功能並支援 [!BADGE 測試版]{type=Informative} |
| [[!DNL Azure Blob] update](../../destinations/catalog/cloud-storage/azure-blob.md#changelog) | 已更新 | 透過此更新，目的地會提供增強的檔案匯出功能並支援 [!BADGE 測試版]{type=Informative} |
| [[!DNL SFTP] update](../../destinations/catalog/cloud-storage/sftp.md#changelog) | 已更新 | 透過此更新，目的地會提供增強的檔案匯出功能並支援 [!BADGE 測試版]{type=Informative} |
| [[!DNL Adobe Campaign Managed Services] 連線](../../destinations/catalog/email-marketing/adobe-campaign-managed-services.md) | 已更新 | 此 [!DNL Adobe Campaign Managed Services] 與Adobe Experience Platform的整合現在支援不同的對象同步型別。 使用「選取同步型別」控制項來決定是否應將對象匯出至Adobe Campaign，或匯出至對象及其設定檔屬性。 <br> ![新增「選取同步型別」選取器並反白顯示。](/help/release-notes/2023/assets/acms-destination-export-type.png "新增「選取同步型別」選取器並反白顯示。"){width="100" zoomable="yes"} |

{style="table-layout:auto"}

**新功能或更新的功能** {#destinations-new-updated-functionality}

上述六個雲端儲存空間目的地的更新及一般可用性版本提供下列功能：

- 其他 [檔案命名選項](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
- 可透過以下方式設定匯出檔案中的自訂檔案標題： [改善對應步驟](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
- 能夠自訂 [轉存的CSV資料檔案的格式化](/help/destinations/ui/batch-destinations-file-formatting-options.md).
- [!BADGE Beta]{type=Informative}[資料集匯出支援](/help/destinations/ui/export-datasets.md).


**修正和增強功能** {#destinations-fixes-and-enhancements}

- 我們修正了(API) SalesforceMarketing Cloud目的地的問題，其中在對應步驟中並未從Salesforce傳回所有可用的目標屬性。 現在有一個 [2000個目標屬性的上限](/help/destinations/catalog/email-marketing/salesforce-marketing-cloud-exact-target.md#mapping-considerations-example) 從Salesforce中開啟的視窗。
- 我們已修正Microsoft Dynamics 365目的地的問題。 目的地現在支援透過的區域資料路由 [區域選擇器](/help/destinations/catalog/crm/microsoft-dynamics-365.md#authenticate)，因此您可以根據貴公司在Microsoft生態系統中布建的地區，路由資料匯出。 <br> ![反白顯示新的「區域」選取器。](/help/release-notes/2023/assets/region-parameter-microsoft-dynamics-365.png "反白顯示新的「區域」選取器。"){width="100" zoomable="yes"}

如需有關目的地的詳細一般資訊，請參閱[目的地概觀](../../destinations/home.md)。

## 查詢服務 {#query-service}

查詢服務可讓您使用標準的 SQL 查詢 Adob&#x200B;&#x200B;e Experience Platform 資料湖中的資料。您可以加入任何資料湖的資料集，並將查詢結果擷取為新資料集，以用於報表、資料科學工作區或擷取至即時客戶設定檔。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 增強型查詢編輯器切換 | 增強的查詢編輯器切換可提供更好的協助工具和多主題支援。 增強的編輯器設定可讓您啟用深色或淺色主題。 如需詳細資訊，請參閱[文件](../../query-service/ui/user-guide.md#enhanced-editor-toggle)。 |
| 已計算統計資料的別名 | 您現在可以提供別名，在SQL查詢的計算統計資料中描述性地參考您的結果。 請參閱檔案，以取得有關COMPUTE STATISTICS命令的此項更新和其他更新的資訊。 如需詳細資訊，請參閱[文件](../../query-service/essential-concepts/dataset-statistics.md#alias-name)。 |

{style="table-layout:auto"}

如需有關查詢服務的詳細資訊，請參考[查詢服務概觀](../../query-service/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 可讓您將儲存在和個人 (例如客戶、潛在客戶、使用者或組織) 相關的 [!DNL Experience Platform] 中的資料分段為不同的對象。您可以透過區段定義或來自 [!DNL Real-Time Customer Profile] 資料的其他來源建立對象。這些對象會在 [!DNL Platform] 上集中設定及維護，並可透過任何 Adob&#x200B;&#x200B;e 解決方案輕鬆存取。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| Audience Portal | Audience Portal 會提供在 Adob&#x200B;&#x200B;e Experience Platform 中存取、建立和管理對象的全新瀏覽體驗。在 Audience Portal 中，您可以檢視 Platform 產生的對象和外部產生的對象；透過篩選、檔案夾和標記提高您的工作效率；建立 Platform 產生的對象；並透過 CSV 檔案匯入外部產生的對象。如需有關 Audience Portal 的詳細資訊，請詳閱 [Segmentation Service UI 指南](../../segmentation/ui/overview.md)。 |
| 對象構成 | 對象構成會提供易於使用的工作區以建置和編輯對象，使用用於表示不同動作的區塊。如需有關對象構成的詳細資訊，請詳閱[對象構成 UI 指南](../../segmentation/ui/audience-composition.md)。 |

如需有關 [!DNL Segmentation Service] 的詳細資訊，請詳閱[分段概觀](../../segmentation/home.md)。

## 來源 {#sources}

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| [!BADGE Beta]{type=Informative}[!DNL SAP Commerce] | 您現在可以使用 [[!DNL SAP Commerce]  來源](../../sources/connectors/ecommerce/sap-commerce.md)，將訂閱帳單資料從您的 [!DNL SAP Commerce] 帳戶帶到 Experience Platform。 |
| 支援 [!DNL Phoenix] | 您現在可以使用 [[!DNL Phoenix]  來源](../../sources/connectors/databases/phoenix.md)，將資料從您的 [!DNL Phoenix] 資料庫帶到 Experience Platform。 |
| [!DNL Salesforce] 和 [!DNL Salesforce Service Cloud] 的驗證更新 | 您現在可以指定 [[!DNL Salesforce]](../../sources/connectors/crm/salesforce.md) 和 [[!DNL Salesforce Service Cloud]](../../sources/connectors/customer-success/salesforce-service-cloud.md) 來源的 API 版本，以使用 Experience Platform UI 或 [!DNL Flow Service] API 驗證新帳戶。 |

{style="table-layout:auto"}

如需有關來源的詳細資訊，請詳閱[來源概觀](../../sources/home.md)。

## 體驗資料模式 (XDM) {#xdm}

XDM 是一種開放原始碼的規格，可為帶到 Adob&#x200B;&#x200B;e Experience Platform 中的資料提供通用結構和定義 (綱要)。若遵守 XDM 標準，即可將所有客戶體驗資料合併到一個常用表述中，以更快速、更整合的方式傳遞分析。您可以從客戶行為中獲得有價值的分析，透過區段定義客戶對象，並使用客戶屬性實現個人化的目的。

**新的 XDM 元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 類別 | [[!UICONTROL XDM 個別潛在客戶設定檔]](https://github.com/adobe/xdm/pull/1758/files) | 此類別可讓您從資料供應商最頂層的客戶贏取使用案例取得潛在客戶設定檔。 |
| 欄位群組 | [[!UICONTROL 擴充事件區段詳細資訊]](https://github.com/adobe/xdm/pull/1754/files) | 在事件集合時，設定檔符合資格的對象清單。 |

{style="table-layout:auto"}

**已更新的 XDM 元件**

| 元件類型 | 名稱 | 更新說明 |
| --- | --- | --- |
| 欄位群組 | [[!UICONTROL MediaAnalytics 互動的詳細資料]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 已從實驗性更新為 `stable`. |
| 欄位群組 | [[!UICONTROL 媒體互動細節]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 更新自 `stable` 至 `deprecated`. |
| 資料類型 | [[!UICONTROL 工作階段細節資訊]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 更新自 `experimental` 至 `stable`. |
| 資料類型 | [[!UICONTROL Qoe 資料細節資訊]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 更新自 `experimental` 至 `stable`. |
| 資料類型 | [[!UICONTROL 播放器狀態資料資訊]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 更新自 `experimental`至 `stable`. |
| 資料類型 | [[!UICONTROL 媒體事件資訊]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 更新自 `experimental` 至 `stable`. |
| 資料類型 | [[!UICONTROL 媒體詳細資訊]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 更新自 `experimental` 至 `stable`. |
| 資料類型 | [[!UICONTROL 錯誤細節資訊]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 更新自 `experimental` 至 `stable`. |
| 資料類型 | [[!UICONTROL 錯誤細節資訊]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 更新自 `stable` 至 `deprecated`. |
| 資料類型 | [[!UICONTROL 自訂中繼資料詳細資訊]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 更新自 `experimental` 至 `stable`. |
| 資料類型 | [[!UICONTROL 章節詳細資訊]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 更新自 `experimental` 至 `stable`. |
| 資料類型 | [[!UICONTROL 廣告Pod詳細資訊]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 更新自 `experimental` 至 `stable`. |
| 資料類型 | [[!UICONTROL 廣告細節資訊]](https://github.com/adobe/xdm/pull/1756/files) | 此 `meta:status` 更新自 `experimental` 至 `stable`. |
| 擴充功能（客戶歷程管理） | [[!UICONTROL 網域]](https://github.com/adobe/xdm/pull/1756/files) | `Domain` 欄位已新增至 [!UICONTROL AdobeCJM ExperienceEvent — 訊息設定檔詳細資料] 記錄收件者電子郵件地址的網域。 |
| 擴充功能（客戶歷程管理） | [[!UICONTROL 頻道的變體名稱]](https://github.com/adobe/xdm/pull/1753/files) | 此欄位已新增至 [!UICONTROL ajo實體欄位] 代表管道變體名稱。 |
| 擴充功能(Adobe Analytics) | [[!UICONTROL 內容值]](https://github.com/adobe/xdm/pull/1761/files) | `Context value` 已新增至 [!UICONTROL `Adobe Analytics ExperienceEvent Full Extension`]. |

{style="table-layout:auto"}

如需有關 Platform 中 XDM 的詳細資訊，請參閱 [XDM 系統概觀](../../xdm/home.md)。

