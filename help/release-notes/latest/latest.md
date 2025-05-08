---
title: Adobe Experience Platform 發行說明 (2025 年 4 月)
description: Adobe Experience Platform 2025 年 4 月版發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: a79efc5d64862850d17cff0fd0633c73fd08207d
workflow-type: tm+mt
source-wordcount: '2197'
ht-degree: 29%

---

# Adobe Experience Platform 發行說明

>[!TIP]
>
>如需其他Adobe Experience Platform應用程式的發行說明，請參閱下列檔案：
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/zh-hant/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/zh-hant/docs/analytics-platform/using/releases/latest)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/zh-hant/docs/real-time-cdp-collaboration/using/latest)

**發行日期： 2025年4月29日**

Adobe Experience Platform 現有功能和文件的更新：

- [Experience League](#experience-league)
- [資料集合](#data-collection)
- [目的地](#destinations)
- [體驗資料模式](#xdm)
- [身分識別服務](#identity)
- [查詢服務](#query-service)
- [即時客戶設定檔](#profile)
- [沙箱](#sandboxes)
- [來源](#sources)
- [使用案例教戰手冊](#use-case-playbooks)

## Experience League {#experience-league}

Experience League是全方位的學習平台，旨在協助您增強Adobe產品的技能。 它提供各種資源，包括：課程、檔案、社群頁面、活動，以及存取認證。

| 功能 | 說明 |
| --- | --- |
| 個人化首頁 | 在[Experience League](https://experienceleague.adobe.com/zh-hant/home#)上存取及自訂您的個人化首頁。 使用您的Adobe認證登入，然後在頂端選單上選取「**[!UICONTROL Experience League]**」以開始最佳化您的學習體驗： <ul><li>**書籤**：使用[!UICONTROL 書籤]功能，將您最愛的資源儲存在同一處，並加以收集。 您可以儲存各種內容，包括播放清單、文章和教學課程。</li><li>**自訂您的學習**：使用最符合您需求的角色、產業、產品和體驗層級，更新您的Experience League設定檔，以增強您的學習體驗。</li><li>**建議**：檢視根據您最近活動建議的學習內容。</li><li>**最近檢視的專案**：使用[!UICONTROL 最近檢視的專案]區段可快速導覽回最近檢視的內容，例如檔案和影片。</li><li>**學習資源**：使用[!UICONTROL 所有學習資源]面板，導覽至教學課程、檔案、社群、活動和認證。</li><li>**新增功能**：檢視[!UICONTROL 新增功能]區段，瞭解Experience League上最新內容的資料流。</li><li>**隨選觀看過去的活動**：透過[!UICONTROL 隨選觀看過去的活動]區段，在產品聚光燈、使用案例和教學課程上觀看先前錄製的即時資料流。</li></ul><br> ![Experience League的個人化首頁。在Experience League上](../2025/assets/april/personalized-home-page.png "個人化首頁。"){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

## 資料彙集 {#data-collection}

Adobe Experience Platform 提供了一套技術，讓您可收集用戶端客戶體驗資料並將其傳送到 Adobe Experience Platform Edge Network，在其中可擴充、轉換資料並將其分送至 Adobe 或非 Adobe 目標。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| [!DNL Adform] 擴充功能 | [!DNL Adform]伺服器端擴充功能可讓品牌使用ECID輕鬆在站外重新鎖定對象。 此伺服器端擴充功能不依賴第三方Cookie或Cookie替代ID。 此外，由於這完全是在伺服器端完成，因此不需要進行額外的畫素或其他使用者端變更。 如需詳細資訊，請參閱[Adform擴充功能概觀](/help/tags/extensions/server/adform/overview.md)。 |
| [!DNL Amazon]網頁事件API延伸模組 | [!DNL Amazon] Conversions API擴充功能可讓廣告商直接與[!DNL Amazon]共用網站互動，進而改善歸因、資料可靠性和行銷活動最佳化。 此擴充功能支援事件轉送，可讓您傳送購買、購物車新增等轉換事件，同時確保適當的重複資料刪除功能，以便產生準確的報告。 如需詳細資訊，請參閱[Amazon擴充功能概觀](/help/tags/extensions/server/amazon/overview.md)。 |

{style="table-layout:auto"}

## 目標 {#destinations}

[!DNL Destinations] 是與目標平台的預先建立整合，能夠順暢啟用來自 Adobe Experience Platform 的資料。您可以使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、定向廣告和其他諸多使用案例。

**新的或更新目的地** {#new-updated-destinations}

| 目標 | 說明 |
| --- | --- |
| [Marketo Engage人員同步](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Adobe已更新[!DNL Marketo Engage Person Sync]目的地，以修正身分對應中出現多封電子郵件時影響客戶的問題。 |
| [(V2) Pega CDH即時對象連線](/help/destinations/catalog/personalization/pega-v2.md) | 當您在Pega帳戶中設定了多個Pega客戶決策中心應用程式時，請在Adobe Experience Platform中使用[!DNL (V2) Pega Customer Decision Hub Realtime Audience]目的地，將設定檔屬性和對象會籍資料傳送至Pega客戶決策中心，以進行次佳動作決策。 |

**全新或更新版功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| --- | --- |
| 完整檔案匯出的&#x200B;**每週**&#x200B;和&#x200B;**每月**&#x200B;排程選項 | 現在當您啟用至雲端儲存體檔案型目的地時，可以排程每週或每月為人員和潛在客戶對象完整檔案匯出。 [閱讀更多有關排程選項的](/help/destinations/ui/activate-batch-profile-destinations.md#export-full-files)。 |

{style="table-layout:auto"}

**修正、增強功能和其他公告** {#destinations-fixes-and-enhancements}

- **強制資料集匯出結束日期延遲至2025年9月1日**\
  在[2024年9月](/help/release-notes/2024/september-2024.md#destinations-new-updated-functionality)版本中，Adobe針對在該版本之前&#x200B;*建立的任何資料集匯出資料流，將預設結束日期設為2025年5月1日*。 Adobe現在正將強制期限延長至&#x200B;**2025年9月1日**，讓客戶有更多時間更新其排程。 如需如何編輯資料集匯出資料流結束日期的詳細資訊，請參閱[匯出資料集教學課程](../../destinations/ui/export-datasets.md#schedule-dataset-export)的排程區段。

- **改善處理LiveRamp上線的失敗SFTP傳輸**\
  Adobe已針對影響透過SFTP將檔案匯出至[LiveRamp上線](/help/destinations/catalog/advertising/liveramp-onboarding.md)目的地的問題實作修正。 有時候，檔案傳輸會因為暫時性的伺服器端問題而失敗，而嘗試失敗的暫存檔案會留在伺服器上。 這些無法刪除的檔案會封鎖後續的重試，因為Adobe沒有覆寫這些檔案的許可權。\
  透過此修正，如果重試嘗試無法刪除暫存檔，Adobe將會產生附加尾碼`attempt2`的新檔案，以確保重試成功完成。

## 體驗資料模式 (XDM) {#xdm}

XDM 是一種開放原始碼的規格，可為帶到 Adobe Experience Platform 中的資料提供通用結構和定義 (結構描述)。若遵守 XDM 標準，即可將所有客戶體驗資料合併到一個常用表述中，以更快速、更整合的方式傳遞分析。您可以從客戶行為中獲得有價值的分析，透過區段定義客戶客群，並使用客戶屬性實現個人化的目的。

**已更新的 XDM 元件**

| 功能 | 說明 |
| --- | --- |
| 字串欄位會收到最小值1 | 新字串欄位預設會有一個最小長度。 仍可接受非必要欄位的Null值。 如需最佳實務的詳細資訊，請閱讀[資料模型最佳實務](../../xdm/schema/best-practices.md#data-integrity-tips)的指南 |

{style="table-layout:auto"}

如需有關 Experience Platform 中 XDM 的詳細資訊，請參閱 [XDM 系統概觀](../../xdm/home.md)。

## 身分識別服務 {#identity}

使用 Adobe Experience Platform 身分識別服務，可在裝置及系統間進行身分識別橋接來建立客戶及其行為的全方位檢視，進而讓您即時實現具影響力的個人數位體驗。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| [!BADGE 有限可用性]{type=Informative} [!DNL Identity Graph Linking Rules] | 身分圖表連結規則現在處於「有限可用性」，可供開發沙箱中的所有客戶存取。 <ul><li>**啟用需求**：在您設定並儲存[!DNL Identity Settings]之前，此功能將保持非使用中狀態。 若沒有此設定，系統將繼續正常運作，且行為不會有任何變更。</li><li>**重要附註**：在此「有限可用性」階段期間，Edge區段可能會產生非預期的區段會籍結果。 不過，串流和批次區段將如預期運作。</li><li>**後續步驟**：如需如何在生產沙箱中啟用此功能的詳細資訊，請聯絡您的Adobe客戶團隊。</li></ul> |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[[!DNL Identity Graph Linking Rules] 檔案](../../identity-service/identity-graph-linking-rules/overview.md)。

## 查詢服務 {#query-service}

使用具備查詢服務的標準 SQL，在 Adobe Experience Platform 資料湖查詢資料。從您的查詢結果來促進報告、啟用資料科學工作流程或協助擷取至即時客戶輪廓，以順暢無礙地合併資料集和產生新資料集。例如，您可以將客戶交易資料與行為資料合併，以確定具目標性之行銷活動的高價值客群。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| SQL對象覆寫 | 使用新SQL查詢的結果覆寫現有設定檔，以重新整理對象成員資格。 這可讓您移除過時的記錄，並在單一操作中插入更新的記錄，藉此更有效率地管理動態對象。 如需詳細資訊，請參閱[SQL對象擴充功能指南](../../query-service/data-distiller-audiences/overview.md#replace-audience)。 |
| 下載並複製查詢結果 | [直接從[查詢編輯器]下載查詢結果](../../query-service/ui/overview.md#download-query-results)為CSV、XLSX或JSON檔案，或[將結果複製到剪貼簿](../../query-service/ui/overview.md#copy-results)為逗號分隔值(CSV)，以便快速用於Excel等試算表應用程式。 這些增強功能可簡化離線分析、報告和資料驗證工作流程。 |
| 以全熒幕檢視查詢結果 | [在全熒幕對話方塊中預覽查詢結果](../../query-service/ui/overview.md#view-results)可改善可讀性、輕鬆掃描大型資料集，並選取要複製的列。 全熒幕檢視提供可調整大小的格線版面配置，協助您更有效率地檢視寬表格和詳細輸出。 |
| 增強模型預測中的欄選擇 | 使用延伸`model_predict`語法選取特定資料行並套用別名。 擷取中繼預測結果，例如特徵向量和機率分數。 增強型選擇需要功能標幟啟用。 如需語法範例和功能標幟詳細資訊，請參閱[模型生命週期檔案](../../query-service/advanced-statistics/models.md#select-specific-output-fields)。 |
| 使用CREATE TABLE和INSERT INTO儲存模型預測輸出 | [使用CREATE TABLE AS SELECT將選取的預測輸出儲存到新資料表，或使用INSERT INTO SELECT插入現有資料表](../../query-service/advanced-statistics/models.md#predict)。 如果啟用了增強欄選擇，則中間結果（例如特徵向量和概率）也可以與最終預測一起保留。 如需使用範例，請參閱[SQL語法檔案](../../query-service/sql/syntax.md#create-table-as-select)。 |

如需更多有關 [!DNL Query Service] 的資訊，請參閱[[!DNL Query Service] 概觀](../../query-service/home.md)。

## 即時客戶設定檔 {#profile}

Adobe Experience Platform 讓您能夠為客戶提供一致且相關的協調體驗，無論他們何時何地與您的品牌互動。透過即時客戶設定檔，您可查看每個個別客戶合併了多個管道的資料 (包括線上、離線、CRM 和協力廠商資料) 的整體檢視。 設定檔可讓您將客戶資料合併成統一的檢視畫面，針對每個客戶互動提供可採取行動且附有時間戳記的說明。

| 功能 | 說明 |
| ------- | ----------- |
| 匿名設定檔資料到期 | 在設定檔控制面板中管理您匿名的設定檔資料有效期。 若要了解有關此功能和匿名輪廓的詳細資訊，請閱讀[匿名輪廓資料期限指南](../../profile/pseudonymous-profiles.md)。 |

{style="table-layout:auto"}

若要深入了解即時客戶設定檔，請閱讀[設定檔概觀](../../profile/home.md)

## 沙箱 {#sandboxes}

Adobe Experience Platform 是為了在全球規模上使數位體驗應用程式更加豐富而打造。公司經常要並行執行多個數位體驗應用程式，且在顧及這些應用程式的開發、測試和部署等需求的同時，也必須確保營運合規性。為了滿足這種需求，Experience Platform 提供的沙箱可將單一 Experience Platform 執行個體分割成個別的虛擬環境，以協助開發並改進數位體驗應用程式。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 沙箱工具外掛程式支援擴展 | 在沙箱工具中複製Journey物件時，現在可以將自訂動作復製為相依物件。 此外，您可以選取要在目標沙箱中重複使用的現有動作。 它們也可以獨立新增到套件中。 如需有關受支援的Adobe Journey Optimizer物件的完整資訊，請閱讀[沙箱工具](../../sandboxes/ui/sandbox-tooling.md#adobe-journey-optimizer-objects)指南。 |

{style="table-layout:auto"}

如需有關沙箱的詳細資訊，請閱讀[沙箱概觀](../../sandboxes/home.md)。

## 來源 {#sources}

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間並管理資料攝取輸送量。

使用 Experience Platform 中的來源，即可從 Adobe 應用程式或第三方資料來源攝取資料。

**新的來源**

| 功能 | 說明 |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Algolia User Profiles] | [[!DNL Algolia User Profiles]](../../sources/connectors/data-partners/algolia-user-profiles.md)來源現已可用。 使用此來源將您的[!DNL Algolia]使用者設定檔相關性資料帶入Experience Platform。 接著，您可以運用這些資料，為網站、電子商務平台和應用程式提供高效能搜尋解決方案，以改善使用者參與度、轉換率和整體客戶體驗。 如需詳細資訊，請閱讀如何[擷取 [!DNL Algolia User Profiles] 資料至Experience Platform](../../sources/tutorials/ui/create/data-partners/algolia-user-profiles.md)的指南。 |
| [!DNL Azure Databricks]的[!BADGE Beta]{type=Informative} API支援 | [!DNL Azure Databricks]來源現在可在API中使用。 使用[!DNL Flow Service] API連線您的[!DNL Databricks]帳戶，並將您的[!DNL Databricks]資料帶入Experience Platform。 如需詳細資訊，請參閱[[!DNL Azure Databricks]](../../sources/connectors/databases/databricks.md)上的檔案。 |

{style="table-layout:auto"}

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 更新XDM欄位，以將串流媒體資料擷取到Experience Platform。 | 新的XDM欄位群組`mediaReporting`現在可以透過Adobe Analytics來源將串流媒體資料擷取到Experience Platform。 此欄位取代`media.mediaTimed`欄位。</br> <br>在三個月的過渡期間，`media.mediaTimed`欄位上的資料擷取將繼續。 但在2025年7月底，`media.mediaTimed`欄位將完全過時且不再顯示在Experience Platform結構描述UI中，而且只會使用`mediaReporting`欄位傳送資料。</br><br>如果您已在2025年4月22日之前實施Analytics來源以將串流媒體資料收集到Platform，則必須移轉現有設定以使用新欄位群組傳送資料。 此移轉必須在2025年7月底前完成。 如需移轉支援，請連絡您的Adobe客戶團隊。 |
| [!DNL MariaDB]和[!DNL PostgreSQL]的新驗證型別 | 您現在可以使用基本驗證來驗證您在Experience Platform上的[!DNL MariaDB]和[!DNL PostgreSQL]來源。 如需詳細資訊，請參閱下列檔案： <ul><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL PostgreSQL]](../../sources/connectors/databases/postgres.md) |
| [!DNL Amazon Redshift]的資料列層級篩選支援 | 您可以在Experience Platform上對[!DNL Amazon Redshift]資料使用列層級篩選功能。 如需詳細資訊，請閱讀[篩選API](../../sources/tutorials/api/filter.md)中來源的資料列層級資料的指南。 |

{style="table-layout:auto"}

請閱讀[來源概觀](../../sources/home.md)以了解更多資訊。

## 使用案例教戰手冊 {#use-case-playbooks}

使用案例教戰手冊最初旨在協助克服開始使用Real-Time Customer Data Platform或Adobe Journey Optimizer時的挑戰。 它們持續發展，現在可讓您快速開始主要行銷使用案例，並提供靈感和預先建立的資產，以測試並投入生產。

使用案例教戰手冊已從探索工具轉換為合作框架。 現在，他們可以協助您在不同組織間建立、管理和共用自己的教戰手冊。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| [!BADGE Beta]{type=Informative}作者並分享您自己的教戰手冊 | 新的Playbook編寫架構可讓您建立、管理和分享您自己的使用案例教戰手冊。 這包括擷取關鍵中繼資料、編輯歷程地圖和關聯相關技術資產的支援。 您可以跨組織共用教戰手冊，以標準化行銷方法並維持一致性。 |

{style="table-layout:auto"}

若要瞭解如何編寫和分享您自己的行動手冊，請閱讀[編寫和分享您自己的行動手冊](/help/use-case-playbooks/playbooks/author.md)檔案。

如需詳細資訊，請閱讀[使用案例行動手冊概觀](/help/use-case-playbooks/playbooks/overview.md)，其中提供行動手冊的功能、用途和端對端示範的概觀，包括如何建立執行個體和將產生的資產匯入其他沙箱環境。
