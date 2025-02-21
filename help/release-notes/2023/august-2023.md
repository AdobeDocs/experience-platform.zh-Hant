---
title: Adobe Experience Platform 發行說明 (2023 年 8 月)
description: Adobe Experience Platform 2023 年 8 月版發行說明。
exl-id: c67dca3a-eccb-427e-8ab3-b69c51b57938
source-git-commit: 4afb2c76f2022423e8f1fa29c91d02b43447ba90
workflow-type: tm+mt
source-wordcount: '1741'
ht-degree: 92%

---

# Adobe Experience Platform 發行說明

**發行日期：2023 年 23 月 8 日**

Adobe Experience Platform 現有功能的更新：

- [Real-Time Customer Data Platform](#rtcdp)
- [屬性型存取控制](#abac)
- [儀表板](#dashboards)
- [資料收集](#data-collection)
- [資料擷取](#data-ingestion)
- [資料準備](#data-prep)
- [目標](#destinations)
- [體驗資料模式 (XDM)](#xdm)
- [身分識別服務](#identity-service)
- [Segmentation Service](#segmentation)
- [來源](#sources)

## Real-Time Customer Data Platform {#rtcdp}

建置在 Experience Platform、Real-Time Customer Data Platform ([!DNL Real-Time CDP]) 上有助於公司匯集已知和未知的資料，以使用整個客戶歷程中的智慧型決策啟動客戶輪廓。

[!DNL Real-Time CDP] 會結合多個企業資料來源以即時建立客戶輪廓。然後，根據這些輪廓建置的區段即可傳送到下游目標，以便在所有管道和裝置上提供一對一的個人化客戶體驗。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 智慧型重新吸引使用案例指南 | [智慧型重新吸引](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md)使用案例指南會提供有關以智慧且可靠方式重新吸引在完成轉換之前放棄轉換的客戶之詳細資訊。本指南使用以下範例歷程來重新吸引客戶： <ul><li>重新吸引歷程 - 針對有捨棄產品瀏覽的客戶。</li><li>捨棄購物車歷程 - 針對已將產品放入購物車但尚未完成購買的客戶。</li><li>訂單確認歷程 - 著重產品購買</li></ul> 請使用[智慧型重新吸引使用案例指南](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md)底部的詳細意見反饋選項連結來提供反饋。 |
| 合作夥伴資料支援 | 在 Real-Time CDP 中執行漏斗上層行銷，利用合作夥伴提供的潛在客戶資料和合作夥伴 ID 來吸引新客戶並擴充您的第一方資料： <ul><li>客戶贏取和可尋址性：利用所選資料合作夥伴的無 cookie 識別碼和雜湊 PII 來吸引新客戶並減少第三方 cookie 相依性。</li><li>單一系統中的完整漏斗行銷：在單一系統中對潛在客戶和已知客戶進行自助分段、客群管理和原生啟用。</li><li>信任基礎：透過專利資料用量、標籤、存取控制等，以負責方式管理合作夥伴資料和輪廓。請閱讀以下使用案例指南，了解更多資訊：尋找潛在客戶使用案例指南現已推出。閱讀尋找潛在客戶使用案例指南，了解如何透過尋找潛在客戶使用案例吸引和贏得新客戶：<ul><li>[尋找潛在客戶](../../rtcdp/partner-data/prospecting.md)</li><li>[現場個人化](../../rtcdp/partner-data/onsite-personalization.md)</li><li>[補充第一方輪廓](../../rtcdp/partner-data/supplement-first-party-profiles.md)</li><li>[啟用潛在客戶客群](../../destinations/ui/activate-prospect-audiences.md)</li></ul> |

{style="table-layout:auto"}

若要了解更多資訊，請詳閱[Real-Time CDP 概觀](../../rtcdp/overview.md)。

## 屬性型存取控制 {#abac}

屬性型存取控制是 Adob&#x200B;&#x200B;e Experience Platform 的一項功能，此平台為注重隱私的品牌提供更大的靈活性來管理使用者存取。可以將結構描述欄位和分段等個別物件指派給使用者角色。此功能允許您授予或撤銷組織中特定平台使用者對個別物件的存取權限。

透過屬性型存取控制，組織的管理員可以控制使用者對所有平台工作流程和資源的存取權限，包括其中的敏感個人資料 (SPD)、個人身分資訊 (PII) 和其他自訂類型資料。管理員可以定義只能存取特定欄位以及這些欄位對應資料的使用者角色。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 權限原則沙箱設定 | 此項新的[權限原則沙箱設定](../../access-control/abac/ui/policies.md)功能允許您根據本身需要和要求，對所有或特定數量的沙箱實施屬性型存取控制原則。 |

{style="table-layout:auto"}

若要了解更多關於屬性型存取控制，請參閱[屬性型存取控制概觀](../../access-control/abac/overview.md)。關於屬性型存取控制工作流程的綜合指南，請閱讀[屬性型存取控制端對端指南](../../access-control/abac/end-to-end-guide.md)。

## 儀表板 {#dashboards}

Adobe Experience Platform 提供了多個儀表板，您可以透過這些儀表板檢視每日快照期間擷取的有關組織資料的重要分析。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 同意分析和追蹤使用案例 | 瞭解如何使用[同意分析和追蹤檔案](../../dashboards/insights-use-cases/consent-analysis.md)，針對Real-Time CDP資料的各種行銷使用案例建立同意儀表板。 此文件會詳細介紹如何建立具備符合您業務需求屬性為主的客群，然後透過使用 Adob&#x200B;&#x200B;e Experience Platform UI 中的預設小工具來獲取深入的分析和見解。此文件還會說明如何使用使用者定義的儀表板功能來構建您自己的自訂小工具。本檔案涵蓋同意趨勢和同意重疊使用案例。 |

{style="table-layout:auto"}

如需有關儀表板的詳細資訊，包括如何授予存取權限和建立自訂小工具，請先詳閱[儀表板概觀](../../dashboards/home.md)。

## 資料收集 {#data-collection}

Adobe Experience Platform 提供了一套技術，讓您可收集用戶端客戶體驗資料並將其傳送到 Adobe Experience Platform Edge Network，在其中可擴充、轉換資料並將其分送至 Adobe 或非 Adobe 目標。

**新功能或更新功能**

| 類型 | 功能 | 說明 |
| --- | --- | --- |
| 標記和事件轉送 | [Experience Platform 標籤 (中國)](/help/tags/ui/publishing/premium-cdn.md) | 全新 Experience Platform 標題 (中國) 功能會提高網站可靠性和延遲，進而為中國網站上部署標籤的客戶提供更快的回應時間。現在，客戶在中國實施網站時可以使用標籤庫中的 JavaScript 代碼。此功能也已新增至統一佈建置協定 (Unified Provisioning Protocol，UPP) 中，允許在購買後自動進行產品部署。 |

{style="table-layout:auto"}

若要了解更多資訊，請詳閱[資料集合概觀](../../tags/home.md)。

## 資料擷取 {#data-ingestion}

Adobe Experience Platform 會提供一組豐富的功能，用於擷取任何類型和任何延遲的資料。您可以使用批次或串流 API (使用 Adobe 建置的來源、資料整合合作夥伴或 Adobe Experience Platform UI) 進行攝取。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 資料擷取工作流程的變更 | 現在，包含數值大於指定資料類型 (例如，作為整數資料類型傳遞的長資料) 的資料行將被拒絕，且系統會報告錯誤訊息。以前，這些資料行會在沒有警告的情況下被拒絕。 |

若要了解更多資訊，請詳閱[資料擷取概觀](../../ingestion/home.md)。

## 資料準備 {#data-prep}

「資料準備」讓資料工程師可在體驗資料模式 (XDM) 之間對應、轉換和驗證資料。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 支持篩選次要身分識別 | 您現在可以使用資料準備來篩選來自 Adob&#x200B;&#x200B;e Analytics 的身分識別，例如 AAID 和 AACUSTOMID。若經過篩選去除，這些身分識別將不會被擷取至即時客戶輪廓中。未被篩選去除的資料將繼續被擷取至資料湖。 |

{style="table-layout:auto"}

若要了解更多資訊，請詳閱[資料準備概觀](../../data-prep/home.md)。

## 目標 {#destinations}

[!DNL Destinations] 是預先建立的和目標平台的整合，可讓來自 Adobe Experience Platform 的資料順暢啟動。您可使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新功能或更新的功能** {#destinations-new-updated-functionality}

- 您現在可以[啟用潛在客戶對象](../../destinations/ui/activate-prospect-audiences.md)至雲端儲存目的地。
- 每個沙箱最多100個目的地的一般[啟動護欄](../../destinations/guardrails.md#general-activation-guardrails)已更新為&#x200B;_硬性限制_。

如需有關目標的詳細一般資訊，請參閱[目標概觀](../../destinations/home.md)。

## 體驗資料模式 (XDM) {#xdm}

XDM 是一種開放原始碼的規格，可為帶到 Adobe Experience Platform 中的資料提供通用結構和定義 (結構描述)。若遵守 XDM 標準，即可將所有客戶體驗資料合併到一個常用表述中，以更快速、更整合的方式傳遞分析。您可以從客戶行為中獲得有價值的分析，透過區段定義客戶客群，並使用客戶屬性實現個人化的目的。

**新的 XDM 元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 類別 | [[!UICONTROL XDM 個別潛在客戶輪廓]](https://github.com/adobe/xdm/pull/1758/files) | 此類別可讓您從資料供應商最頂層的客戶贏取使用案例取得潛在客戶設定檔。 請參閱[[!UICONTROL XDM個別潛在客戶設定檔]](../../xdm/classes/prospect.md)檔案，檢視範例並瞭解更多資訊。 |

{style="table-layout:auto"}

**已更新的 XDM 元件**

| 元件類型 | 名稱 | 更新說明 |
| --- | --- | --- |
| 擴充功能([!UICONTROL Adobe Analytics ExperienceEvent完整擴充功能]) | [[!UICONTROL 內容資料]](https://github.com/adobe/xdm/pull/1761/files) | [!UICONTROL 內容資料]對應物件已新增至[!UICONTROL Adobe Analytics ExperienceEvent完整擴充功能]，以提供Adobe Analytics的內容資料。 |
| 欄位群組 | 多個 | 數個欄位已新增至[[!UICONTROL 擴充事件區段詳細資料]](https://github.com/adobe/xdm/pull/1760/files)。 |

{style="table-layout:auto"}

若要了更多資訊，請閱讀 [XDM 系統概觀](../../xdm/home.md)。

## 身分識別服務 {#identity-service}

Adobe Experience Platform 身分識別服務透過跨裝置和系統橋接身分，為您提供客戶及其行為的全方位檢視，讓您可即時實現有影響力的個人數位體驗。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 身分識別圖譜限制的變更 | 到了 9 月底，身分識別圖譜將變更為每個圖譜 50 個身分識別，並且最後一個身分識別會被擷取。因此，系統將根據擷取時間戳和身分類型刪除最舊的身分識別，並最先會刪除 cookie 身分識別類型。現在，身分識別圖譜的每個圖譜有 150 個身分識別的限制，一旦達到上限，圖譜就不再更新。如果您的生產沙箱包含以下內容，請聯絡您的客戶代表以要求變更身分識別類型： <ul><li>個人識別碼 (例如 CRM ID) 設定為 cookie/裝置身分識別類型的自訂命名空間。</li><li>cookie/裝置識別碼被設定為跨裝置身分識別類型的自訂命名空間。</li></ul> Adobe 工程部門將手動處理這些要求。若要了解更多資訊，請閱讀[身分識別服務資料的護欄](../../identity-service/guardrails.md)。 |

若要了解更多資訊，請詳閱[身分識別服務概觀](../../identity-service/home.md)。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 可讓您將儲存在和個人 (例如客戶、潛在客戶、使用者或組織) 相關的 [!DNL Experience Platform] 中的資料分段為不同的客群。您可以透過區段定義或來自 [!DNL Real-Time Customer Profile] 資料的其他來源建立客群。這些客群會在 [!DNL Platform] 上集中設定及維護，並可透過任何 Adobe 解決方案輕鬆存取。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 相似的客群 (數量有限) | 相似客群可以為您的每個客群提供智慧型分析見解，運用機器學習型的分析見解來透過行銷活動識別和鎖定高價值客戶。透過相似客群功能，您可以建立範圍擴大的客群，目標是針對類似高績效客群的客戶或類似先前轉換客群的客戶。若要了解更多相似客群，請閱讀[相似客群概觀](../../segmentation/types/account-audiences.md)。 |

{style="table-layout:auto"}

若要了解更多資訊，請詳閱[分段概觀](../../segmentation/home.md)。

## 來源 {#sources}

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間並管理資料攝取輸送量。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 正式推出 [!DNL SugarCRM] | [!DNL SugarCRM] 來源現已推出。使用 [!DNL SugarCRM Accounts & Contacts] 和 [!DNL SugarCRM Events] 來源將資料從您的 [!DNL SugarCRM] 帳戶帶到 Experience Platform。如需詳細資訊，請閱讀 [[!DNL SugarCRM]  概觀](../../sources/connectors/crm/sugarcrm.md)。 |
| 支持 UI 中來源資料流的隨選擷取 | 現在，您可以根據需要為 UI 中的現有來源資料流建立流量執行。若要了解更多資訊，請閱讀[為使用 UI 的來源建立隨選的流量執行](../../sources/tutorials/ui/on-demand-ingestion.md)。 |
| 支持 Adobe Analytics 新的 `correlationID` 欄位 | `_experience.decisioning.propositions.scopeDetails.correlationID` 欄位現在適用於 Adob&#x200B;&#x200B;e Analytics 來源連接器的結構描述中。此欄位是用來支持 A4T 分類，並將於 2023 年 9 月開始填入。 |

{style="table-layout:auto"}

若要了解更多資訊，請詳閱[來源概觀](../../sources/home.md)。
