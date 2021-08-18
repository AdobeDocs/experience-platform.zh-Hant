---
keywords: 平台；目的地；目的地工作區；工作區；ui；目的地ui；目錄；目的地目錄；
title: 目的地工作區
description: 「目的地」工作區包含四個區段：目錄、瀏覽、帳戶和系統檢視。 以下各節將說明這些規則。
seo-description: 在Adobe Experience Platform中，從左側導覽列選取「目的地」 ，以存取目的地工作區。
exl-id: 0f46f08d-0fe3-441d-933a-86bc146c0f19
source-git-commit: a97b235e2d8834f6be002923be9cdbca5f08495b
workflow-type: tm+mt
source-wordcount: '873'
ht-degree: 2%

---

# 目的地工作區 {#destinations-workspace}

在Adobe Experience Platform中，從左側導覽列選取&#x200B;**[!UICONTROL 目標]**&#x200B;以存取[!UICONTROL 目標]工作區。

[!UICONTROL Destinations]工作區由以下各節中描述的五個部分組成：[!UICONTROL Overview]、[!UICONTROL Catalog]、[!UICONTROL Browse]、[!UICONTROL Accounts]和[!UICONTROL System View]。

![目的地概述](../assets/ui/workspace/destinations-overview.png)

## [!UICONTROL 概覽] {#overview}

**[!UICONTROL 概述]**&#x200B;標籤顯示[!UICONTROL 目標]控制面板，提供與貴組織的目的地資料相關的關鍵量度。 若要進一步了解，請造訪[[!UICONTROL 目標]控制面板指南](../../dashboards/guides/destinations.md)。

>[!NOTE]
>
>如果您的組織剛開始Experience Platform，且尚未有作用中的目的地，則不會顯示[!UICONTROL Destinations]控制面板和[!UICONTROL Overview]標籤。 相反地，從左側導覽中選取[!UICONTROL Destinations]會顯示[[!UICONTROL Catalog]標籤](#catalog)。

![](../../dashboards/images/destinations/dashboard-overview.png)

## [!UICONTROL 目錄] {#catalog}

**[!UICONTROL Catalog]**&#x200B;標籤顯示[!DNL Platform]中所有可用的目標的清單，您可以將資料發送到這些目標。

[!DNL Platform]使用者介面在目標目錄頁面上提供數個搜尋和篩選選項：

* 使用頁面上的搜尋功能來尋找特定目的地。
* 使用[!UICONTROL 類別]控制項篩選目的地。
* 在[!UICONTROL 所有目標]和[!UICONTROL 我的目標]之間切換。 選擇&#x200B;**[!UICONTROL 所有目標]**&#x200B;時，將顯示所有可用的[!DNL Platform]目標。 選擇&#x200B;**[!UICONTROL 我的目標]**&#x200B;時，您只能查看已建立連接的目標。
* 選擇以查看&#x200B;**[!UICONTROL Connections]**&#x200B;和/或&#x200B;**[!UICONTROL Extensions]**。 若要了解這兩個類別之間的差異，請參閱[目標類型和類別](../destination-types.md)。

![目的地篩選和搜尋示範](../assets/ui/workspace/destinations-search-and-filter.gif)

目標卡包含&#x200B;**[!UICONTROL Configure]**&#x200B;或&#x200B;**[!UICONTROL Activate]**&#x200B;控制項，以及帶有更多選項的輔助控制項。 以下說明這些控制項：

| 控制 | 說明 |
|---------|----------|
| [!UICONTROL 設定] | 可讓您建立與目的地的連線。 |
| [!UICONTROL 啟動] | 建立與目的地的連線後，您就可以啟用區段。 |
| [!UICONTROL 查看帳戶] | 查看已為目標連接的帳戶。 |
| [!UICONTROL 查看資料流] | 檢視目的地的資料啟動流程。 |
| [!UICONTROL 檢視檔案] | 開啟該特定目的地的檔案頁面連結，以取得詳細資訊並協助您進行設定。 |

{style=&quot;table-layout:auto&quot;}

![控制目的地卡](../assets/ui/workspace/destination-card-options.png)

在目錄中選取目的地卡片，以開啟右側邊欄。 您可以在此處查看目的地的說明。 右側邊欄提供上表所述的相同控制項，包括目的地說明以及目的地類別和類型的指示。

![目標目錄選項](../assets/ui/workspace/destination-right-rail.png)

有關目標類別和每個目標資訊的詳細資訊，請參閱[目標目錄](../catalog/overview.md)和[目標類型和類別](../destination-types.md)。

## [!UICONTROL 帳戶] {#accounts}

**[!UICONTROL Accounts]**&#x200B;頁簽顯示您與各種目的地建立的連接的詳細資訊，並允許您更新現有的連接詳細資訊。 有關詳細說明，請參閱[更新帳戶](update-accounts.md)。

## [!UICONTROL 瀏覽] {#browse}

**[!UICONTROL Browse]**&#x200B;標籤顯示您已建立連接的目標。 已分別開啟&#x200B;**[!UICONTROL 啟用/停用]**&#x200B;的目標，將目標設定為使用中或非使用中。 您也可以選取&#x200B;**[!UICONTROL 區段]** > **[!UICONTROL 瀏覽]**&#x200B;並選取要檢查的區段，以檢視有資料流動的目的地。 有關在「瀏覽」頁簽中為每個目標提供的所有資訊，請參閱下表：

>[!TIP]
>
> * 在[!UICONTROL Name]欄上選取三個點，然後使用![Add segments按鈕](../assets/ui/workspace/add-data-symbol.png)**[!UICONTROL Activate ]**按鈕將區段傳送至該目的地。
> * 在[!UICONTROL Name]列上選擇三個點，然後使用![Delete destinations按鈕](../assets/ui/workspace/delete-destination-symbol.png)**[!UICONTROL Delete ]**按鈕[Remove](delete-destinations.md)與目標的現有連接。


![瀏覽頁簽](../assets/ui/workspace/browse-tab.png)

| 元素 | 說明 |
|---------|----------|
| 名稱 | 您為啟動流程提供的名稱，可用於此目的地。 同一欄包含兩個控制項：[!UICONTROL 啟動]和[!UICONTROL 刪除目標]。 |
| [!UICONTROL 上次流運行狀態] | 上次資料流運行的狀態。 有關資料流運行的詳細資訊，請參閱[查看目標詳細資訊](destination-details-page.md)。 |
| [!UICONTROL 上次流運行日期] | 上次資料流運行發生的時間和日期。 有關資料流運行的詳細資訊，請參閱[查看目標詳細資訊](destination-details-page.md)。 |
| [!UICONTROL 目標] | 您為啟動流程選取的目的地平台。 |
| [!UICONTROL 連線類型] | 代表與儲存貯體或目的地的連線類型。 <ul><li>對於電子郵件行銷目的地：可以是S3、FTP或[!DNL Azure Blob]。</li><li>針對即時廣告目的地：伺服器對伺服器。</li><li>針對串流目的地：可以是[!DNL Azure Event Hubs]或[!DNL Amazon Kinesis]。</li></ul> |
| [!UICONTROL 使用者名稱] | 您為目的地流程選擇的帳戶憑據。 |
| [!UICONTROL 啟動資料] | 指出要啟動至此目的地的區段數。 選取此控制項，即可進一步了解已啟用的區段。 如需已啟動區段的詳細資訊，請參閱目標詳細資訊頁面中的[啟動資料](/help/destinations/ui/destination-details-page.md#activation-data)。 |
| [!UICONTROL 已建立] | 建立至目的地的啟動流程的日期和UTC時間。 |
| [!UICONTROL 狀態] | `Active` 或 `Inactive`. 指示是否正在將資料激活到此目標。 |

按一下目的地列，在右側邊欄中顯示有關目的地的詳細資訊。

![按一下目標列](../assets/ui/workspace/click-destination-row.png)

選取目標名稱，以查看已啟動至此目標之區段的相關資訊。 按一下&#x200B;**[!UICONTROL 編輯啟用]**&#x200B;以修改或新增至傳送至此目的地的區段。

## [!UICONTROL 系統視圖] {#system-view}

**[!UICONTROL 系統視圖]**&#x200B;頁簽顯示您已在Adobe Experience Platform中設定的激活流的圖形表示。

![資料流1](../assets/ui/workspace/data-flows1.png)

選擇頁面上顯示的任何目標，然後按一下&#x200B;**[!UICONTROL 查看資料流]**&#x200B;以查看您為每個目標設定的所有連接的資訊。

![資料流2](../assets/ui/workspace/data-flows2.png)
