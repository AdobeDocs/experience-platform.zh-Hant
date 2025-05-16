---
title: Adobe Experience Platform 發行說明 (2025 年 4 月)
description: Adobe Experience Platform 2025 年 4 月版發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 6558046e9708267cd0ceda36e7c0bdba6b2f758a
workflow-type: tm+mt
source-wordcount: '2192'
ht-degree: 98%

---

# Adobe Experience Platform 發行說明

>[!TIP]
>
>如需其他 Adobe Experience Platform 應用程式的發行說明，請參閱以下文件：
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/releases/latest)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/zh-hant/docs/real-time-cdp-collaboration/using/latest)

**發行日期：2025 年 4 月 29 日**

Adobe Experience Platform 現有功能和文件的更新：

- [Experience League](#experience-league)
- [資料集合](#data-collection)
- [目標](#destinations)
- [體驗資料模型](#xdm)
- [身分識別服務](#identity)
- [查詢服務](#query-service)
- [即時客戶輪廓](#profile)
- [沙箱](#sandboxes)
- [來源](#sources)
- [使用案例教戰手冊](#use-case-playbooks)

## Experience League {#experience-league}

Experience League 是一個綜合性的學習平台，旨在協助您提升使用 Adobe 產品的技能。此平台提供各種資源，包括：課程、文件、社群頁面、活動，以及獲得認證的途徑。

| 功能 | 說明 |
| --- | --- |
| 個人化首頁 | 在[Experience League](https://experienceleague.adobe.com/zh-hant/home#)上存取及自訂您的個人化首頁。 使用您的 Adobe 認證登入，然後在頂端選單選取「**[!UICONTROL Experience League]**」，即可開始最佳化您的學習體驗： <ul><li>**書籤**：使用「[!UICONTROL 書籤]」功能，將您喜愛的資源儲存並收集在同一位置。您可以儲存各種內容，包括播放清單、文章及教學課程。</li><li>**自訂您的學習**：更新您的 Experience League 輪廓，選用最符合您需求的角色、產業、產品及經驗等級，進而提升您的學習體驗。</li><li>**推薦**：檢視根據您最近活動所推薦的學習內容。</li><li>**最近檢視的項目**：使用「[!UICONTROL 最近檢視的項目]」區段，快速導覽回最近檢視過的內容，例如文件和影片。</li><li>**學習資源**：使用「[!UICONTROL 所有學習資源]」面板，導覽至教學課程、文件、社群、活動及認證。</li><li>**最新資訊**：檢視「[!UICONTROL 最新資訊]」區段，了解 Experience League 的一系列最新內容。</li><li>**隨選觀看過往活動**：使用「[!UICONTROL 隨選觀看過往活動]」區段，觀看先前錄製的直播活動，包括產品焦點、使用案例與教學課程。</li></ul><br> ![Experience League 的個人化首頁。](../2025/assets/april/personalized-home-page.png "Experience League 的個人化首頁。"){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

## 資料集合 {#data-collection}

Adobe Experience Platform 提供了一套技術，可讓您收集用戶端的客戶體驗資料，並將其傳送到 Adobe Experience Platform Edge Network，然後在其中擴充及轉換資料，再分送至 Adobe 或非 Adobe 目標。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| [!DNL Adform] 擴充功能 | [!DNL Adform] 伺服器端擴充功能可讓品牌使用 ECID，在網站外輕鬆地重新定位客群。此伺服器端擴充功能不依賴第三方 Cookie 或 Cookie 替代 ID。此外，因為這完全是在伺服器端完成，因此不需要其他像素或其他用戶端變更。如需詳細資訊，請參閱 [Adform 擴充功能概觀](/help/tags/extensions/server/adform/overview.md)。 |
| [!DNL Amazon] 網頁事件 API 擴充功能 | [!DNL Amazon] Conversions API 擴充功能可讓廣告商直接與 [!DNL Amazon] 共用網站互動，從而改善歸因、資料可靠性及行銷活動最佳化成效。此擴充功能支援事件轉送，可讓您傳送轉換事件 (例如購買、加入購物車等)，同時確保正確的重複資料刪除處理，以獲得準確的報告結果。如需詳細資訊，請參閱 [Amazon 擴充功能概觀](/help/tags/extensions/server/amazon/overview.md)。 |

{style="table-layout:auto"}

## 目標 {#destinations}

[!DNL Destinations] 是預先建立的目標平台整合功能，能夠順暢啟用來自 Adobe Experience Platform 的資料。您可以使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、定向廣告和其他諸多使用案例。

**全新或已更新的目標** {#new-updated-destinations}

| 目標 | 說明 |
| --- | --- |
| [Marketo Engage Person Sync (人員同步)](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Adobe 已更新 [!DNL Marketo Engage Person Sync] 目標，以修正身分識別圖中存在多封電子郵件時，會對客戶造成影響的問題。 |
| [(V2) Pega CDH Realtime Audience (即時客群) 連線](/help/destinations/catalog/personalization/pega-v2.md) | 當您在 Pega 帳戶中設定了多個 Pega Customer Decision Hub 應用程式時，可使用 Adobe Experience Platform 中的 [!DNL (V2) Pega Customer Decision Hub Realtime Audience] 目標將輪廓屬性和客群會籍資料傳送至 Pega Customer Decision Hub，以決定下一步最佳行動。 |

**全新或更新版功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| --- | --- |
| **每週**&#x200B;和&#x200B;**每月**&#x200B;完整檔案匯出排程選項 | 從現在起，您可以為啟用至雲端儲存空間檔案型目標的人員和潛在客戶，設定每週或每月完整檔案匯出排程。[閱讀更多](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files)有關排程選項的資訊。 |

{style="table-layout:auto"}

**修正、增強功能及其他公告** {#destinations-fixes-and-enhancements}

- **資料集匯出結束日期的執行延遲至 2025 年 9 月 1 日**\
  在 [2024 年 9 月版本](/help/release-notes/2024/september-2024.md#destinations-new-updated-functionality)中，Adobe 將&#x200B;*在該版本之前*&#x200B;建立之任何資料集匯出資料流的預設結束日期設定為 2025 年 5 月 1 日。Adobe 現已將此執行期限延長至 **2025 年 9 月 1 日**，為客戶提供更多時間更新其排程。如需有關如何編輯資料集匯出資料流結束日期的資訊，請參閱[匯出資料集教學課程](../../destinations/ui/export-datasets.md#schedule-dataset-export)的排程區段。

- **已改善 LiveRamp Onboarding 的 SFTP 傳輸失敗處理方式**\
  Adobe 已修正一項會影響透過 SFTP 將檔案匯出至 [LiveRamp Onboarding](/help/destinations/catalog/advertising/liveramp-onboarding.md) 目標的問題。之前，由於暫時性的伺服器端問題，檔案傳輸偶爾會失敗，且失敗嘗試產生的暫存檔案會保留在伺服器上。這些無法刪除的檔案會阻擋後續重試，因為 Adobe 沒有權限覆寫這些檔案。\
  修正後，如果重試無法刪除暫存檔案，Adobe 將產生一個含附加字尾 `attempt2` 的新檔案，以確保重試成功完成。

## 體驗資料模型 (XDM，Experience Data Model) {#xdm}

XDM 是一種開放原始碼的規格，可為帶入 Adobe Experience Platform 的資料提供通用結構和定義 (結構描述)。若遵守 XDM 標準，即可將所有客戶體驗資料合併為單一常用表述，以更快速、更整合的方式提供分析洞察。您可以從客戶行為中獲得有價值的分析洞察、透過區段定義客戶客群，並基於個人化目的使用客戶屬性。

**已更新的 XDM 元件**

| 功能 | 說明 |
| --- | --- |
| 字串欄位的最小長度值預設為 1 | 新字串欄位的最小長度會預設為 1。仍可接受非必填欄位為 Null 值。如需更多有關最佳實務的資訊，請閱讀[資料建模最佳實務](../../xdm/schema/best-practices.md#data-integrity-tips)指南 |

{style="table-layout:auto"}

如需有關 Experience Platform 中 XDM 的詳細資訊，請參閱 [XDM 系統概觀](../../xdm/home.md)。

## 身分識別服務 {#identity}

Adobe Experience Platform 身分識別服務可在裝置及系統間進行身分識別橋接，進而建立客戶及其行為的全貌，協助您即時提供個人化且具影響力的數位體驗。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 開發沙箱中的所有客戶現在都可以存取[!BADGE 有限可用性]{type=Informative} [!DNL Identity Graph Linking Rules]身分圖表連結規則。 <ul><li>**啟用要求**：此功能將維持非使用中，直到您設定並儲存 [!DNL Identity Settings] 為止。若未進行此設定，系統將繼續正常運作，行為不會有任何變化。</li><li>**重要說明**：在此限量開放階段，邊緣分段可能會產生非預期的分段會籍結果。但是，串流和批次分段將按預期運作。</li><li>**後續步驟**：如需有關如何在生產沙箱中啟用此功能的資訊，請聯絡您的 Adobe 帳戶團隊。</li></ul> |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[[!DNL Identity Graph Linking Rules] 文件](../../identity-service/identity-graph-linking-rules/overview.md)。

## 查詢服務 {#query-service}

「查詢服務」可讓您使用標準 SQL，在 Adobe Experience Platform 資料湖查詢資料。您可以順暢無礙地合併資料集，並根據查詢結果建立新資料集，以支援報表產出、啟用資料科學工作流程，或協助攝取至即時客戶輪廓。例如，您可以合併客戶交易資料與行為資料，以找出高價值客群進行精準行銷活動。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| SQL 客群覆寫 | 使用新 SQL 查詢的結果覆寫現有輪廓，以重新整理客群會籍。如此一來，您就能在單一操作中移除過時的記錄並插入更新的記錄，以更有效地管理動態客群。如需詳細資訊，請參閱 [SQL 客群擴充功能指南](../../query-service/data-distiller-audiences/overview.md#replace-audience)。 |
| 下載並複製查詢結果 | [直接從查詢編輯器將查詢結果下載](../../query-service/ui/overview.md#download-query-results)為 CSV、XLSX 或 JSON 檔案，或者[將結果複製到剪貼簿](../../query-service/ui/overview.md#copy-results)作為逗號分隔值 (CSV)，以便在 Excel 等試算表應用程式中快速使用。這些增強功能可簡化離線分析、報告及資料驗證工作流程。 |
| 全螢幕檢視查詢結果 | [在全螢幕對話框中預覽查詢結果](../../query-service/ui/overview.md#view-results)，以改善可讀性、輕鬆瀏覽大型資料集，並選取要複製的列。全螢幕檢視提供可調整大小的網格版面，協助您更有效率地檢閱寬表格和詳細輸出內容。 |
| 模型預測中的增強欄選擇 | 使用擴充的 `model_predict` 語法選取特定欄，並套用別名。獲取中繼預測結果，例如功能向量和機率分數。增強選擇功能需啟用功能標幟。請參閱[模型生命週期文件](../../query-service/advanced-statistics/models.md#select-specific-output-fields)，以了解語法範例和功能標幟的詳細資訊。 |
| 使用 CREATE TABLE 和 INSERT INTO 儲存模型預測輸出 | [使用 CREATE TABLE AS SELECT 將選取的預測輸出儲存至新表格，或使用 INSERT INTO SELECT 插入現有表格](../../query-service/advanced-statistics/models.md#predict)。若已啟用增強欄選擇功能，則功能向量和機率等中繼結果也可以與最終預測一起保留。如需使用範例，請參閱 [SQL 語法文件](../../query-service/sql/syntax.md#create-table-as-select)。 |

若需更多有關 [!DNL Query Service] 的資訊，請參閱 [[!DNL Query Service] 概觀](../../query-service/home.md)。

## 即時客戶輪廓 {#profile}

Adobe Experience Platform 可讓您為客戶提供協調一致且相關的體驗，無論他們何時何地與您的品牌互動。即時客戶輪廓會合併來自多個管道的資料 (包括線上、離線、CRM 和協力廠商資料)，讓您可以掌握每位個別客戶的全貌。「輪廓」可讓您將客戶資料合併為統一視圖，以針對每次客戶互動留下可做為行動依據、並附有時間戳記的說明。

| 功能 | 說明 |
| ------- | ----------- |
| 匿名輪廓資料期限 | 在「輪廓」儀表板中管理您的匿名輪廓資料期限。若要了解更多有關此功能和匿名輪廓的資訊，請閱讀[匿名輪廓資料期限指南](../../profile/pseudonymous-profiles.md)。 |

{style="table-layout:auto"}

若要了解更多有關即時客戶輪廓的資訊，請閱讀[輪廓概觀](../../profile/home.md)

## 沙箱 {#sandboxes}

Adobe Experience Platform 旨在協助您在全球各地打造更豐富的數位體驗應用程式。公司經常需要並行執行多個數位體驗應用程式，且在顧及這些應用程式的開發、測試和部署等需求的同時，也必須確保營運合規性。為了滿足這種需求，Experience Platform 提供的沙箱可將單一 Experience Platform 執行個體分割成個別的虛擬環境，以協助開發並改進數位體驗應用程式。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 沙箱工具外掛程式支援擴充 | 現在起，在沙箱工具中複製 Journey 物件時，可將自訂動作作為相依物件一併複製。此外，您可以選取現有動作，以在目標沙箱中重複使用。它們也可以獨立新增至到封裝中。如需有關受支援 Adobe Journey Optimizer 物件的完整資訊，請閱讀[沙箱工具](../../sandboxes/ui/sandbox-tooling.md#adobe-journey-optimizer-objects)指南。 |

{style="table-layout:auto"}

如需有關沙箱的詳細資訊，請閱讀[沙箱概觀](../../sandboxes/home.md)。

## 來源 {#sources}

Experience Platform 提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證，並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間，並管理資料攝取輸送量。

使用 Experience Platform 中的來源，即可從 Adobe 應用程式或第三方資料來源攝取資料。

**新的來源**

| 功能 | 說明 |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Algolia User Profiles] | [[!DNL Algolia User Profiles]](../../sources/connectors/data-partners/algolia-user-profiles.md) 來源現已可用。使用此來源，即可將 [!DNL Algolia] 使用者輪廓親和原則資料帶入 Experience Platform。接著，您可以使用這些資料，為網站、電子商務平台及應用程式提供高效能搜尋解決方案，以改善使用者參與度、轉換率及整體客戶體驗。如需詳細資訊，請閱讀有關如何[攝取 [!DNL Algolia User Profiles] 資料至 Experience Platform](../../sources/tutorials/ui/create/data-partners/algolia-user-profiles.md) 的指南。 |
| [!BADGE Beta]{type=Informative} [!DNL Azure Databricks] 的 API 支援 | [!DNL Azure Databricks] 來源現在已可在 API 中使用。使用 [!DNL Flow Service] API 可連結您的 [!DNL Databricks] 帳戶，並將您的 [!DNL Databricks] 資料帶至 Experience Platform。如需詳細資訊，請閱讀有關 [[!DNL Azure Databricks]](../../sources/connectors/databases/databricks.md) 的文件。 |

{style="table-layout:auto"}

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| XDM 欄位已更新，可將串流媒體資料攝取至 Experience Platform。 | 全新的 XDM 欄位群組 (`mediaReporting`) 現已推出，可透過 Adobe Analytics 來源將串流媒體資料攝取至 Experience Platform。此欄位會取代 `media.mediaTimed` 欄位。</br> <br>在三個月的過渡期間內，`media.mediaTimed` 欄位的資料攝取功能將持續運作。但是，在 2025 年 7 月底，`media.mediaTimed` 欄位就會完全棄用，也不會再顯示於 Experience Platform Schema UI 中，且資料只會透過 `mediaReporting` 欄位傳送。</br><br>如果您已在 2025 年 4 月 22 日之前實作 Analytics 來源，將串流媒體資料收集至 Platform，就必須移轉您的現有設定，才能使用新欄位群組傳送資料。此移轉必須在 2025 年 7 月底前完成。請聯絡您的 Adobe 帳戶團隊以取得移轉支援。 |
| [!DNL MariaDB] 和 [!DNL PostgreSQL] 的新驗證類型 | 現在起，您可以使用基本驗證，在 Experience Platform 上驗證您的 [!DNL MariaDB] 和 [!DNL PostgreSQL] 來源。請閱讀下列文件以了解更多資訊： <ul><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL PostgreSQL]](../../sources/connectors/databases/postgres.md) |
| [!DNL Amazon Redshift] 的列層級篩選支援 | 對於您在 Experience Platform 上的 [!DNL Amazon Redshift] 資料，您可以使用列層級篩選功能。如需詳細資訊，請閱讀[針對 API 中的來源篩選列層級資料](../../sources/tutorials/api/filter.md)指南。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[來源概觀](../../sources/home.md)。

## 使用案例教戰手冊 {#use-case-playbooks}

「使用案例教戰手冊」最初旨在協助克服開始使用 Real-Time Customer Data Platform 或 Adobe Journey Optimizer 時遇到的挑戰。它們不斷發展，現已成為讓您快速開始關鍵行銷使用案例的利器，並提供靈感和預先建立的資產，協助您進行測試並進入生產階段。

「使用案例教戰手冊」已經從探索工具轉換為協作框架。現在，它們可協助您在不同的組織之間建置、管理及分享您自己的教戰手冊。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| [!BADGE Beta]{type=Informative} 製作並分享您自己的教戰手冊 | 全新教戰手冊製作框架可讓您建立、管理和分享您自己的使用案例教戰手冊。這包括支援擷取關鍵中繼資料、編輯歷程圖，以及與相關的技術資產建立關聯。您可以在組織之間分享教戰手冊，將行銷方法標準化並保持一致性。 |

{style="table-layout:auto"}

若要了解如何製作和分享自己的教戰手冊，請閱讀[製作和分享您自己的教戰手冊](/help/use-case-playbooks/playbooks/author.md)文件。

如需更多資訊，請閱讀[使用案例教戰手冊概觀](/help/use-case-playbooks/playbooks/overview.md)，其中提供教戰手冊的功能概觀、用途及端對端示範，包括如何建立實例以及將產生的資產匯入其他沙箱環境。
