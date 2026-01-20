---
title: Experience Platform發行前說明
description: Adobe Experience Platform最新版本注意事項預覽。
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: acb8303673c3271794dcda87b149b473328a7a21
workflow-type: tm+mt
source-wordcount: '1150'
ht-degree: 24%

---

# Adobe Experience Platform搶鮮版發行說明

>[!IMPORTANT]
>
>本檔案旨在當月發行說明的&#x200B;**預覽**。 發行專案可能會有所變更，且可能會在最終發行中新增或移除。

>[!TIP]
>
>如需其他 Adobe Experience Platform 應用程式的發行說明，請參閱以下文件：
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/releases/pre-release-notes)
>- [聯合客群構成](https://experienceleague.adobe.com/zh-hant/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/zh-hant/docs/real-time-cdp-collaboration/using/latest)

**發行日期： 2026年1月**

Adobe Experience Platform 的新功能及現有功能更新：

- [Agent Orchestrator](#agent-orchestrator)
- [目標](#destinations)
- [即時客戶輪廓](#real-time-customer-profile)
- [結構描述](#schemas)
- [細分服務](#segmentation-service)
- [來源](#sources)

## Agent Orchestrator {#agent-orchestrator}

Agent Orchestrator可讓您建置和部署AI支援的代理程式，這些代理程式可自動化工作流程，並在多個管道與客戶互動。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| Agent Orchestrator試用方案 | Agent Orchestrator現在提供試用方案，讓客戶在確認完整購買服務前，先探索及測試該服務。 這個購買前試用選項可讓組織評估Agent Orchestrator在其自身環境中的功能，包括技能和協調功能。 此試用版提供建置AI支援代理程式的實作體驗，並瞭解如何將其整合至現有工作流程。 |

{style="table-layout:auto"}

如需詳細資訊，請參閱[Agent Orchestrator檔案](https://experienceleague.adobe.com/zh-hant/docs/experience-cloud-ai/experience-cloud-ai/agents/agent-orchestrator)。

## 目標 {#destinations}

[!DNL Destinations] 是預先建立的目標平台整合功能，能夠順暢啟用來自 Experience Platform 的資料。您可以使用目標來啟用已知和未知的資料，以供跨通道行銷活動、電子郵件行銷活動、定向廣告及其他許多使用案例使用。

**全新或更新版功能**

| 功能 | 說明 |
| --- | --- |
| 更新Adobe Target目的地的護欄限制 | 可對應至單一Adobe Target目的地的受眾數量上限，已經從50增加到250。 這可讓Adobe Target符合其他目的地的標準對象限制，為對象啟用工作流程提供更大的彈性。 客戶現在可以對Adobe Target目的地啟用更多對象，而無需建立多個資料流。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[目標概觀](../destinations/home.md)。

## 即時客戶輪廓 {#real-time-customer-profile}

即時客戶設定檔可讓您透過合併來自多個管道（包括線上、離線、CRM和第三方資料）的資料，檢視每個個別客戶的整體檢視。 設定檔可讓您將客戶資料合併成統一的檢視畫面，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 串流容量強制執行 | Experience Platform現在為即時客戶個人資料和身分服務強制執行串流輸送量容量。 當客戶超過其合約的串流容量時，資料將會以先進先出方式排入佇列及處理。 這可確保可預測的系統效能，並防止容量違規影響資料擷取品質。 重要注意事項：超過容量時，資料湖上將無法使用串流更新插入，此強制不適用於擁有Adobe Journey Optimizer授權的客戶，而且一旦容量可用，佇列的資料將會依序處理。 |
| 不再使用Real-Time CDP Prime的API存取 | 所有Real-Time CDP Prime客戶現在都不再使用體驗事件的API存取。 此變更會影響透過API直接查詢體驗事件的能力。 Real-Time CDP Ultimate客戶可透過正式的例外程式來要求例外狀況，以便視使用案例的需求啟用體驗事件API存取。 此淘汰專案有助於最佳化系統效能，並符合資料存取模式的最佳實務。 |
| 監視資料流執行 | 您現在可以在Profile中監視資料流執行的進度和整備。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀 [[!DNL Real-Time Customer Profile]  概觀](../profile/home.md)。

## 結構描述 {#schemas}

Experience Platform使用結構描述，以一致且可重複使用的方式說明資料結構。 藉由定義跨系統的一致資料，將更容易保留意義，進而從資料中獲得價值。 結構描述是由基底類別和零個或多個結構描述欄位群組所組成。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 使用搜尋、篩選、標籤和資料夾進行結構描述詳細目錄現代化 | 結構描述瀏覽頁面已更新，可提供增強的組織和探索功能。 新功能包括進階搜尋和篩選選項、支援使用者產生的標籤和資料夾來組織結構描述，以及內嵌動作來簡化工作流程。 關鍵改進包括：更新欄（名稱、類別、資料集、身分、關係、為設定檔啟用、行為、結構描述型別、標籤、建立日期、上次修改）、進階篩選器（顯示設定檔、結構描述型別、類別、具有任何標籤、建立者、建立日期、修改日期、具有主要身分、具有關係、主要身分名稱空間）、內嵌動作（編輯、刪除、套用標籤、為非關聯式結構描述建立資料集、管理標籤、移動到資料夾、新增到套件、複製JSON結構、下載範例檔案）以及組織能力使用標籤和資料夾的架構。 這些增強功能提供方案資源的全面可見度，並在沙箱層級實現更有效的方案管理。 |

如需詳細資訊，請閱讀 [[!DNL Schemas]  概觀](../xdm/home.md)。

## 細分服務 {#segmentation-service}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷人員群組的標準，進而定義設定檔的特定子集。客群的根據可以是記錄資料 (例如人口統計資訊) 或是代表客戶與您的品牌互動情形的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 串流細分監視 | 串流區段的即時監視可在沙箱、資料集和受眾層級提供評估率、延遲和資料品品質度的透明度。 此功能支援主動警示和可操作的洞察，可協助資料工程師識別容量違規和攝取問題。監控量度包括評估率、P95擷取延遲，以及接收、評估、失敗和略過的記錄。 逐個資料集和逐個對象檢視功能可全面顯示符合資格和取消資格的淨新設定檔。 |
| 外部對象TTL重新整理 | 外部對象（例如CSV上傳）現在支援存留時間(TTL)設定的強制重新整理功能。 此功能可讓使用者手動重新整理外部對象的TTL到期日，在對象生命週期管理的控制方面提供更大力。 這對於需要在初始TTL期間之後持續存在或需要重新啟用而不需重新上傳資料的對象特別有用。 |

如需詳細資訊，請閱讀[[!DNL Segmentation Service] 概觀](../segmentation/home.md)。

## 來源 {#sources}

Experience Platform 提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證，並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間，並管理資料攝取輸送量。

**新的或更新來源**

| 來源 | 說明 |
| --- | --- |
| [!DNL Oracle Eloqua] V2來源 | 新的[!DNL Oracle Eloqua]來源聯結器現已可用，取代已棄用的聯結器。 此更新的聯結器提供增強的功能，並改善將資料從[!DNL Oracle Eloqua]擷取到Experience Platform的可靠性。 使用現有聯結器的客戶應移轉至新的實作，因為現有連線將無法繼續運作。 新聯結器支援連線至[!DNL Oracle Eloqua]並擷取行銷自動化資料所需的所有設定和設定步驟。 |
| [!DNL Salesforce Marketing Cloud] V2來源 | 新的[!DNL Salesforce Marketing Cloud]來源聯結器現已可用，取代已棄用的聯結器。 此更新的聯結器提供改良的效能和額外功能，可將資料從[!DNL Salesforce Marketing Cloud]擷取至Experience Platform。 使用現有聯結器的客戶應轉換至新實作。 新聯結器包含連線至[!DNL Salesforce Marketing Cloud]及擷取行銷自動化資料的完整設定指示。 |

如需詳細資訊，請閱讀[來源概觀](../sources/home.md)。

