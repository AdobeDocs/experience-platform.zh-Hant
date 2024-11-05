---
title: Adobe Experience Platform 發行說明 (2024 年 10 月)
description: Adobe Experience Platform 2024 年 10 月版發行說明。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: f30a124a40928abf69366d311131e353c2779191
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 78%

---

# Adobe Experience Platform 發行說明

**發行日期：2024 年 10 月 29 日**

Adobe Experience Platform 現有功能及文件的更新：

- [儀表板](#dashboards)
- [資料彙集](#data-collection-)
- [目標](#destinations)
- [分段服務](#segmentation-service)
- [沙箱](#sandboxes)
- [來源](#sources)

## 儀表板 {#dashboards}

Experience Platform 提供多個儀表板，您可以透過這些儀表板檢視每日快照期間擷取之組織資料的重要分析。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 資料Distiller範本 | 探索多個範本，以取得對象資料的結構化深入分析。 使用如&#x200B;**進階[!UICONTROL 對象重疊]**、**[!UICONTROL 對象比較]**、**[!UICONTROL 對象趨勢]**&#x200B;和&#x200B;**[!UICONTROL 對象身分重疊]**&#x200B;等控制面板，以做出資料導向式決策、最佳化細分並增強參與策略。 如需詳細資訊，請參閱[資料Distiller範本指南](../../dashboards/sql-insights-query-pro-mode/templates/overview.md)。 |
| 進階客群重疊 | 快速分析特定對象的對象交集，或檢視所有重疊，以發掘整個對象集中的寶貴見解。 運用這些見解來調整細分、減少多餘的訊息，並建立更有針對性的行銷活動，以提升行銷效率。 如需詳細資訊，請參閱[進階對象重疊指南](../../dashboards/sql-insights-query-pro-mode/templates/overlaps.md)。 |
| 對象比較增強功能 | 使用&#x200B;**對象比較**&#x200B;儀表板，檢視不同對象群組之間的關鍵量度並排比較。 利用此控制面板，您可以選取特定時間範圍和KPI （例如對象人數和身分構成），針對對象細分和鎖定目標策略做出更明智的決策。 如需詳細資訊，請參閱[對象比較指南](../../dashboards/sql-insights-query-pro-mode/templates/comparison.md)。 |
| 對象趨勢視覺效果 | 使用&#x200B;**[!UICONTROL 對象趨勢]**&#x200B;儀表板分析一段時間內的對象量度。 將對象規模、身分數和單一身分設定檔數的趨勢視覺化，協助您監控對象演變、衡量成長情況，並調整參與策略。 如需詳細資訊，請參閱[對象趨勢指南](../../dashboards/sql-insights-query-pro-mode/templates/trends.md)。 |
| 身分重疊分析 | 使用&#x200B;**[!UICONTROL 對象身分重疊]**&#x200B;儀表板，分析所選對象中的身分重疊。 檢視身分趨勢和劃分，以瞭解對象中不同的身分型別如何產生關聯，進而增強身分拼接並改善客戶細分準確性。 如需詳細資訊，請參閱[對象身分重疊指南](../../dashboards/sql-insights-query-pro-mode/templates/identity-overlaps.md)。 |

{style="table-layout:auto"}

如需有關儀表板的詳細資訊，包括如何授予存取權限和建立自訂 Widget，請先詳閱[儀表板概觀](../../dashboards/home.md)。

## 資料彙集 {#data-collection}

Adobe Experience Platform 提供了一套技術，可讓您收集用戶端客戶體驗資料並將其傳送至 Experience Platform Edge Network；資料可在 Experience Platform Edge Network 中擴充和轉換，以及分送至 Adobe 或非 Adobe 目標。

**新功能**

| 類型 | 功能 | 說明 |
| --- | --- | --- |
| 標籤和擴充功能 | Adobe Analytics JSON 檢視 | 您現在可以使用 Adobe Analytics 標籤擴充功能，以 JSON 格式檢查 eVar、prop 和事件設定；這些內容現在能夠包含在 Web SDK 擴充功能中，並匯出以進行編輯。您也可以上傳或複製此資料，並將其儲存在您的裝置上。如需詳細資訊，請參閱 [Adobe Analytics 擴充功能文件](../../tags/extensions/client/analytics/overview.md)。 |

{style="table-layout:auto"}

如需詳細資訊，請參閱[資料彙集概觀](../../collection/home.md)。

## 目標 {#destinations}

[!DNL Destinations] 是預先建立的和目標平台的整合，可讓來自 Adobe Experience Platform 的資料順暢啟動。您可使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新功能或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| ----------- | ----------- |
| [陣列匯出支援已正式推出](../../destinations/ui/export-arrays-calculated-fields.md) | 現在，所有客戶都能夠使用&#x200B;**[!UICONTROL 新增計算欄位]**&#x200B;選項來匯出整個陣列或陣列中的元素 (將客群啟用&#x200B;*至檔案型目標*&#x200B;時)。請注意，您仍然需要使用 `array_to_string` 函數將陣列扁平化為目標檔案中的字串。<br> ![新增附帶函數及欄位的計算欄位選項。](../2024/assets/october/array-export.gif "新增附帶 array_to_string 函數及組織陣列選項的計算欄位。"){width="250" align="center" zoomable="yes"} |
| [增強串流目標的報告準確性](/help/destinations/ui/export-datasets.md) | 自 2024 年 10 月開始，Adobe 推出更新以提高串流目標的報告準確性。此增強功能可確保 Experience Platform 和目標平台報告之間達到更佳的一致性。<br>在此更新之前，**[!UICONTROL 失敗的身分]**&#x200B;包含了所有的啟用重試。此更新後，總計數中僅會包含最後一次啟用重試。<br>此增強功能目前僅適用於 [Google 目標客戶比對目標](../../destinations/catalog/advertising/google-customer-match.md)，但會逐步擴大至其他 Experience Platform 的串流目標。此增強功能之後，[Google 目標客戶比對目標](../../destinations/catalog/advertising/google-customer-match.md)的使用者應該會發現&#x200B;**[!UICONTROL 失敗的身分]**&#x200B;計數有所下降。 |
| 彈性客群評估對[批次客群啟用](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files)的影響 | 若您對原已設定為在區段評估後啟用的客群，執行[彈性客群評估](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation)，則一旦彈性客群評估工作完成，無論先前的每日啟用工作為何，這些客群都會立即啟用。<br>視您的動作而定，這可能會導致一天多次匯出客群。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[目標概觀](../../destinations/home.md)。

## 分段服務 {#segmentation-service}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷的一群人的標準，從而定義輪廓的特定子集。區段的基礎可能是記錄資料 (例如人口統計資訊) 或表示客戶與您的品牌互動的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| [!BADGE 有限可用性]{type=Informative} 彈性客群評估 | 彈性客群評估可讓您快速地隨選建立新客群，以進行具有時效性的通訊。如需更多有關這個新功能的資訊，請參閱[客群入口網站文件](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation)。 |

{style="table-layout:auto"}

如需有關 [!DNL Segmentation Service] 的詳細資訊，請閱讀[客戶細分概觀](../../segmentation/home.md)。

## 沙箱 {#sandboxes}

Adobe Experience Platform 是為了在全球規模上使數位體驗應用程式更加豐富而打造。公司經常要並行執行多個數位體驗應用程式，且在顧及這些應用程式的開發、測試和部署等需求的同時，也必須確保營運合規性。為了滿足這種需求，Experience Platform 提供的沙箱可將單一 Platform 執行個體分割成個別的虛擬環境，以協助開發並改進數位體驗應用程式。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 共用沙箱工具套件 | 您現在可以使用沙箱工具，在不同組織的沙箱之間輕鬆匯出和匯入沙箱設定。現在有兩個可供使用的共用套件類別：<br><ul><li>**[私人套件](../../sandboxes/ui/sharing-packages-across-orgs.md#private-packages)：**&#x200B;使用私人套件，與已核准來源組織之共用請求的組織共用。</li><li>**[公開套件](../../sandboxes/ui/sharing-packages-across-orgs.md#public-packages)：**&#x200B;公開套件不需額外核准即可共用，而且能夠使用套件的承載輕鬆匯入。</li></ul><br>如需這些功能的詳細資訊，請閱讀有關[跨組織共用套件](../../sandboxes/ui/sharing-packages-across-orgs.md)的指南。 |
| 沙箱工具 API 中的[套件共用](https://experienceleague.adobe.com/zh-hant/docs/experience-platform/sandbox/sandbox-tooling-api/packages#org-linking) | 使用沙箱工具 API 向兩個新端點 `/handshake` 和 `/transfer` 發出請求，以便在組織間共用、擷取和建立套件共用請求。已為 `/packages` 端點新增了一個額外的請求，以擷取套件的承載。 |

{style="table-layout:auto"}

如需有關沙箱的詳細資訊，請閱讀[沙箱概觀](../../sandboxes/home.md)。

## 來源 {#sources}

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間並管理資料攝取輸送量。

使用 Experience Platform 中的來源，即可從 Adobe 應用程式或第三方資料來源攝取資料。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 支援在 [!DNL Marketo Engage] 中篩選標準活動實體 | 從 [!DNL Marketo Engage] 來源擷取資料時，您可以使用 [!DNL Flow Service] API 篩選標準活動實體。如需詳細資訊，請閱讀有關[篩選 [!DNL Marketo] 標準活動資料](../../sources/tutorials/api/filter.md#filter-activity-entities-for-marketo-engage)的指南。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[來源概觀](../../sources/home.md)。