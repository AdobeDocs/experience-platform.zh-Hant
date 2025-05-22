---
title: Adobe Experience Platform 發行說明 (2025 年 5 月)
description: Adobe Experience Platform 2025 年 5 月版發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: ad9ec9c3177c25e2207b67b4c939c3f6fa97883f
workflow-type: tm+mt
source-wordcount: '1171'
ht-degree: 51%

---

# Adobe Experience Platform 發行說明

>[!TIP]
>
>如需其他 Adobe Experience Platform 應用程式的發行說明，請參閱以下文件：
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/releases/latest)
>- [聯合客群構成](https://experienceleague.adobe.com/zh-hant/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/zh-hant/docs/real-time-cdp-collaboration/using/latest)

**發行日期： 2025年5月20日**

Adobe Experience Platform 現有功能和文件的更新：

- [目錄服務](#catalog-service)
- [資料準備](#data-prep)
- [目標](#destinations)
- [身分識別服務](#identity)
- [查詢服務](#query-service)
- [沙箱](#sandboxes)
- [細分服務](#segmentation-service)
- [來源](#sources)

## 目錄服務 {#catalog-service}

目錄服務是 Adobe Experience Platform 內部的資料位置和譜系記錄系統。雖然攝取至 Experience Platform 中的所有資料都會以檔案及目錄形式儲存在資料湖中，但是為了查詢和監控目的，目錄也會保留這些檔案及目錄的中繼資料與說明。

| 功能 | 說明 |
| --- | --- |
| 使用資料集層級的保留規則最佳化資料儲存 | 使用根據您指定的時間範圍刪除過時資料的保留原則，有效管理資料儲存。 <ul><li>**資料集保留**：定義資料集規則，從資料湖和個人檔案存放區移除過時的資料。</li><li>**儲存裝置深入分析**：透過內嵌量度監視使用狀況並確保符合授權規範。</li><li>**增強的可見度**：透過改善的監視功能，追蹤從擷取到刪除的資料集活動。</li><li>**簡化管理**：在單一統一檢視中存取保留設定、監視、稽核記錄和深入分析。</li></ul> 如需詳細資訊，請參閱[資料集保留規則](../../catalog/datasets/user-guide.md#data-retention-policy)的指南。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[目錄服務總覽](../../catalog/home.md)。

## 資料準備 {#data-prep}

使用資料準備功能，與體驗資料模型 (XDM) 相互對應、轉換和驗證資料。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 支援Adobe Analytics的匯入和匯出對應 | 使用Adobe Analytics來源聯結器時，您現在可以針對Adobe Analytics報表套裝資料使用匯入和匯出對應功能。 <br><br>將您的對應匯出至CSV檔案，並在試算表上設定為本機。 接著，您可以透過使用者介面中的對應介面，將更新後的對應匯入 Experience Platform。您可以使用此功能設定大量對應，無需在使用者介面中手動建置。此外，在建立新的資料流時，您可以將對應的副本直接上傳至 Experience Platform，以加快工作流程。<br><br>如需詳細資訊，請閱讀[將Adobe Analytics連線到Experience Platform](../../sources/tutorials/ui/create/adobe-applications/analytics.md)的指南。</br> |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[資料準備概觀](../../data-prep/home.md)。

## 目標 {#destinations}

[!DNL Destinations] 是預先建立的目標平台整合功能，能夠順暢啟用來自 Adobe Experience Platform 的資料。您可以使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、定向廣告和其他諸多使用案例。

**全新或更新版功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| --- | --- |
| [Google客戶符合](../../destinations/catalog/advertising/google-customer-match.md)的其他識別碼支援 | Google客戶比對目的地現在支援對應位址相關欄位，以改善Google平台中的比對率。 <br><br>為確保Google符合位址，您必須對應全部四個位址欄位（`address_info_first_name`、`address_info_last_name`、`address_info_country_code`和`address_info_postal_code`），並確定這些欄位在匯出的設定檔中都沒有遺漏資料。 <br>如果有任何欄位未對應或包含遺漏的資料，Google將不會符合位址。 |
| [Facebook](../../destinations/catalog/social/facebook.md)連線的帳戶到期資料行 | 您現在可以在[瀏覽](../../destinations/ui/destinations-workspace.md#browse)和[帳戶](../../destinations/ui/destinations-workspace.md#accounts)索引標籤中看到Facebook帳戶權杖到期日。 |
| 匯出API建立的資料集 | 您現在可以匯出API建立的資料集。 先前只有在UI中建立的資料集才可供匯出的限制已解除。 深入瞭解[匯出資料集](../../destinations/ui/export-datasets.md)。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[目的地概觀](../../destinations/home.md)。

## 身分識別服務 {#identity}

Adobe Experience Platform 身分識別服務可在裝置及系統間進行身分識別橋接，進而建立客戶及其行為的全貌，協助您即時提供個人化且具影響力的數位體驗。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| [!DNL Identity Graph Linking Rules] | [!DNL Identity Graph Linking Rules]現已正式可用。 [!DNL Identity Graph Linking Rules]防止「圖表摺疊」，確保跨Experience Platform和應用程式進行個人化行銷時，有清楚且準確的客戶設定檔。 主要功能包括：<ul><li>[圖表模擬工具](../../identity-service/identity-graph-linking-rules/graph-simulation.md)：探索演演算法並測試身分設定組態。</li><li> [身分設定](../../identity-service/identity-graph-linking-rules/identity-settings-ui.md)：設定唯一的名稱空間並設定優先順序。</li><li>[身分儀表板](../../identity-service/identity-graph-linking-rules/implementation-guide.md#validate-your-graphs)：監檢視形並驗證身分設定。</li></ul> **注意**：在您手動設定身分設定之前，您的資料不會有任何變更。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[Identity Service概觀](../../identity-service/home.md)。

## 查詢服務 {#query-service}

「查詢服務」可讓您使用標準 SQL，在 Adobe Experience Platform 資料湖查詢資料。您可以順暢無礙地合併資料集，並根據查詢結果建立新資料集，以支援報表產出、啟用資料科學工作流程，或協助攝取至即時客戶輪廓。例如，您可以合併客戶交易資料與行為資料，以找出高價值客群進行精準行銷活動。

**新功能或更新功能**

| 功能 | 說明 |
|--------|-------------|
| JWT到OAuth憑證移轉 | 必須在2025年6月30日前將不過期JWT憑證移轉至OAuth伺服器對伺服器，以免服務中斷。 此變更可改善安全性與平台一致性。 如需詳細資訊，請參閱[從JWT移轉至OAuth伺服器對伺服器認證指南](../../query-service/ui/migrate-jwt-to-oauth.md)。 |
| 舊版結果表格（可用性限制） | 依賴拖曳選取工作流程的使用者可請求存取支援瀏覽器原生選擇和複製行為的舊版結果表格。 貼上的輸出以定位點分隔，因此欄在Excel中保持對齊和可讀取，讓試算表稽核和QA程式更容易。 如需詳細資訊，請參閱[查詢編輯器UI指南](../../query-service/ui/user-guide.md#legacy-results-table)。 |

如需更多有關 [!DNL Query Service] 的資訊，請參閱[[!DNL Query Service] 概觀](../../query-service/home.md)。

## 沙箱 {#sandboxes}

Adobe Experience Platform 旨在協助您在全球各地打造更豐富的數位體驗應用程式。公司經常需要並行執行多個數位體驗應用程式，且在顧及這些應用程式的開發、測試和部署等需求的同時，也必須確保營運合規性。為了滿足這種需求，Experience Platform 提供的沙箱可將單一 Experience Platform 執行個體分割成個別的虛擬環境，以協助開發並改進數位體驗應用程式。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 沙箱工具外掛程式支援擴充 | 行銷活動現在可以透過沙箱工具移轉與其他相依物件，包括通道設定、統一決定、實驗設定/變體等。 如需支援的行銷活動物件以及所有支援的Adobe Journey Optimizer物件的完整清單，請閱讀[沙箱工具](../../sandboxes/ui/sandbox-tooling.md#adobe-journey-optimizer-objects)指南。 |

{style="table-layout:auto"}

如需有關沙箱的詳細資訊，請閱讀[沙箱概觀](../../sandboxes/home.md)。

## 細分服務 {#segmentation-service}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷人員群組的標準，進而定義設定檔的特定子集。對象可以是以記錄資料（例如人口資訊）或代表客戶與品牌互動的時間序列事件為基礎。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 串流細分標準更新 | 從2025年5月版本開始，已更新適用於串流細分的受眾條件。 有關這些變更的更多資訊，請參閱[串流細分資格標準更新](../../segmentation/eligibility-criteria-update.md)。 |

## 來源 {#sources}

Experience Platform 提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證，並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間，並管理資料攝取輸送量。

使用 Experience Platform 中的來源，即可從 Adobe 應用程式或第三方資料來源攝取資料。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 支援[!DNL MySQL]的基本驗證 | 您現在可以使用基本驗證，將您的[!DNL MySQL]資料庫連線至Experience Platform。 如需詳細資訊，請閱讀[[!DNL MySQL] 來源概觀](../../sources/connectors/databases/mysql.md)。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[來源概觀](../../sources/home.md)。