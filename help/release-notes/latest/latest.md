---
title: Adobe Experience Platform發行說明2024年10月
description: Adobe Experience Platform 2024 年 10 月版本注意事項。
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: f30a124a40928abf69366d311131e353c2779191
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 35%

---

# Adobe Experience Platform 發行說明

**發行日期： 2024年10月29日**

Adobe Experience Platform 現有功能及文件的更新：

- [儀表板](#dashboards)
- [資料彙集](#data-collection-)
- [目標](#destinations)
- [Segmentation Service](#segmentation-service)
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
| 標籤和擴充功能 | Adobe Analytics JSON檢視 | 您現在可以使用Adobe Analytics標籤擴充功能，以JSON格式檢查eVar、prop和事件設定，這些現在可以包含在Web SDK擴充功能中，並匯出以供編輯。 您也可以上傳或複製此資料，並將其儲存在裝置上。 如需詳細資訊，請參閱[Adobe Analytics擴充功能檔案](../../tags/extensions/client/analytics/overview.md)。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[資料彙集概觀](../../collection/home.md)。

## 目標 {#destinations}

[!DNL Destinations] 是預先建立的和目標平台的整合，可讓來自 Adobe Experience Platform 的資料順暢啟動。您可使用目標啟用已知和未知的資料，以進行跨通路行銷活動、電子郵件行銷活動、設定目標的廣告活動和其他諸多使用案例。

**新功能或更新的功能** {#destinations-new-updated-functionality}

| 功能 | 說明 |
| ----------- | ----------- |
| [一般可用的陣列匯出支援](../../destinations/ui/export-arrays-calculated-fields.md) | 所有客戶現在都可以使用&#x200B;**[!UICONTROL 新增計算欄位]**&#x200B;選項，將對象&#x200B;*啟動至檔案型目的地*&#x200B;以匯出整個陣列或陣列元素。 請注意，您仍需使用`array_to_string`函式，將陣列平面化為目標檔案中的字串。<br> ![新增包含函式和欄位的計算欄位選擇。](../2024/assets/october/array-export.gif "使用array_to_string函式與組織陣列中的選項新增計算欄位。"){width="250" align="center" zoomable="yes"} |
| [串流目的地的報表準確性增強功能](/help/destinations/ui/export-datasets.md) | Adobe自2024年10月起陸續推出更新，以提高串流目的地的報表準確性。 此增強功能可確保Experience Platform與目的地平台報告之間更佳的對應。 <br>在此更新之前，**[!UICONTROL 身分失敗]**&#x200B;包含所有啟用重試。 在此更新後，只有上次啟用重試會包含在總計數中。 <br>此增強功能目前適用於[Google Customer Match目的地](../../destinations/catalog/advertising/google-customer-match.md)，但將逐步推廣至其他Experience Platform串流目的地。 進行此增強功能後，[Google Customer Match目的地](../../destinations/catalog/advertising/google-customer-match.md)的使用者可能會看到其&#x200B;**[!UICONTROL 身分識別失敗]**&#x200B;計數中預期的下降。 |
| 彈性對象評估對[批次對象啟用](../../destinations/ui/activate-batch-profile-destinations.md#export-full-files)的影響 | 如果您對已設定在區段評估後啟用的對象執行[彈性對象評估](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation)，則無論任何先前的每日啟用工作，彈性對象評估工作一完成，對象就會啟用。 <br>這可能會導致根據您的動作，一天匯出多次對象。 |

{style="table-layout:auto"}

如需詳細資訊，請閱讀[目標概觀](../../destinations/home.md)。

## Segmentation Service {#segmentation-service}

[!DNL Segmentation Service] 會說明區分客戶群中可行銷的一群人的標準，從而定義輪廓的特定子集。區段的基礎可能是記錄資料 (例如人口統計資訊) 或表示客戶與您的品牌互動的時間序列事件。

**新功能或更新功能**

| 功能 | 說明 |
| ------- | ----------- |
| [!BADGE 可用性限制]{type=Informative}彈性對象評估 | 彈性的受眾評估可讓您根據對時間敏感的通訊的需求，快速建立新的受眾。 您可以在[Audience Portal檔案](../../segmentation/ui/audience-portal.md#flexible-audience-evaluation)中找到有關此新功能的詳細資訊。 |

{style="table-layout:auto"}

如需有關 [!DNL Segmentation Service] 的詳細資訊，請參閱「[客戶細分概觀](../../segmentation/home.md)」。

## 沙箱 {#sandboxes}

Adobe Experience Platform 是為了在全球規模上使數位體驗應用程式更加豐富而打造。公司經常要並行執行多個數位體驗應用程式，且在顧及這些應用程式的開發、測試和部署等需求的同時，也必須確保營運合規性。為了滿足這種需求，Experience Platform 提供的沙箱可將單一 Platform 執行個體分割成個別的虛擬環境，以協助開發並改進數位體驗應用程式。

**新功能或更新功能**

| 功能 | 說明 |
| --- | --- |
| 沙箱工具封裝共用 | 您現在可以使用沙箱工具，輕鬆匯出和匯入不同組織沙箱之間的沙箱設定。 目前有兩個可用的共用套件類別： <br><ul><li>**[私人套件](../../sandboxes/ui/sharing-packages-across-orgs.md#private-packages)：**&#x200B;使用私人套件與已核准來源組織之共用要求的組織共用。</li><li>**[公用套件](../../sandboxes/ui/sharing-packages-across-orgs.md#public-packages)：**&#x200B;公用套件不需額外核准即可共用，並可使用套件的裝載輕鬆匯入。</li></ul><br>如需這些功能的詳細資訊，請閱讀[跨組織共用封裝](../../sandboxes/ui/sharing-packages-across-orgs.md)的指南。 |
| 沙箱工具API中的[封裝共用](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/sandbox-tooling-api/packages#org-linking) | 使用沙箱工具API向兩個新端點`/handshake`和`/transfer`發出請求，以便跨組織共用、擷取和建立套件共用請求。 已新增其他要求至`/packages`端點，以擷取封裝的裝載。 |

{style="table-layout:auto"}

如需有關沙箱的詳細資訊，請閱讀[沙箱概觀](../../sandboxes/home.md)。

## 來源 {#sources}

Experience Platform 可提供 RESTful API 和互動式 UI，可讓您輕鬆為各種資料提供者設定來源連線。這些來源連線可讓您進行驗證並連線到外部儲存系統和 CRM 服務、設定攝取執行的時間並管理資料攝取輸送量。

使用 Experience Platform 中的來源，即可從 Adobe 應用程式或第三方資料來源攝取資料。

**更新的功能**

| 功能 | 說明 |
| --- | --- |
| 支援篩選[!DNL Marketo Engage]中的標準活動實體 | 從[!DNL Marketo Engage]來源擷取資料時，您可以使用[!DNL Flow Service] API來篩選標準活動實體。 如需詳細資訊，請閱讀[篩選 [!DNL Marketo] 標準活動資料](../../sources/tutorials/api/filter.md#filter-activity-entities-for-marketo-engage)的指南。 |

{style="table-layout:auto"}

如需詳細資訊，請參閱[來源概觀](../../sources/home.md)。