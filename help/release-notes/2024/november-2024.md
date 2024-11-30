---
title: Adobe Experience Platform 發行說明 (2024 年 11 月)
description: Adobe Experience Platform 2024 年 11 月版發行說明。
exl-id: e3969f8b-70b2-40f8-bb9b-5be6e3d8f722
source-git-commit: f71fc1d4ad51af52046caeee289546e05967d5bd
workflow-type: tm+mt
source-wordcount: '852'
ht-degree: 98%

---

# Adobe Experience Platform 發行說明

>[!TIP]
>
>新的[AI Assistant產品檔案](../../ai-assistant/landing.md)現已推出。 使用此頁面作為所有 AI 助理相關資源的中心。

**發行日期：2024 年 11 月 26 日**

Adobe Experience Platform 現有功能和文件的更新：

- [AI 助理](#ai-assistant)
- [目標](#destinations)
- [查詢服務](#query-service)
- [沙箱](#sandboxes)
- [文件更新](#documentation-updates)
   - [互動式 Experience Platform API 文件](#interactive-experience-platform-api-documentation)
   - [Experience League 的新目錄](#new-table-of-contents-on-experience-league)
   - [全新 AI 助理登陸頁面](#new-ai-assistant-landing-page)

## AI 助理 {#ai-assistant}

Adobe Experience Platform 的 AI 助理是一種對話式體驗，可用來加速 Adobe 應用程式中的工作流程。您可以使用 AI 助理增進產品知識、疑難排解問題，或搜尋資訊和尋找營運深入解析。AI 助理支援 Experience Platform、Real-Time Customer Data Platform、Adobe Journey Optimizer 和 Customer Journey Analytics。

**新功能**

| 功能 | 說明 |
| --- | --- |
| [!BADGE Alpha]{type=Informative} 監測重大變更並預測客群增長 | 使用 AI 助理可監測重大變更，並提供客群和資料集大小的成長預測。然後，您可以使用這些資訊來確保客群資料的完整性，並提供前瞻性預測來支援以資料為主的明智決策。如需更多資訊，請閱讀有關[監測重大變更和預測客群成長](../../ai-assistant/new-features/audience-forecasting.md)的指南。 |
| [!BADGE Alpha]{type=Informative} 自然語言預估 | 使用 AI 助理的自然語言預估功能可預估客群規模，並根據簡單的對話問題預測客群傾向。如需更多資訊，請閱讀有關[透過 AI 助理使用自然語言預估](../../ai-assistant/new-features/natural-language.md)的指南。 |

{style="table-layout:auto"}

## 目標 {#destinations}

[!DNL Destinations] 是預先建立的和目標平台的整合，可讓來自 Adobe Experience Platform 的資料順暢啟動。您可使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新目標或更新的目標** {#new-updated-destinations}

| 目標 | 說明 |
| --- | --- |
| [Magnite 即時串流](/help/destinations/catalog/advertising/magnite-streaming.md) | 匯出客群以在 Magnite 串流平台中進行啟用、目標市場選擇或隱藏。請注意，為了將客群正確匯出至 Magnite，您必須同時使用即時和批次目標。 |
| [Magnite 串流批次](/help/destinations/catalog/advertising/magnite-batch.md) | 匯出客群以在 Magnite 串流平台中進行啟用、目標市場選擇或隱藏。請注意，為了將客群正確匯出至 Magnite，您必須同時使用即時和批次目標。 |

{style="table-layout:auto"}

**新功能或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| --- | --- |
| [在邊緣即時查詢設定檔屬性](/help/destinations/ui/activate-edge-profile-lookup.md) | 了解如何即時查詢邊緣設定檔屬性以傳送個人化體驗，或藉由使用自訂個人化目標和 Edge Network API，透過下游應用程式通知決策規則。 |

{style="table-layout:auto"}

如需更多資訊，請閱讀[目標概觀](../../destinations/home.md)。

## 查詢服務 {#query-service}

使用具備查詢服務的標準 SQL，在 Adobe Experience Platform 資料湖查詢資料。從您的查詢結果來促進報告、啟用資料科學工作流程或協助擷取至即時客戶輪廓，以順暢無礙地合併資料集和產生新資料集。例如，您可以將客戶交易資料與行為資料合併，以確定具目標性之行銷活動的高價值客群。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 資料蒸餾器授權 API | 管理和強制執行基於 IP 的查詢服務沙箱存取限制，以增強資料安全性並確保符合組織原則。如需有關其主要特性和功能的更多資訊，請參閱[資料蒸餾器授權 API 指南](../../query-service/auth-api/overview.md)，或參閱 [OpenAPI 文件](https://developer.adobe.com/experience-platform-apis/references/data-distiller-auth/)以取得全方位資訊，包括端點詳細資訊、參數清單、請求/回應範例和測試功能。 |

如需更多有關 [!DNL Query Service] 的資訊，請參閱[[!DNL Query Service] 概觀](../../query-service/home.md)。

## 沙箱 {#sandboxes}

Adobe Experience Platform 是為了在全球規模上使數位體驗應用程式更加豐富而打造。公司經常要並行執行多個數位體驗應用程式，且在顧及這些應用程式的開發、測試和部署等需求的同時，也必須確保營運合規性。為了滿足這種需求，Experience Platform 提供的沙箱可將單一 Platform 執行個體分割成個別的虛擬環境，以協助開發並改進數位體驗應用程式。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 使用沙箱工具 API 的套件共用 | 使用兩個新 API 端點 ([`/handshake`](../../sandboxes/sandbox-tooling-api/packages.md#org-linking) 和 [`/transfers`](../../sandboxes/sandbox-tooling-api/packages.md#transfer-packages))，透過沙箱工具 API 處理跨組織的套件共用，例如請求核准、套件可見度和匯入套件。 |

如需更多有關沙箱的資訊，請閱讀[沙箱概觀](../../sandboxes/home.md)。

## 文件更新 {#documentation-updates}

### 互動式 Experience Platform API 文件 {#interactive-api-documentation}

[Experience Platform API 文件](https://developer.adobe.com/experience-platform-apis/)現在是完全互動式，可讓您直接在 API 參考文件頁面上驗證和探索 API。現在起，您現在前往所需的 API 參考文件頁面、建立或取得 API 驗證憑證，將其貼上至「**[!UICONTROL 嘗試]**」區塊，然後執行呼叫。所有動作都在單一頁面中進行。[閱讀更多](/help/landing/api-authentication.md#get-credentials-functionality)有關此功能的資訊。

### Experience League 的新目錄 {#new-table-of-contents-on-experience-league}

Experience League 文件頁面的目錄已改良，可為讀者提供更好的體驗，包括用於發現您需要之確切頁面的關鍵字篩選器、展開所有頁面的功能等。<br> ![新目錄體驗，包括關鍵字篩選器和展開所有頁面的功能。](../2024/assets/november/new-toc-experience.gif "新目錄體驗，包括關鍵字篩選器和展開所有頁面的功能。"){width="250" align="center" zoomable="yes"}

### 全新 AI 助理登陸頁面 {#new-ai-assistant-landing-page}

使用新的 [AI 助理產品文件](../../ai-assistant/landing.md)頁面作為 AI 助理所有內容的中心。請參閱產品文件，以了解影片教學課程、技術文件、使用案例以及有關 AI 助理的部落格文章連結。
