---
title: Adobe Experience Platform 發行說明 (2022 年 8 月)
description: Adobe Experience Platform 2022 年 8 月版發行說明。
exl-id: dbf1e7a3-8599-4991-8932-f57d3b1c640d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2012'
ht-degree: 26%

---

# Adobe Experience Platform 發行說明

**發行日期： 2022年8月24日**

Adobe Experience Platform 現有功能的更新：

- [[!DNL Artificial Intelligence and Machine Learning Services]](#ai-and-ml-services)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [體驗資料模式 (XDM)](#xdm)
- [即時客戶輪廓](#profile)
- [Segmentation Service](#segmentation)
- [來源](#sources)

## [!DNL Artificial Intelligence/Machine Learning services] {#ai-and-ml-services}

AI/ML服務可讓行銷分析師和從業人員運用客戶體驗使用案例中人工智慧和機器學習的強大功能。 這可讓行銷分析人員使用業務層級設定，針對公司需求設定模型，而不需要資料科學的專業知識。

### Attribution AI

Attribution AI 可將點數歸因到促成轉換事件的接觸點。行銷人員可善用此工具，協助量化客戶歷程中各個獨立行銷接觸點對行銷的影響。

**更新的功能**

| 功能 | 說明 |
| ------- | ----------- |
| 隱私權支援 | <ul><li> Attribution AI現在支援定義使用者角色和存取原則，以管理產品應用程式內功能和物件的[許可權](../../../help/access-control/abac/ui/permissions.md)。 </li><li>活動發生時，會自動記錄稽核記錄資源。</li><li> 透過[以屬性為基礎的存取控制](../../access-control/abac/overview.md)，管理員可以控制特定物件及/或特定屬性的權能，這些屬性可以是新增至物件的中繼資料，例如標籤。管理員也可以定義使用者角色，這些角色只能存取特定欄位，以及對應至這些欄位的資料。</li><li>Attribution AI會利用Experience Platform資料集。 為支援品牌可能收到的消費者權利請求，品牌應使用Experience Platform Privacy Service提交消費者存取和刪除請求，以透過Data Lake、Identity Service和即時客戶設定檔移除其資料。  </li><li>所有用於模型輸入/輸出的資料集都將遵循Experience Platform准則。 Experience Platform資料加密適用於待命和傳輸中的資料。 請參閱檔案以進一步瞭解[資料加密](../../../help/landing/governance-privacy-security/encryption.md)。</li></ul> |

{style="table-layout:auto"}

**注意**：在進一步通知之前，Attribution AI不可供現有的Healthcare Shield客戶使用。

如需Attribution AI的詳細資訊，請參閱[Attribution AI](../../intelligent-services/attribution-ai/overview.md)總覽。

### Customer AI

Real-Time Customer Data Platform中可用的Customer AI可產生自訂傾向分數，例如大規模個別設定檔的流失和轉換情形。

**更新的功能**

| 功能 | 說明 |
| ------- | ----------- |
| 隱私權支援 | <ul><li> Customer AI現在支援定義使用者角色和存取原則，以管理產品應用程式內功能和物件的[許可權](../../../help/access-control/abac/ui/permissions.md)。 </li><li>活動發生時，會自動記錄稽核記錄資源。</li><li> 透過[以屬性為基礎的存取控制](../../access-control/abac/overview.md)，管理員可以根據特定屬性控制特定物件和/或權能的存取。 這些屬性可以是新增至物件的中繼資料，例如標籤。 管理員也可以定義只有對應至特定欄位和資料之存取權的使用者角色。</li><li>Customer AI會利用Experience Platform資料集。 為支援品牌可能收到的消費者權利請求，品牌應使用Experience Platform Privacy Service提交消費者存取和刪除請求，以透過Data Lake、Identity Service和即時客戶設定檔移除其資料。 </li><li>所有用於模型輸入/輸出的資料集都將遵循Experience Platform准則。 Experience Platform資料加密適用於待命和傳輸中的資料。 請參閱檔案以進一步瞭解[資料加密](../../../help/landing/governance-privacy-security/encryption.md)。</li></ul> |

{style="table-layout:auto"}

**注意**：在進一步通知之前，現有Healthcare Shield客戶將無法使用Customer AI。

如需Customer AI的詳細資訊，請參閱[Customer AI](../../intelligent-services/customer-ai/overview.md)概述。

## [!DNL Dashboards] {#dashboards}

Adobe Experience Platform提供多個[!DNL dashboards]，您可以透過它們檢視有關您組織資料的重要深入分析，如每日快照期間所擷取。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 排定的啟用Widget | [!UICONTROL 已排程的啟用] Widget提供最近啟用的目的地的表格化檢視。 每個區段都包含名稱、目的地平台，以及啟動開始和結束日期。 此Widget可讓您一目瞭然地發現正在啟用對象的位置和時間，並讓重複或不必要的啟用更加透明。 此累積資訊也會反白標示任何啟用被遺漏的位置。 |

如需更多有關 [!DNL Dashboards] 的資訊，請參閱[[!DNL Dashboards] 概觀](../../dashboards/home.md)。

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep]可讓資料工程師對應、轉換及驗證與Experience Data Model (XDM)之間的資料。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 支援擷取含有警告的記錄 | 「資料準備」現在會將警告（非嚴重錯誤）當地語系化至欄位，並允許擷取列的其餘部分。 現在，所有對應程式轉換錯誤都會回報為警告，而部分擷取的列會被視為成功，但有警告。  含有警告和診斷詳細資訊的記錄也支援監視。 含有警告的記錄部分擷取目前僅適用於串流資料。 如需詳細資訊，請檢閱有關[擷取含有警告的記錄](../../sources/tutorials/ui/monitor-streaming.md)的檔案。 |

{style="table-layout:auto"}

若要深入瞭解[!DNL Data Prep]，請參閱[[!DNL Data Prep] 概觀](../../data-prep/home.md)。

## [!DNL Destinations] {#destinations}

[!DNL Destinations] 是與目標平台的預先建立整合，能夠順暢啟用來自 Adobe Experience Platform 的資料。您可以使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、定向廣告和其他諸多使用案例。

**新功能或更新功能**

| 功能 | 說明 |
| ----------- | ----------- |
| (Beta)個人化目的地的屬性式個人化支援 | 隨著屬性型個人化的測試版發行，您會在[目的地目錄](../../destinations/catalog/overview.md)中看到兩張新卡片： <ul><li>**[!UICONTROL Adobe Target V2]**：此聯結器目前為測試版，僅供特定數量的客戶使用。 除了Adobe Target V1卡片所提供的功能之外，Target V2聯結器還將[對應步驟](/help/destinations/ui/activate-edge-personalization-destinations.md#map-attributes)新增至啟用工作流程，可讓您將設定檔屬性對應至Adobe Target，進而啟用屬性式相同頁面和下一頁個人化。</li><li>**[!UICONTROL 具有屬性的自訂Personalization]**：此聯結器目前為測試版，僅供特定數量的客戶使用。 除了&#x200B;**[!UICONTROL 自訂Personalization]**&#x200B;所提供的功能之外，**[!UICONTROL 具有屬性的自訂Personalization]**&#x200B;聯結器還新增了選用的[對應步驟](../../destinations/ui/activate-edge-personalization-destinations.md#map-attributes)至啟動工作流程，可讓您將設定檔屬性對應至您的自訂個人化目的地，以啟用基於屬性的相同頁面和下一頁個人化。</li></ul> <br>設定檔屬性可能包含敏感資料。 為了保護此資料，**[!UICONTROL 具有屬性的自訂Personalization]**&#x200B;目的地需要您使用[Edge Network伺服器API](../../server-api/overview.md)進行資料收集。 此外，所有伺服器API呼叫都必須在[已驗證的內容](../../server-api/authentication.md)中進行。 |

{style="table-layout:auto"}

**新目的地**

| 目標 | 說明 |
| ----------- | ----------- |
| [[!DNL Outreach]](../..//destinations/catalog/crm/outreach.md) | [[!DNL Outreach]](https://www.outreach.io/)是Sales Execution Experience Platform，擁有全球最豐富的B2B買賣雙方互動資料，並在專有AI技術方面投入巨資，以將銷售資料轉換為智慧。 [!DNL Outreach]可協助組織自動化銷售參與度，並依據收入情報採取行動，以改善其效率、可預測性及成長。 |

{style="table-layout:auto"}

如需有關目標的詳細一般資訊，請參閱[目標概觀](../../destinations/home.md)。

## 體驗資料模式 (XDM) {#xdm}

XDM 是一種開放原始碼的規格，可為帶到 Adobe Experience Platform 中的資料提供通用結構和定義 (結構描述)。若遵守 XDM 標準，即可將所有客戶體驗資料合併到一個常用表述中，以更快速、更整合的方式傳遞分析。您可以從客戶行為中獲得有價值的分析，透過區段定義客戶客群，並使用客戶屬性實現個人化的目的。

**新的 XDM 元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 類別 | [[!UICONTROL AJO實體類別]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/customerJourneyManagement/ajo-entity-class.schema.json) | 以記錄為基礎的類別，可建立Adobe Journey Optimizer的查詢結構。 |
| 欄位群組 | [[!UICONTROL Workfront工作物件]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/workfront/workobjects-all.schema.json) | 參考Adobe Workfront所有較低層級物件特定欄位群組的包裝函式欄位群組。 |

{style="table-layout:auto"}

**已更新的 XDM 元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 欄位群組 | [[!UICONTROL Journey Orchestration步驟事件通用欄位]](https://github.com/adobe/xdm/blob/master/extensions/adobe/experience/journeyOrchestration/stepEvents/journeyStepEventCommonFieldsMixin.schema.json) | 已新增兩個新屬性： `origTimeStamp`和`experienceID`。 |
| 欄位群組 | [[!UICONTROL 區段會籍詳細資料]](https://github.com/adobe/xdm/blob/master/components/fieldgroups/shared/segmentation.schema.json) | 除了[!UICONTROL XDM個人設定檔]之外，此欄位群組現在也可用於根據XDM商業帳戶類別的結構描述。 |
| 欄位群組 | (多個) | 與Marketo B2B活動相關的數個欄位群組已更新為穩定狀態。 如需詳細資訊，請參閱下列[提取要求](https://github.com/adobe/xdm/pull/1593/files)。 |
| 欄位群組 | (多個) | 已更新數個與天氣相關的欄位群組，以修正`uvIndex`和`sunsetTime`發生的錯誤。 如需詳細資訊，請參閱下列[提取要求](https://github.com/adobe/xdm/pull/1602/files)。 |
| 資料類型 | [[!UICONTROL 產品清單項目]](https://github.com/adobe/xdm/blob/master/components/datatypes/productlistitem.schema.json) | 已新增屬性`productImageUrl`。 |
| 資料類型 | [[!UICONTROL Qoe 資料細節資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/qoedatadetails.schema.json) | 已新增屬性`framesPerSecond`。 |
| 資料類型 | [[!UICONTROL 工作階段細節資訊]](https://github.com/adobe/xdm/blob/master/components/datatypes/sessiondetails.schema.json) | `sdkVersion` 已重新命名為 `appVersion`。`meta:enum`及`description`欄位也已更新。 |
| 資料型別和欄位群組 | (多個) | 數個媒體資料型別和欄位群組有新欄位和更新的說明。 如需詳細資訊，請參閱下列[提取要求](https://github.com/adobe/xdm/pull/1582/files)。 |
| （全部） | (多個) | 包含`enum`欄位的所有結構描述物件現在也包含對應的`meta:enum`欄位，以表示每個條件約束的顯示值。 如需詳細資訊，請參閱下列[提取要求](https://github.com/adobe/xdm/pull/1601/files)。 |

{style="table-layout:auto"}

如需Experience Platform中XDM的詳細資訊，請參閱[XDM系統總覽](../../xdm/home.md)。

## 即時客戶輪廓 {#profile}

Adobe Experience Platform 讓您能夠為客戶提供一致且相關的協調體驗，無論他們何時何地與您的品牌互動。透過即時客戶輪廓，您可查看每個個別客戶合併了多個管道的資料 (包括線上、離線、CRM 和協力廠商資料) 的整體檢視。 輪廓可讓您將客戶資料合併成統一的檢視畫面，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

| 功能 | 說明 |
| ------- | ----------- |
| 合併原則硬性限制 | Experience Platform現在會強制每個沙箱硬性限制&#x200B;**5個**&#x200B;合併原則。 如果您的沙箱目前有超過五個合併原則，在沙箱有少於五個合併原則之前，您將&#x200B;**無法**&#x200B;建立新的合併原則。 |
| 孤立的設定檔邊緣屬性清理 | 對於所有組織，設定檔服務現在會每天移除使用者活動區域的剩餘邊緣屬性，以在系統中更準確地呈現您的設定檔。 此清理會在特定設定檔的所有設定檔片段刪除後發生，而且應該會影響從`com_adobe_aep_profile_region_dataset`標示為`true`的資料集中合併的設定檔。 授權使用儀表板中的「可定址的受眾」量度可能會下降，而個人資料儀表板中的「個人資料計數」量度可能會下降，因為這些量度包含此版本之前的剩餘邊緣屬性片段。 |

{style="table-layout:auto"}

若要了解有關即時客戶輪廓的詳細資訊，包括使用輪廓資料的教學課程和最佳做法，請從閱讀[即時客戶輪廓概觀](../../profile/home.md)開始。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷的一群人的標準，從而定義輪廓的特定子集。區段的基礎可能是記錄資料 (例如人口統計資訊) 或表示客戶與您的品牌互動的時間序列事件。

**新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 支援4000個區段 | 所有具有Experience Platform的組織現在最多可支援4000個區段定義。 如需此變更如何影響區段作業API的詳細資訊，請參閱[區段作業端點指南](../../segmentation/api/segment-jobs.md) |

如需有關 [!DNL Segmentation Service] 的詳細資訊，請參閱[分段概觀](../../segmentation/home.md)。

## 來源 {#sources}

Adobe Experience Platform可內嵌來自外部來源的資料，同時允許您使用Experience Platform服務來建構、加標籤及增強這些資料。 您可以從各種來源擷取資料，例如 Adob&#x200B;&#x200B;e 應用程式、雲端型儲存空間、協力廠商軟體和 CRM 系統。

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間並管理資料攝取輸送量。

**新功能**

| 功能 | 說明 |
| --- | --- |
| 自助來源的一般可用性(批次SDK) | 開發、測試及整合您的REST API型資料來源，以使用易於設定的來源規格將批次資料擷取到Experience Platform。 使用來源SDK，您可以： <ul><li>設定Experience Platform目錄的新來源。</li><li>定義來源規格，包括與支援的驗證型別、排程及資源資料擷取方式相關的資訊。</li><li>為您的新來源建立面向使用者的檔案。</li></ul> 如需詳細資訊，請參閱有關[自助式來源(批次SDK)](../../sources/sources-sdk/overview.md)的檔案。 |
| [!DNL Google BigQuery] 來源正式推出 | 使用[!DNL Google BigQuery]來源將資料從您的[!DNL Google BigQuery]資料倉儲擷取至Experience Platform。 如需詳細資訊，請閱讀[[!DNL Google BigQuery] 來源](../../sources/connectors/databases/bigquery.md)的檔案。 |
| [!DNL Teradata Vantage]來源(Beta) | 使用[!DNL Teradata Vantage]來源將混合式多雲端環境中的資料擷取至Experience Platform。 如需詳細資訊，請閱讀[[!DNL Teradata Vantage] 來源](../../sources/connectors/databases/teradata-vantage.md)的檔案。 |
| Adobe Analytics來源的跨區域支援 | 您現在可以從任何區域擷取報告套裝（美國、英國或新加坡）。 報告套裝必須對應至跟Experience Platform Sandbox執行個體（正在其中建立來源連線）相同的組織。 如需詳細資訊，請參閱[在UI](../../sources/tutorials/ui/create/adobe-applications/analytics.md)中建立Adobe Analytics來源連線的指南。 |

{style="table-layout:auto"}

若要深入瞭解來源，請參閱[來源概觀](../../sources/home.md)。
