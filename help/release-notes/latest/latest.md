---
title: Adobe Experience Platform發行說明2024年6月
description: Adobe Experience Platform 2024 年 6 月的發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 01ce38d26cf61706de84ec143e3dd8af720d0591
workflow-type: tm+mt
source-wordcount: '1357'
ht-degree: 18%

---

# Adobe Experience Platform 發行說明

**發行日期： 2024年6月18日**

>[!TIP]
>
>[Experience Platform中的AI助理](https://platform.adobe.com) 現已推出。 使用AI助理加速您在Adobe應用程式中的工作流程。 [閱讀全文](#ai-assistant) 關於新功能。

Adobe Experience Platform中的新功能：

- [AI 助理](#ai-assistant)
- [Experience Platform API 的驗證](#authentication-platform-apis)
- [資料準備](#data-prep)
- [目的地](#destinations)
- [身分識別服務](#identity-service)
- [Privacy Service](#privacy)
- [Segmentation Service](#segmentation)
- [使用案例教戰手冊](#use-case-playbooks)

## AI 助理 {#ai-assistant}

Adobe Experience Platform中的AI助理是一種對話式體驗，可用來加速Adobe應用程式中的工作流程。 您可以使用AI Assistant來進一步瞭解產品知識、疑難排解問題，或搜尋資訊並尋找營運見解。 AI助理支援Experience Platform、Real-time Customer Data Platform、Adobe Journey Optimizer和Customer Journey Analytics。

**新功能**

| 功能 | 說明 |
| --- | --- |
| Experience Platform中的AI助理 | 您現在可以在Experience Platform中使用AI助理。 AI助理支援Experience Platform、Real-time Customer Data Platform、Adobe Journey Optimizer和Customer Journey Analytics。 <br> ![Experience Platform中的AI助理。](../2024/assets/june/ai-assistant-full.png "Experience Platform中的AI助理。"){width="100" zoomable="yes"} <br> 如需有關此功能的詳細資訊，請參閱 [AI助理使用者介面指南](../../ai-assistant/ui-guide.md). |
| 支援產品知識問題 | [產品知識](../../ai-assistant/home.md#product-knowledge) 是以Experience League檔案為根據的概念和主題，可用於定點學習、開放式探索和疑難排解。 您可以詢問AI Assistant產品知識問題，例如： <ul><li>哪些對象具有相似性？</li><li>如何計算設定檔豐富度？</li><li> 我可以在擷取資料後刪除已啟用設定檔的結構描述嗎？</li></ul> |
| [!BADGE Beta]{type=Informative}支援營運見解問題 | [營運分析](../../ai-assistant/home.md#operational-insights) 是AI助理針對您的中繼資料物件產生的回答，包括計數、查閱和歷程影響。 操作深入分析不會檢視沙箱中的任何資料。 您可以詢問AI Assistant操作深入分析問題，例如： <ul><li>哪些目的地處於作用中狀態？</li><li>我有多少資料集？</li><li>列出即時歷程中使用的對象。</li></ul> 下列網域支援營運深入分析：屬性、受眾、資料流程、資料集、目的地、歷程、結構描述和來源。 |
| 存取AI助理 | 若要存取Experience Platform、Real-Time CDP和Journey Optimizer的AI助理，您必須新增至包含 **啟用AI助理** 和 **檢視營運分析** 許可權。 如需詳細資訊，請閱讀 [功能存取指南](../../ai-assistant/access.md). 您必須將Admin Console用於 [在Customer Journey Analytics中存取](https://experienceleague.adobe.com/en/docs/analytics-platform/using/ai-assistant?lang=en#feature-access). |

如需AI助理的詳細資訊，請閱讀 [AI助理總覽](../../ai-assistant/home.md).

## Experience Platform API 的驗證 {#authentication-platform-apis}

用於取得存取權杖的JWT方法現在已針對新整合淘汰，並替換為較簡單的OAuth伺服器對伺服器驗證方法。<p>![已反白顯示取得存取權杖的全新 OAuth 驗證方法。](/help/landing/images/api-authentication/oauth-authentication-method.png "已反白顯示取得存取權杖的全新 OAuth 驗證方法。"){width="100" zoomable="yes"}</p>

儘管使用 JWT 驗證方法的現有 API 整合將持續運作至 2025 年 1 月 1 日為止，但 Adob&#x200B;&#x200B;e 強烈建議您在該日期之前將現有整合移轉至新的 OAuth Server-to-Server 方法。請至「[從服務帳戶 (JWT) 認證移轉至 OAuth Server-to-Server 認證](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/)」詳閱指南。

## 資料準備 {#data-prep}

使用資料準備來對映、轉換和驗證與Experience Data Model (XDM)之間的資料。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 保留關鍵字清單的新增 | 下列字詞已新增至「資料準備」保留關鍵字清單：<ul><li>`do`</li><li>`empty`</li><li>`function`</li><li>`size`</li></ul> 如需詳細資訊，請閱讀 [資料準備函式指南](../../data-prep/functions.md). |

{style="table-layout:auto"}

如需「資料準備」的詳細資訊，請閱讀 [資料準備總覽](../../data-prep/home.md).

## 目的地 {#destinations}

[!DNL Destinations] 是預先建立的和目標平台的整合，可讓來自 Adobe Experience Platform 的資料順暢啟動。您可使用目的地啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新功能或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| ----------- | ----------- |
| 增強隨選匯出API，可匯出外部對象 | 您現在可以使用臨機匯出API來匯出外部（自訂上傳）對象。 [閱讀全文](/help/destinations/api/ad-hoc-activation-api.md) . |
| (Beta)匯出陣列支援Beta版階段所支援的其他函式 | 先前，將受眾啟用至檔案型目的地並選取「使用計算欄位」時，您只能使用資料準備中可用受眾的子集。 該限制現已解除，當將受眾匯出至檔案型目的地時，客戶可存取資料準備提供的所有功能。 [閱讀全文](/help/destinations/ui/export-arrays-calculated-fields.md#supported-functions)。 |
| 僅顯示含有對應步驟中資料的欄位 | 將設定檔屬性對應至目的地時，您現在可以在所有設定檔屬性之間切換，或僅切換包含資料的屬性。 依預設，僅顯示包含資料的欄位。 請參閱啟用指南，以瞭解 [批次](../../destinations/ui/activate-batch-profile-destinations.md#mapping) 和 [串流](../../destinations/ui/activate-segment-streaming-destinations.md#mapping) 目的地以取得更多詳細資料。 |

{style="table-layout:auto"}

如需有關目的地的詳細一般資訊，請參閱[目的地概觀](../../destinations/home.md)。

## 身分識別服務 {#identity-service}

使用Adobe Experience Platform Identity Service，透過跨裝置和系統橋接身分，讓您即時提供具影響力的個人數位體驗，進而建立客戶及其行為的全面檢視。

**即將推出的功能**

| 功能 | 說明 |
| --- | --- |
| [!BADGE Beta]{type=Informative}身分圖表連結規則 | Beta版計畫的參與者可以使用身分圖表連結規則，防止「共用裝置」和其他圖表摺疊情況，以確保系統中的個人實體表示方式。 為達成此目標，Beta版計畫中的參與者將可存取開發沙箱環境中的三項功能： <ul><li>圖表模擬工具，用於瞭解圖表演演算法的運作方式。</li><li>身分設定畫面可設定唯一的名稱空間和名稱空間優先順序。</li><li>可深入分析所擷取圖形的身分控制面板。</li></ul> 此外，Beta版計畫也包含設定檔行為穩定性的改善專案。 如需詳細資訊，請閱讀 [身分圖表連結規則](../../identity-service/identity-graph-linking-rules/overview.md) 檔案。 |

{style="table-layout:auto"}

如需Identity Service的詳細資訊，請參閱 [Identity Service總覽](../../identity-service/home.md).

## [!DNL Privacy Service] {#privacy}

幾項法律和組織法規授予使用者權利，讓使用者有權應要求從您的資料存放區存取或刪除其個人資料。 Adobe Experience Platform [!DNL Privacy Service] 提供RESTful API和使用者介面，協助您管理客戶的這些資料請求。 替換為 [!DNL Privacy Service]，您可以提交存取和刪除Adobe Experience Cloud應用程式中私人或個人客戶資料的請求，協助促進法律和組織隱私法規的自動合規性。

**新功能**

| 功能 | 說明 |
|--- | ---|
| Adobe Journey Optimizer的Privacy Service支援 | Privacy Service功能現在與Adobe Journey Optimizer通訊協定相容，以處理刪除請求。 請參閱 [Adobe Journey Optimizer隱私權請求檔案](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/requests) 以取得詳細資訊，或參閱以下清單的Experience Platform檔案： [Experience Cloud與Privacy Service整合的應用程式](../../privacy-service/experience-cloud-apps.md). |

請參閱 [Privacy Service概觀](../../privacy-service/home.md) 以取得服務的詳細資訊。

## Segmentation Service {#segmentation}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷的一群人的標準，從而定義設定檔的特定子集。區段的基礎可能是記錄資料 (例如人口統計資訊) 或表示客戶與您的品牌互動的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| 時間限制更新 | 「本月」和「今年」的行為已更新，現在分別代表「月至今」和「年初至今」。 如需此變更的詳細資訊，請參閱 [區段產生器指南](../../segmentation/ui/segment-builder.md#rule-builder-canvas). |

{style="table-layout:auto"}

如需有關 [!DNL Segmentation Service] 的詳細資訊，請參閱[分段概觀](../../segmentation/home.md)。

## 使用案例教戰手冊 {#use-case-playbooks}

[!DNL Use Case Playbooks] 所有Adobe Experience Platform客戶都可免費使用。 若要在Experience Platform UI中存取豐富的用例教戰手冊，您現在可以選擇 **[!UICONTROL 教戰手冊]** 從左側導覽。

[!DNL Use Case Playbooks] 專為在開始使用Real-time Customer Data Platform或Adobe Journey Optimizer時協助克服挑戰而設計。 即使您不確定從何處開始或是如何針對您的預期使用案例產生正確的資產，這類資產仍可提供指引，並產生各種資產，讓您可以在準備就緒時測試並匯入生產環境。

若要開始使用，請閱讀 [使用案例教戰手冊概覽](/help/use-case-playbooks/playbooks/overview.md)，此頁面會提供教戰手冊功能、用途的概觀，以及端對端示範，包括如何建立例項，並將產生的資產匯入其他沙箱環境。

若要瞭解如何存取及設定啟發性的沙箱，以實驗及探索各種使用案例教戰手冊，請參閱 [導覽至使用案例教戰手冊](/help/use-case-playbooks/playbooks/navigate.md) 檔案。

若要深入瞭解 [!DNL Use Case Playbooks]，請閱讀下列檔案頁面：

- 取得完整清單 [可用的教戰手冊](/help/use-case-playbooks/playbooks/playbooks-list.md)，依產品分組(Real-Time CDP或Journey Optimizer)。
- 瞭解內容 [許可權](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) 是您使用教戰手冊及其所建立資產的必要專案。
- 瞭解 [資料感知功能](/help/use-case-playbooks/playbooks/data-awareness.md) 這可讓您將產生的資產複製到其他沙箱環境。
