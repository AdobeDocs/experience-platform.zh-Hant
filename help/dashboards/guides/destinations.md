---
keywords: Experience Platform；設定檔；即時客戶設定檔；使用者介面；UI；自訂；設定檔控制面板；控制面板
title: 目的地控制面板
description: Adobe Experience Platform提供控制面板，讓您透過該控制面板檢視組織作用中目的地的重要資訊。
type: Documentation
exl-id: 6a34a796-24a1-450a-af39-60113928873e
source-git-commit: 2791c32abe582d51d05d4bf0488ba82dfadfd053
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---

#  Destinationsdk

Adobe Experience Platform使用者介面(UI)提供控制面板，可讓您檢視有關組織作用中目的地的重要資訊，如每日快照中所擷取。 本指南概述如何在UI中存取和使用目標控制面板，並提供控制面板中所顯示量度的詳細資訊。

如需目的地的概觀，以及Experience Platform內所有可用目的地的目錄，請造訪[目的地檔案](../../destinations/home.md)。

##  Destinationsdkboard資料  {#destinations-dashboard-data}

[!UICONTROL 目標]控制面板會顯示您的組織已在體驗設定檔中啟用的目標快照。 快照中的資料與建立快照時在特定時間點顯示的資料完全相同。 換句話說，快照不是資料的近似值或樣本，目標控制面板不會即時更新。

>[!NOTE]
>
>自拍攝快照以來對資料所做的任何更改或更新都不會反映在儀表板中，直到拍攝下一個快照。

## 探索目的地控制面板

若要導覽至Platform UI中的目的地控制面板，請在左側邊欄中選取「**[!UICONTROL 目的地]**」，然後選取「**[!UICONTROL 概述]**」標籤以顯示控制面板。

>[!NOTE]
>
>如果您的組織剛開始Experience Platform，且尚未有作用中的目的地，則不會顯示[!UICONTROL Destinations]控制面板和[!UICONTROL Overview]標籤。 相反地，從左側導覽中選取[!UICONTROL Destinations]會顯示[!UICONTROL Catalog]標籤。 若要進一步了解[!UICONTROL Catalog]標籤，請參閱[[!UICONTROL Destinations]工作區指南](../../destinations/ui/destinations-workspace.md)。

![](../images/destinations/dashboard-overview.png)

## 可用介面工具集

Experience Platform提供多個Widget，您可用來視覺化與目的地相關的不同量度。 選取下方介面工具集的名稱以深入了解：

* [[!UICONTROL 最常使用的目的地]](#most-used-destinations)
* [[!UICONTROL 最近建立的目的地]](#recently-created-destinations)
* [[!UICONTROL 最近啟動的區段]](#recently-activated-segments)

### [!UICONTROL 最常使用的目的地] {#most-used-destinations}

**[!UICONTROL 最常使用的目標]**&#x200B;介面工具集按映射的區段數顯示貴組織自上次快照起的排名最前的目標。 此排名可深入分析正在使用哪些目的地，同時可能顯示未充分利用的目標。

例如，如果您昨天配置了目標，但未將任何段映射到該目標，則您將會看到該目標當前未充分利用。

自上次每日快照起，區段計數欄中顯示的對應區段數是準確的。 將新區段對應至目標要等到下一個快照建立後，才會更新計數。

從介面工具集上顯示的清單中選擇目標名稱，將帶您前往目標詳細資訊，如從&#x200B;**[!UICONTROL Browse]**&#x200B;標籤連結。 您也可以選擇&#x200B;**[!UICONTROL 查看全部]**&#x200B;以導覽至&#x200B;**[!UICONTROL 瀏覽]**&#x200B;標籤，然後選擇目標名稱以查看其詳細資訊。

![](../images/destinations/most-used-destinations.png)

### [!UICONTROL 最近建立的目的地] {#recently-created-destinations}

**[!UICONTROL 最近建立的目標]**&#x200B;介面工具集可讓您查看組織最近設定的目標清單。

顯示的建立日期與上次每日快照準確。 換言之，如果建立新目標，則要等到建立下一個快照後，它才會出現在清單中。

從介面工具集上顯示的清單中選擇目標名稱，將帶您前往目標詳細資訊，如從&#x200B;**[!UICONTROL Browse]**&#x200B;標籤連結。 您也可以選擇&#x200B;**[!UICONTROL 查看全部]**&#x200B;以導覽至&#x200B;**[!UICONTROL 瀏覽]**&#x200B;標籤，然後選擇目標名稱以查看其詳細資訊。

若要進一步了解如何設定特定類型的目的地，請造訪[目的地檔案](../../destinations/home.md)。

![](../images/destinations/recently-created-destinations.png)

### [!UICONTROL 最近啟動的區段] {#recently-activated-segments}

**[!UICONTROL 最近啟用的區段]**&#x200B;介面工具集提供最近映射至目的地的區段清單。 此清單提供系統中正在使用哪些區段和目標的快照，並有助於疑難排解任何錯誤對應。

顯示的更新日期會顯示上次啟動區段至目的地的時間，且對最後的每日快照準確。 換言之，如果您對目的地啟用區段，則更新的日期要等到下次快照建立後才會變更。

從介面工具集上顯示的清單中選取區段名稱，會帶您前往區段詳細資訊。 您也可以選取&#x200B;**[!UICONTROL 檢視全部]**&#x200B;以導覽至區段瀏覽標籤，然後選取區段名稱以檢視其詳細資訊。

如需在Experience Platform中使用區段的詳細資訊，請先閱讀[分段服務概述](../../segmentation/home.md)開始。

![](../images/destinations/recently-activated-segments.png)

## 後續步驟

依照本檔案操作，您現在應該能夠找到目的地控制面板並了解可用介面工具集中顯示的量度。 若要進一步了解如何在Experience Platform中使用目標，請參閱[目標檔案](../../destinations/home.md)。
