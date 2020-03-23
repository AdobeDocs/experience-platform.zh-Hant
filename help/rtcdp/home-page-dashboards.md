---
title: 即時客戶資料平台首頁和資料板
seo-title: 即時客戶資料平台首頁和資料板
description: Adobe Experience Platform的儀表板、首頁和首次使用者體驗
seo-description: Adobe Experience Platform的儀表板、首頁和首次使用者體驗
translation-type: tm+mt
source-git-commit: 6c8d0757d7e7568b1976823d9c52221374e67cbb

---


# 即時客戶資料平台量度概觀

當您登入即時CDP時，會顯示Adobe即時客戶資料平台（即時CDP）首頁，其中包含量度控制面板。

首頁只是顯示量度卡片的位置之一。 即時CDP在您的整個體驗中提供度量卡。 這些量度會通知您系統中的資料、設定檔和區段對象。

![影像](assets/home2.jpg)

如果登錄到即時CDP時系統中沒有資料，則首頁上的儀表板不會顯示。 在這種情況下，首頁會提供首次使用者體驗的學習教材。 當資料收集時(換言之，當資料集、描述檔、區段 <!--sources-->和目的地建立並將資料流入系統時)，控制面板會自動更新以顯示該資料的相關資訊<!-- in metric cards-->。

## 首頁控制面板檢視

<!--The dashboard shows information in several areas. Each category of information displays for the time range shown beneath the data.-->

控制面板分為<!-- two areas.-->:

* **排行榜** (leaderboard)位於儀表板的頂端。 排行榜會顯示系統中的資料集、設定檔、區段和目標數目。

   ![影像](assets/home-leaderboard2.jpg)

<!-- * **Metric cards** display beneath the leaderboard. Metric cards show additional information, such as percentages or trends. Metric cards appear as data is collected.
    ![image](assets/home-metrics.jpg)
Some information is shown in different ways on both the leaderboard and metric cards. -->
* **最近的項目** (Recent items)列出系統中新增的5個最近的資料集、來源、區段和目標。

   ![影像](assets/home-recent.jpg)

其他度量（例如描述檔和細分）可在即時客戶資料平台的其他部分取得。

### 資料集

計數 **[!UICONTROL Datasets]** 器顯示系統中的資料集數和平台中的資料量。 建立資料集時，會更新此計數器。

如需資料集的詳細資訊，請參 [閱將資料內嵌至Adobe Experience Platform](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/data_ingestion_tutorial/data_ingestion_tutorial.md)。

### 設定檔

計 **[!UICONTROL Profiles]** 數顯示「即時客戶設定檔」中具有設定檔的總人數。 它不包含描述檔片段。 這是您可定址的觀眾總數。

此計數使用預設 [合併策略](profile/merge-policies.md) ，如統一配置檔案中合併策略配置中所設定。

每24小時更新一次設定檔數。

有關配置檔案的詳細資訊，請 [參閱Real-time CDP中對客戶的統一視圖](profile/profile-overview.md)。

### 區段

**[!UICONTROL Segments]** 顯示為組織建立的區段總數。 建立新區段時，會更新此數字。

如需區段的詳細資訊，請參閱區 [段服務概觀](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/segmentation/segmentation-overview.md)。

### 目的地

**[!UICONTROL Destinations]** 顯示為組織建立的目標總數。 當建立新目標時，此數字會更新。

如需目標的詳細資訊，請參閱目 [標概觀](destinations/destinations-overview.md)。

<!-- ### Successful profile records

In the leaderboard **[!UICONTROL Successful profile records]** shows the total number of records that have been successfully processed into the profile.

There is also a metric card that shows the percentage of successful records. Click **[!UICONTROL View datasets]** to see more details about the profile records. Hover over the colored area of the graph to see additional details:

![image](assets/home-profilerecords-details.PNG)

The number of successful profile records is updated hourly. 

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

### Total profile records

The **[!UICONTROL Total profile records]** metric card shows the total number of data records enabled to feed into the profiles, and the percentage that are successful, updated once per day. This does not include all data in the data lake, because some data might not be enabled to feed into the profiles.

 Hover over the colored area of the graph to see additional details about the successful profiles:

![image](assets/home-profile-details.PNG)

Click **[!UICONTROL View profiles]** to see more details about the profile records.

For more information about profiles, see [A unified view of your customer in Real-time CDP](profile/profile-overview.md).

For more information about viewing a specific profile, see [Profile viewer](profile/profile-viewer.md).

### Failed profile records

In the leaderboard, **[!UICONTROL Failed profile records]** counts the number of records that failed to process into the profile.

The **[!UICONTROL Failed profile records]** metric card shows this count, and includes a graphical representation that helps you see how failures have trended during the time shown below the graphic. This chart is updated hourly. Click **[!UICONTROL View datasets]** to see more details about the profile records.

The number of failed profile records is updated hourly. -->

### 最近的資料集

該卡 **[!UICONTROL Recent datasets]** 顯示在組織內建立的五個最近資料集。 建立新資料集時，會更新此清單。

按一下資料集可檢視該項目的詳細資訊，或 **[!UICONTROL View all]** 查看資料集清單。 在此處，您可以按一下特定源以獲取詳細資訊。

如需資料集的詳細資訊，請參 [閱將資料內嵌至Adobe Experience Platform](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html#!api-specification/markdown/narrative/tutorials/data_ingestion_tutorial/data_ingestion_tutorial.md)。

### 最近來源

量 **[!UICONTROL Recent sources]** 度卡顯示組織內建立的5個最近來源。 當建立新來源時，此清單會更新。

按一下來源可檢視該項目的詳細資訊，或 **[!UICONTROL View all]** 查看來源清單。 在此處，您可以按一下特定源以獲取詳細資訊。

如需來源的詳細資訊，請參閱 [來源概觀](sources/sources-overview.md)。

### 最近區段

量 **[!UICONTROL Recent segments]** 度卡顯示在組織內建立的5個最近區段。 建立新區段時，此清單會更新。

按一下區段可檢視該項目的詳細資訊，或 **[!UICONTROL View all]** 查看更多區段的資訊。

如需區段的詳細資訊，請參閱區 [段服務概觀](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/segmentation/segmentation-overview.md)。

### 最近的目的地

量 **[!UICONTROL Recent destinations]** 度卡顯示組織內建立的五個最近目的地。 當建立新目標時，會更新此清單。

按一下目標可檢視該項目的詳細資訊，或 **[!UICONTROL View all]** 查看更多目標的相關資訊。

如需目標的詳細資訊，請參閱目 [標概觀](destinations/destinations-overview.md)。
