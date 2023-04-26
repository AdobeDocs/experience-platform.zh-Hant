---
keywords: 量度概觀；rtcdp量度概觀
title: Real-time Customer Data Platform首頁和控制面板
description: Adobe Experience Platform 的儀表板、首頁和首次使用者體驗
exl-id: ced5b69c-5bb5-4e06-9cb4-938e36e6e5cc
source-git-commit: 8ea657e379248616d3140bc0a7b0c25a918bc857
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 1%

---

# [!DNL Real-Time Customer Data Platform] 首頁

Adobe Real-time Customer Data Platform(Real-Time CDP)首頁是登入Real-Time CDP後顯示的第一頁。

Real-Time CDP首頁包含快速入門Widget，可讓您快速存取數種不同功能，以及量度區段，可顯示貴組織內資料的最新資訊。

本檔案概述Real-Time CDP首頁和量度控制面板。

![平台UI首頁。](assets/platform-home/home.png)

## 快速入門介面工具集

此 [!UICONTROL 即時客戶個人檔案快速入門] 介面工具集分為四個區段：

* **將資料內嵌至Platform**:此介面工具集會將您導向源目錄。 使用來源目錄來選取來源並擷取資料以Experience Platform。 如需詳細資訊，請閱讀 [來源概觀](../sources/home.md)
* **模型資料結構**:此介面工具集會將您導向結構概觀。 使用結構概觀來瀏覽現有的結構，或建立描述資料結構的基礎要素。 如需詳細資訊，請閱讀 [綱要概觀](../xdm/home.md).
* **區段對象**:此介面工具集會將您導向 [!DNL Segment Builder] 在UI中。 使用 [!DNL Segment Builder] 與設定檔資料元素互動並定義區段規則。 如需詳細資訊，請閱讀 [區段服務概觀](../segmentation/home.md).
* **將資料傳送至目的地**:此介面工具集會將您導向目標目錄。 使用目標目錄來選取目的地，然後您可以連線至該目的地，並將區段傳送至該目的地。 如需詳細資訊，請閱讀 [目的地概述](../destinations/home.md)

![顯示快速入門介面工具集的Platform UI首頁](assets/platform-home/getting-started-widget.png)

## 量度控制面板

量度控制面板會顯示您Experience Platform資料的最新資訊。 控制面板分為兩個區段：

### 排行榜

展示板會顯示貴組織中目前的結構、資料集、設定檔和區段總數，以及其最近的更新日期。

![Platform UI首頁的排行榜區段。](assets/platform-home/leaderboard.png)

* **結構總計**:此 **結構總計** 計數器顯示系統中的結構數目。 建立架構時會更新此計數器。 如需詳細資訊，請閱讀 [綱要概觀](../xdm/home.md).
* **資料集總計**:此 **資料集總計** 計數器會顯示系統中的資料集數，以及 [!DNL Platform]. 建立資料集時，會更新此計數器。 如需資料集的詳細資訊，請參閱 [資料集概述](../catalog/datasets/overview.md).
* **設定檔總計**:此 **設定檔** count會顯示在 [!DNL Real-Time Customer Profile]. 其中不包含設定檔片段。 這是可定址的受眾總數。 此計數使用預設值 [合併策略](profile/merge-policies.md) 在統一配置檔案的合併策略配置中設定。 每24小時更新一次設定檔數目。 如需設定檔的詳細資訊，請參閱 [即時客戶個人檔案概觀](../profile/home.md).
* **總區段**: **區段** 顯示為組織建立的區段總數。 建立新區段時，會更新此數字。 如需區段的詳細資訊，請參閱 [區段服務概觀](../segmentation/home.md).

### 最近的項目

最近的項目列出貴組織中最近的變更。 在以下範例中，最近的變更涉及資料集、來源、區段和目的地。

![Platform UI首頁的最近項目區段。](assets/platform-home/recent-items.png)

* **最近的資料集**:此 **[!UICONTROL 最近的資料集]** 卡片顯示組織內最近建立的五個資料集。 建立新資料集時，會更新此清單。 選取資料集以檢視該項目的詳細資訊，或選取 **[!UICONTROL 查看全部]** 以取得資料集清單。 從那裡，您可以選擇特定的來源以獲取詳細資訊。 如需資料集的詳細資訊，請參閱 [資料集概述](../catalog/datasets/overview.md).
* **最近的來源**:此 **[!UICONTROL 最近的來源]** 「量度卡」會顯示組織內建立的5個最近來源。 建立新源時，將更新此清單。 選擇一個源以查看該項的詳細資訊，或選擇 **[!UICONTROL 查看全部]** 來源清單。 從那裡，您可以選擇特定的來源以獲取詳細資訊。 如需來源的詳細資訊，請參閱 [來源概觀](../sources/home.md).
* **最近區段**:此 **[!UICONTROL 最近區段]** 量度卡顯示組織內建立的5個最近區段。 建立新區段時，會更新此清單。 選取要檢視該項目的詳細資料的區段，或選取 **[!UICONTROL 查看全部]** ，以取得區段清單。 如需區段的詳細資訊，請參閱 [區段服務概觀](../segmentation/home.md).
* **近期目的地**:此 **[!UICONTROL 近期目的地]** 量度卡顯示組織內建立的5個最近目的地。 建立新目的地時，會更新此清單。 選擇要查看該項的詳細資訊的目標，或選擇 **[!UICONTROL 查看全部]** 以取得目的地清單。 如需詳細資訊，請閱讀 [目的地概述](../destinations/home.md).

## 資源

最後，資源Widget會提供您可參考的其他檔案資源。 這些類別包括：

![Platform UI首頁的「資源」區段。](assets/platform-home/resources.png)

* [了解結構](../xdm/schema/composition.md)
* [連接源](../sources/home.md)
* [如何填入您的即時客戶個人檔案](../profile/home.md)
* [連接目的地](../destinations/home.md)
* [管理存取](../access-control/abac/overview.md)

<!-- ### Successful profile records

In the leaderboard **[!UICONTROL Successful profile records]** shows the total number of records that have been successfully processed into the profile.

There is also a metric card that shows the percentage of successful records. Select **[!UICONTROL View datasets]** to see more details about the profile records. Hover over the colored area of the graph to see additional details:

![image](assets/home-profilerecords-details.PNG)

The number of successful profile records is updated hourly. 

For more information about profiles, see [A unified view of your customer in Real-Time CDP](profile/profile-overview.md).

### Total profile records

The **[!UICONTROL Total profile records]** metric card shows the total number of data records enabled to feed into the profiles, and the percentage that are successful, updated once per day. This does not include all data in the data lake, because some data might not be enabled to feed into the profiles.

 Hover over the colored area of the graph to see additional details about the successful profiles:

![image](assets/home-profile-details.PNG)

Select **[!UICONTROL View profiles]** to see more details about the profile records.

For more information about profiles, see [A unified view of your customer in Real-Time CDP](profile/profile-overview.md).

For more information about viewing a specific profile, see [Profile viewer](profile/profile-viewer.md).

### Failed profile records

In the leaderboard, **[!UICONTROL Failed profile records]** counts the number of records that failed to process into the profile.

The **[!UICONTROL Failed profile records]** metric card shows this count, and includes a graphical representation that helps you see how failures have trended during the time shown below the graphic. This chart is updated hourly. Select **[!UICONTROL View datasets]** to see more details about the profile records.

The number of failed profile records is updated hourly. -->
