---
keywords: 量度概述；rtcdp度量概觀
title: 即時客戶資料平台首頁和資料板
seo-title: 即時客戶資料平台首頁和資料板
description: Adobe Experience Platform 的儀表板、首頁和首次使用者體驗
seo-description: Adobe Experience Platform 的儀表板、首頁和首次使用者體驗
translation-type: tm+mt
source-git-commit: 00010d38a5d05800aeac9af8505093fee3593b45
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 4%

---


# [!DNL Real-time Customer Data Platform] 度量概述

當您登入即時CDP時，會顯示即時客戶資料平台（即時CDP）首頁，其中包含量度儀表板。

首頁只是顯示量度卡片的位置之一。 即時CDP在您的整個體驗中提供度量卡。 這些量度會通知您系統中的資料、設定檔和區段對象。

![image](assets/home.png)

如果登錄到即時CDP時系統中沒有資料，則首頁上的儀表板不會顯示。 在這種情況下，首頁會提供首次使用者體驗的學習教材。 當資料收集時，也就是當<!--sources-->資料集、描述檔、區段和目的地建立後，資料就會自動更新以顯示該資料的相關資訊。<!-- in metric cards-->

## 首頁控制面板檢視

<!--The dashboard shows information in several areas. Each category of information displays for the time range shown beneath the data.-->

控制面板分為<!-- two areas.-->:

* **領** 導層位於儀表板頂部。排行榜會顯示系統中的資料集、設定檔、區段和目標數目。

   ![影像](assets/leaderboard.png)

<!-- * **Metric cards** display beneath the leaderboard. Metric cards show additional information, such as percentages or trends. Metric cards appear as data is collected.
    ![image](assets/home-metrics.jpg)
Some information is shown in different ways on both the leaderboard and metric cards. -->
* **最近** 的項目會列出系統中新增的5個最近的資料集、來源、區段和目標。

   ![影像](assets/recent.png)

其他度量（例如描述檔和細分）可在即時客戶資料平台的其他部分取得。

### 資料集

**[!UICONTROL Datasets]**&#x200B;計數器顯示系統中的資料集數和[!DNL Platform]中的資料量。 建立資料集時，會更新此計數器。

有關資料集的詳細資訊，請參見[資料集概述](../catalog/datasets/overview.md)。

### 設定檔

**[!UICONTROL Profiles]**&#x200B;計數顯示在[!DNL Real-time Customer Profile]中具有配置檔案的總人數。 它不包含描述檔片段。 這是您可定址的觀眾總數。

此計數使用預設[合併策略](profile/merge-policies.md)，如統一配置檔案中合併策略配置中所設定。

每24小時更新一次設定檔數。

有關配置檔案的詳細資訊，請參閱即時CDP中的[客戶的統一視圖。](profile/profile-overview.md)

### 區段

**[!UICONTROL 區]** 段顯示為組織建立的區段總數。建立新區段時，會更新此數字。

如需區段的詳細資訊，請參閱[區段服務概觀](segmentation/segmentation-overview.md)。

### 目的地

**[!UICONTROL 目]** 標顯示為組織建立的目標總數。當建立新目標時，此數字會更新。

有關目標的詳細資訊，請參閱[目標概述](destinations/overview.md)。

<!-- ### Successful profile records

In the leaderboard **[!UICONTROL Successful profile records]** shows the total number of records that have been successfully processed into the profile.

There is also a metric card that shows the percentage of successful records. Select **[!UICONTROL View datasets]** to see more details about the profile records. Hover over the colored area of the graph to see additional details:

![image](assets/home-profilerecords-details.PNG)

The number of successful profile records is updated hourly. 

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

### Total profile records

The **[!UICONTROL Total profile records]** metric card shows the total number of data records enabled to feed into the profiles, and the percentage that are successful, updated once per day. This does not include all data in the data lake, because some data might not be enabled to feed into the profiles.

 Hover over the colored area of the graph to see additional details about the successful profiles:

![image](assets/home-profile-details.PNG)

Select **[!UICONTROL View profiles]** to see more details about the profile records.

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

For more information about viewing a specific profile, see [Profile viewer](profile/profile-viewer.md).

### Failed profile records

In the leaderboard, **[!UICONTROL Failed profile records]** counts the number of records that failed to process into the profile.

The **[!UICONTROL Failed profile records]** metric card shows this count, and includes a graphical representation that helps you see how failures have trended during the time shown below the graphic. This chart is updated hourly. Select **[!UICONTROL View datasets]** to see more details about the profile records.

The number of failed profile records is updated hourly. -->

### 最近的資料集

**[!UICONTROL 最近的資料集]**&#x200B;卡顯示了在組織內建立的五個最近的資料集。 建立新資料集時，會更新此清單。

選擇一個資料集以查看該項的詳細資訊，或選擇&#x200B;**[!UICONTROL 查看所有]**&#x200B;以查看資料集清單。 您可從中選擇特定來源以取得詳細資訊。

有關資料集的詳細資訊，請參見[資料集概述](../catalog/datasets/overview.md)。

### 最近來源

**[!UICONTROL 最近來源]**&#x200B;量度卡顯示組織內建立的5個最近來源。 當建立新來源時，此清單會更新。

選擇一個源以查看該項的詳細資訊，或選擇&#x200B;**[!UICONTROL 查看所有]**&#x200B;查看源清單。 您可從中選擇特定來源以取得詳細資訊。

有關源的詳細資訊，請參閱[源概述](sources/sources-overview.md)。

### 最近區段

**[!UICONTROL 最近區段]**&#x200B;量度卡顯示組織內建立的五個最近區段。 建立新區段時，此清單會更新。

選取區段以檢視該項目的詳細資訊，或&#x200B;**[!UICONTROL 檢視全部]**&#x200B;以檢視更多區段的相關資訊。

如需區段的詳細資訊，請參閱[區段服務概觀](segmentation/segmentation-overview.md)。

### 最近的目的地

**[!UICONTROL 最近目標]**&#x200B;度量卡顯示組織內建立的五個最近目標。 當建立新目標時，會更新此清單。

選擇一個目標以查看該項目的詳細資訊，或選擇&#x200B;**[!UICONTROL 查看所有]**&#x200B;查看更多目標的資訊。

有關目標的詳細資訊，請參閱[目標概述](destinations/overview.md)。
