---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；用戶介面；UI；自定義；配置檔案面板；儀表板
title: 目標儀表板
description: Adobe Experience Platform提供了一個儀表板，您可以通過該儀表板查看有關組織活動目標的重要資訊。
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: 86041e3165d4ea9cb55717f24b002afa084ff420
workflow-type: tm+mt
source-wordcount: '1709'
ht-degree: 0%

---

# [!UICONTROL 目標] 儀表板

Adobe Experience Platform用戶介面(UI)提供了一個儀表板，您可以通過該儀表板查看有關組織活動目標的重要資訊，這些資訊在每日快照中捕獲。 本指南概述了如何訪問和使用UI中的目標儀表板，並提供了有關儀表板中顯示的度量的詳細資訊。

有關目的地的概述，以及Experience Platform內所有可用目的地的目錄，請訪問 [目標文檔](../../destinations/home.md)。

## [!UICONTROL 目標] 儀表板資料 {#destinations-dashboard-data}

的 [!UICONTROL 目標] 儀表板顯示您的組織在Experience Platform中啟用的目標的快照。 快照中的資料與拍攝快照時在特定時間點顯示的資料完全相同。 換句話說，快照不是資料的近似值或示例，目標儀表板不會即時更新。

>[!NOTE]
>
>自拍攝快照以來對資料所做的任何更改或更新不會反映在儀表板中，直到拍攝下一個快照。

## 瀏覽目標儀表板

要導航到平台UI中的目標儀表板，請選擇 **[!UICONTROL 目標]** 在左滑軌中，選擇 **[!UICONTROL 概述]** 頁籤。

>[!NOTE]
>
>如果您的組織是新Experience Platform的，且尚未有活動目標， [!UICONTROL 目標] 儀表板和 [!UICONTROL 概述] 頁籤不可見。 而是選擇 [!UICONTROL 目標] 從左側導航顯示 [!UICONTROL 目錄] 頁籤。 瞭解有關 [!UICONTROL 目錄] ，請參閱 [[!UICONTROL 目標] 工作區指南](../../destinations/ui/destinations-workspace.md)。

![](../images/destinations/dashboard-overview.png)

### 修改目標儀表板

通過選擇 **[!UICONTROL 修改儀表板]**。 這使您能夠從儀表板中移動、添加和刪除小部件，以及訪問 **[!UICONTROL 小部件庫]** 瀏覽可用小部件並為您的組織建立自定義小部件。

請參閱 [修改儀表板](../customize/modify.md) 和 [構件庫概述](../customize/widget-library.md) 文檔以瞭解詳細資訊。

## 標準小部件

Adobe提供了多個標準小部件，您可以使用這些部件來可視化與目標相關的不同度量，並評估可用於資料分析的段的完整性。 您也可以使用 [!UICONTROL 小部件庫]。 要瞭解有關建立自定義小部件的詳細資訊，請首先閱讀 [構件庫概述](../customize/widget-library.md)。

要瞭解有關每個可用標準小部件的詳細資訊，請從以下清單中選擇小部件的名稱：

* [[!UICONTROL 最常用的目標]](#most-used-destinations)
* [[!UICONTROL 最近建立的目標]](#recently-created-destinations)
* [[!UICONTROL 最近激活的段]](#recently-activated-segments)
* [[!UICONTROL 按目標最近激活的段]](#recently-activated-segments-by-destination)
* [[!UICONTROL 受眾規模趨勢]](#audience-size-trends)
* [[!UICONTROL 按標識未映射的段]](#unmapped-segments-by-identity)
* [[!UICONTROL 按標識映射的段]](#mapped-segments-by-identity)
* [[!UICONTROL 普通觀眾]](#common-audiences)
* [[!UICONTROL 目標計數]](#destinations-count)

### [!UICONTROL 最常用的目標] {#most-used-destinations}

的 **[!UICONTROL 最常用的目標]** 小部件按映射的段數顯示組織的頂級目標，截止到上次快照。 此排名可以深入瞭解哪些目標正被利用，同時可能還顯示那些可能未充分利用的目標。

例如，如果您昨天配置了目標，但尚未將任何段映射到該目標，則您將能夠看到該目標當前未充分利用。

在段計數列中顯示的映射段數截至最後一個每日快照時是準確的。 將新段映射到目標將不會更新計數，直到拍攝下一個快照。

從小部件上顯示的清單中選擇目標名稱將帶您轉到連結自 **[!UICONTROL 瀏覽]** 頁籤。 也可以選擇 **[!UICONTROL 全部查看]** 導航至 **[!UICONTROL 瀏覽]** 頁籤，然後選擇目標名稱以查看其詳細資訊。

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL 最近建立的目標] {#recently-created-destinations}

的 **[!UICONTROL 最近建立的目標]** 構件使您可以查看組織最近配置的目標的清單。

顯示的建立日期與最後一個每日快照準確無誤。 換句話說，如果建立新目標，則在拍攝下一個快照之前，它不會出現在清單中。

從小部件上顯示的清單中選擇目標名稱將帶您轉到連結自 **[!UICONTROL 瀏覽]** 頁籤。 也可以選擇 **[!UICONTROL 全部查看]** 導航至 **[!UICONTROL 瀏覽]** 頁籤，然後選擇目標名稱以查看其詳細資訊。

要瞭解有關如何配置特定目標類型的詳細資訊，請訪問 [目標文檔](../../destinations/home.md)。

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL 最近激活的段] {#recently-activated-segments}

的 **[!UICONTROL 最近激活的段]** 構件提供最近映射到目標的段的清單。 此清單提供了系統中正在使用哪些段和目標的快照，並有助於排除任何錯誤映射。

顯示的更新日期顯示段上次激活到目標的時間，並且與上次的每日快照準確。 換句話說，如果將段激活到目標，則更新的日期在拍攝下一個快照之後才會更改。

從小部件上顯示的清單中選擇段的名稱將帶您進入段詳細資訊。 也可以選擇 **[!UICONTROL 全部查看]** 導航到段瀏覽頁籤，然後選擇段名稱以查看其詳細資訊。

有關使用Experience Platform中段的詳細資訊，請首先閱讀 [分段服務概述](../../segmentation/home.md)。

![](../images/destinations/recently-activated-segments.png)

### [!UICONTROL 按目標最近激活的段] {#recently-activated-segments-by-destination}

的 **[!UICONTROL 按目標最近激活的段]** 小部件根據在概述下拉清單中選擇的目標按降序顯示前五個最近激活的段。 與 [!UICONTROL 最近激活的段] 小部件，但顯示的資料 **僅** 應用於所選目標。

此小部件包含兩個度量：段名稱和段上次激活到目標的日期。 顯示的資料自上次的每日快照時起是正確的。

通過從顯示的清單中選擇段名稱，可以查看段的詳細資訊。

![最近按目標小部件激活的段。](../images/destinations/recently-activated-segments-by-destination.png)

### [!UICONTROL 受眾規模趨勢] {#audience-size-trend}

的 **[!UICONTROL 受眾規模趨勢]** 小部件描述已映射到該目標帳戶的段的配置檔案計數在一段時間內的關係。 構件使用線形圖來說明段中包含的每天發送到目標帳戶的配置檔案數。

過去30天、90天或12個月的受眾趨勢時段可以使用第一個下拉菜單進行調整。

第二個下拉菜單列出了每個可發送到儀表板頂部所選目標帳戶的可用段。

![受眾大小趨勢小部件。](../images/destinations/audience-size-trend.png)

### [!UICONTROL 按標識未映射的段] {#unmapped-segments-by-identity}

的 **[!UICONTROL 按標識未映射的段]** 小部件列出前五 **未映射** 按給定目標和標識的降序標識計數排序的段。 它突出顯示基於所選ID映射到所選目標帳戶最有益的段。

目標ID下拉清單將篩選可用段。 下拉清單中列出的篩選器ID取決於在概述頁頂部選擇的目標帳戶。

標識列計算段內可映射到構件ID下拉清單中選擇的ID的源ID數。

![按標識構件顯示的未映射段。](../images/destinations/unmapped-segments-by-identity.png)

### [!UICONTROL 按標識映射的段] {#mapped-segments-by-identity}

此小部件提供了 **映射** 段。 根據段中包含的源ID數，從高到低對清單進行排序。 要計數的目標ID是從小部件標題下的下拉菜單中選擇的。 從構件中的下拉清單中可用的目標ID將根據在概述儀表板頂部選擇的目標帳戶篩選器進行更改。

![按標識小部件映射的段。](../images/destinations/mapped-segments-by-identity.png)

的 **[!UICONTROL 按標識映射的段]** 小部件一覽表就會突出顯示，成功鎖定所選目標內市場活動的配置檔案機會的可能性。 有效的目標市場活動不取決於發送到目標的配置檔案數量，而取決於可能與目標ID匹配以提供有用且可操作資料的源ID數量。

### 普通觀眾

的 **[!UICONTROL 普通觀眾]** 小部件提供了在頁面頂部選擇的目標帳戶中激活的前五個段以及在小部件下拉清單中選擇的目標的清單。 段清單按激活時間排序。 最近激活的段顯示在頂部。

的 [!UICONTROL 受眾大小] 列提供每個列出段的總配置檔案計數。

![常見受眾小部件。](../images/destinations/common-audiences.png)

### 映射的受眾健康

該小部件提供一個清單，列出多達20個映射的段，其截至最後一個每日快照，其配置檔案總數與映射到該目標的30天平均受眾大小的至少一個標準偏差因子。

簡而言之，它提供了計算過去30天中觀眾人數的平均分佈的指標。 它比較了今天的受眾規模是否超出了過去30天資料中所見的歷史標準差。

系統中的所有觀眾大小按高到低的觀眾大小排序，如 [!UICONTROL 最新大小] 的雙曲餘切值。

如果您的段映射配置檔案計數與過去30天內的平均映射配置檔案大小不在一個標準偏差範圍之內，則表明系統中存在異常，應對其進行調查。

如果 [!UICONTROL 映射的受眾健康] 小部件偏差較大，您應參考受眾大小趨勢圖並查找異常段。 這一趨勢可以進一步瞭解您所在細分市場的健康狀況。

![映射的受眾健康小部件。](../images/destinations/mapped-audience-health.png)

### [!UICONTROL 目標計數] (#destinations-count)

的 [!UICONTROL 目標計數] 構件提供了可在系統中激活和傳遞受眾的可用終結點總數。 此數字包括活動和非活動目標。

在總計數以下，選擇 **[!UICONTROL 目標]** 導航至目標瀏覽頁籤。 此頁列出了您已建立與迄今為止的連接的所有目標。

![目標計數構件。](../images/destinations/destinations-count.png)

## 後續步驟

現在，通過遵循本文檔，您應該能夠找到目標儀表板並瞭解可用小部件中顯示的度量。 要瞭解有關使用Experience Platform中的目標的詳細資訊，請參閱 [目標文檔](../../destinations/home.md)。
