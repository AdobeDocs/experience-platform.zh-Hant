---
title: Adobe Experience Platform 發行說明
description: Adobe Experience Platform 2023年8月版本注意事項。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 5c1566bac20f7fb83a0ce48c4fe7a22e15dbeb37
workflow-type: tm+mt
source-wordcount: '1650'
ht-degree: 37%

---

# Adobe Experience Platform 發行說明

**發行日期：2023 年 23 月 8 日**

Adobe Experience Platform 現有功能的更新：

- [Real-Time Customer Data Platform](#rtcdp)
- [以屬性為基礎的存取控制](#abac)
- [儀表板](#dashboards)
- [資料收集](#data-collection)
- [資料擷取](#data-ingestion)
- [資料準備](#data-prep)
- [體驗資料模式 (XDM)](#xdm)
- [身分識別服務](#identity-service)
- [Segmentation Service](#segmentation)
- [來源](#sources)

## Real-Time Customer Data Platform {#rtcdp}

建置在 Experience Platform、Real-Time Customer Data Platform ([!DNL Real-Time CDP]) 上有助於公司匯集已知和未知的資料，以使用整個客戶歷程中的智慧型決策啟動客戶設定檔。

[!DNL Real-Time CDP] 會結合多個企業資料來源以即時建立客戶設定檔。然後，根據這些設定檔建置的區段即可傳送到下游目的地，以便在所有管道和裝置上提供一對一的個人化客戶體驗。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 智慧型重新參與使用案例指南 | 此 [智慧型重新參與](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) 使用案例指南提供詳細資訊，說明如何與已放棄轉換的客戶重新互動，然後以聰明負責的方式完成轉換。 本指南使用下列範例歷程來重新吸引客戶： <ul><li>重新參與歷程 — 將目標定位為放棄產品瀏覽的客戶。</li><li>捨棄的購物車歷程 — 鎖定已將產品放入購物車但尚未完成購買的客戶。</li><li>訂單確認歷程 — 著重於產品購買</li></ul> 請使用底部的詳細意見選項連結 [智慧型重新參與使用案例指南](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) 以提供意見回饋。 |
| 合作夥伴資料支援 | 在Real-Time CDP中使用合作夥伴來源的潛在客戶設定檔和合作夥伴ID來執行上層漏斗行銷，以觸及新客戶並豐富您的第一方資料： <ul><li>客戶贏取與定址能力：運用資料合作夥伴選用的無Cookie識別碼和雜湊PII，觸及淨新客戶，並降低第三方Cookie相依性。</li><li>單一系統中的完整漏斗行銷：為單一系統中的潛在和已知客戶自助式細分、對象管理和原生啟用。</li><li>信任基礎：透過專利資料使用、標籤、存取控制及其他向市場銷售的資訊，以負責任的方式控管合作夥伴資料和設定檔。 如需詳細資訊，請參閱下列使用案例指南：現在提供潛在客戶使用案例指南。 閱讀潛在客戶使用案例指南，瞭解如何透過潛在客戶使用案例來吸引和贏取新客戶：<ul><li>[潛在客戶](../../rtcdp/partner-data/prospecting.md)</li><li>[站上個人化](../../rtcdp/partner-data/onsite-personalization.md)</li><li>[補充第一方設定檔](../../rtcdp/partner-data/supplement-first-party-profiles.md)</li><li>[啟用潛在客戶對象](../../destinations/ui/activate-prospect-audiences.md)</li></ul> |

{style="table-layout:auto"}

如需詳細資訊，請閱讀 [Real-Time CDP概觀](../../rtcdp/overview.md).

## 以屬性為基礎的存取控制 {#abac}

以屬性為基礎的存取控制是Adobe Experience Platform的一項功能，可讓注重隱私權的品牌在管理使用者存取許可權時擁有更大的彈性。 可以將個別物件（例如綱要欄位和區段）指派給使用者角色。 此功能可讓您為貴組織中的特定Platform使用者，授予或撤銷個別物件的存取權。

透過以屬性為基礎的存取控制，您組織的管理員可以控制使用者對所有Platform工作流程與資源的敏感個人資料(SPD)、個人識別資訊(PII)及其他自訂型別資料的存取。 管理員可以定義僅能存取特定欄位的使用者角色，以及對應至這些欄位的資料。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 許可權原則沙箱設定 | 新的 [許可權原則沙箱設定](../../access-control/abac/ui/policies.md) 功能可讓您根據您的需求和需求，對所有或所選數量的沙箱強制執行以屬性為基礎的存取控制原則。 |

{style="table-layout:auto"}

如需以屬性為基礎的存取控制的詳細資訊，請參閱 [屬性型存取控制概觀](../../access-control/abac/overview.md). 如需以屬性為基礎的存取控制工作流程的完整指南，請參閱 [屬性型存取控制端對端指南](../../access-control/abac/end-to-end-guide.md).

## 儀表板 {#dashboards}

Adobe Experience Platform 提供了多個儀表板，您可以透過這些儀表板檢視每日快照期間擷取的有關組織資料的重要分析。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 同意分析和追蹤使用案例 | 瞭解如何針對各種行銷使用案例，使用建立Real-Time CDP資料的同意儀表板 [同意分析和追蹤檔案](../../dashboards/insights-use-cases/consent-analysis.md). 它詳細說明如何根據您的業務需求建立具有適當屬性的受眾，然後透過Adobe Experience Platform UI中使用預先設定的Widget來使用深入分析。 它還提供有關如何使用使用者定義儀表板功能建置您自己的自訂Widget的說明。 本檔案涵蓋同意趨勢和同意重疊使用案例。 |

{style="table-layout:auto"}

如需有關儀表板的詳細資訊，包括如何授予存取權限和建立自訂 Widget，請先詳閱[儀表板概觀](../../dashboards/home.md)。

## 資料收集 {#data-collection}

Adobe Experience Platform 提供了一套技術，讓您可收集用戶端客戶體驗資料並將其傳送到 Adobe Experience Platform Edge Network，在其中可擴充、轉換資料並將其分送至 Adobe 或非 Adobe 目的地。

**新功能或更新功能**

| 類型 | 功能 | 說明 |
| --- | --- | --- |
| 標記和事件轉送 | [Experience Platform標籤（中國）](/help/tags/ui/publishing/premium-cdn.md) | 新的Experience Platform標籤（中國）功能改善了網站可靠性和延遲，讓在中國網站上部署標籤的客戶可加快回應時間。 客戶現在可在中國實作網站時，使用標籤資料庫中的JavaScript程式碼。 此功能也已新增至統一布建通訊協定(UPP)，以便在購買後自動部署產品。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀 [資料集合概觀](../../tags/home.md).

## 資料擷取 {#data-ingestion}

Adobe Experience Platform 會提供一組豐富的功能，用於擷取任何類型和任何延遲的資料。您可以使用批次或串流 API (使用 Adobe 建置的來源、資料整合合作夥伴或 Adobe Experience Platform UI) 進行擷取。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 資料擷取工作流程的變更 | 包含大於指定資料型別（例如，以整數資料型別傳遞的長資料）的資料列現在將會遭到拒絕，並會報告錯誤訊息。 以前，這些列會在沒有警告的情況下被拒絕。 |

如需詳細資訊，請閱讀 [資料擷取概觀](../../ingestion/home.md).

## 資料準備 {#data-prep}

「資料準備」讓資料工程師可在體驗資料模式 (XDM) 之間對應、轉換和驗證資料。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 支援篩選次要身分 | 您現在可以使用「資料準備」來篩選來自Adobe Analytics的身分，例如AAID和AACUSTOMID。 如果篩選掉，這些身分不會擷取到即時客戶個人檔案中。 未篩選的資料將繼續內嵌至Data Lake。 |
| 支援新功能 `correlationID` Adobe Analytics的欄位 | 此 `_experience.decisioning.propositions.scopeDetails.correlationID` 欄位現在可在Adobe Analytics來源聯結器結構描述中使用。 此欄位用於支援A4T分類，並將從2023年9月起填入。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀 [資料準備總覽](../../data-prep/home.md).

## 體驗資料模式 (XDM) {#xdm}

XDM 是一種開放原始碼的規格，可為帶到 Adobe Experience Platform 中的資料提供通用結構和定義 (架構)。若遵守 XDM 標準，即可將所有客戶體驗資料合併到一個常用表述中，以更快速、更整合的方式傳遞分析。您可以從客戶行為中獲得有價值的分析，透過區段定義客戶對象，並使用客戶屬性實現個人化的目的。

**新的 XDM 元件**

| 元件類型 | 名稱 | 說明 |
| --- | --- | --- |
| 類別 | [[!UICONTROL XDM 個別潛在客戶設定檔]](https://github.com/adobe/xdm/pull/1758/files) | 使用此類別引入來自資料供應商的漏斗頂部客戶贏取使用案例的潛在客戶資料。 |

{style="table-layout:auto"}

**已更新的 XDM 元件**

| 元件類型 | 名稱 | 更新說明 |
| --- | --- | --- |
| 副檔名([!UICONTROL Adobe Analytics ExperienceEvent完整擴充功能]) | [[!UICONTROL 內容資料]](https://github.com/adobe/xdm/pull/1761/files) | [!UICONTROL 內容資料] 將對應物件新增至 [!UICONTROL Adobe Analytics ExperienceEvent完整擴充功能] 以提供Adobe Analytics的內容資料。 |
| 欄位群組 | 多個 | 多個欄位已新增至 [[!UICONTROL 擴充事件區段詳細資訊]](https://github.com/adobe/xdm/pull/1760/files). |

{style="table-layout:auto"}

如需詳細資訊，請閱讀 [XDM系統概覽](../../xdm/home.md).

## 身分識別服務 {#identity-service}

Adobe Experience Platform 身分識別服務透過跨裝置和系統橋接身分，為您提供客戶及其行為的全方位檢視，讓您可即時實現有影響力的個人數位體驗。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 身分圖表限制的變更 | 在9月底前，身分圖表將變更為每個圖表50個身分，並將擷取最新身分。 因此，系統會根據擷取時間戳記和身分型別刪除最舊的身分，並會先刪除Cookie身分型別。 今天，身分圖表限制每個圖表有150個身分，一旦達到此限制，圖表將不再更新。 如果您的生產沙箱包含： <ul><li>將人員識別碼（例如CRM ID）設定為Cookie/裝置身分型別的自訂名稱空間。</li><li>將cookie/裝置識別碼設定為跨裝置識別型別的自訂名稱空間。</li></ul> Adobe工程將手動處理這些請求。 如需詳細資訊，請閱讀 [Identity Service資料的護欄](../../identity-service/guardrails.md). |

如需詳細資訊，請閱讀 [Identity Service總覽](../../identity-service/home.md).

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 可讓您將儲存在和個人 (例如客戶、潛在客戶、使用者或組織) 相關的 [!DNL Experience Platform] 中的資料分段為不同的對象。您可以透過區段定義或來自 [!DNL Real-Time Customer Profile] 資料的其他來源建立對象。這些對象會在 [!DNL Platform] 上集中設定及維護，並可透過任何 Adobe 解決方案輕鬆存取。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 相似的對象（可用性限制） | 相似的對象會針對您的每個對象提供智慧型深入分析，運用機器學習式的深入分析，透過您的行銷活動識別及鎖定高價值客戶。 透過相似受眾，您可以建立擴充受眾，將目標鎖定於與您表現優異的受眾類似的客戶，或將目標鎖定於與先前轉換的受眾類似的客戶。 如需相似對象的詳細資訊，請參閱 [相似受眾概述](../../segmentation/ui/lookalike-audiences.md). |

{style="table-layout:auto"}

如需詳細資訊，請閱讀 [區段概觀](../../segmentation/home.md).

## 來源 {#sources}

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定擷取執行的時間並管理資料擷取輸送量。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 正式發行 [!DNL SugarCRM] | [!DNL SugarCRM] 來源現已可用。 使用 [!DNL SugarCRM Accounts & Contacts] 和 [!DNL SugarCRM Events] 來源將資料從您的 [!DNL SugarCRM] 帳戶帶到 Experience Platform。如需詳細資訊，請閱讀 [[!DNL SugarCRM]  概觀](../../sources/connectors/crm/sugarcrm.md)。 |
| 支援UI中來源資料流的隨選擷取 | 您現在可以在UI中依需求建立現有來源資料流程的流程執行。 如需詳細資訊，請閱讀以下指南： [使用UI建立來源的隨選流程執行](../../sources/tutorials/ui/on-demand-ingestion.md). |

{style="table-layout:auto"}

如需詳細資訊，請閱讀 [來源概觀](../../sources/home.md).
