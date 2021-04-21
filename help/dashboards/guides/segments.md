---
keywords: Experience Platform；配置檔案；段；段；分段；用戶介面；UI；定制；段儀表板；儀表板
title: 區段控制面板
description: 'Adobe Experience Platform提供控制面板，您可透過此控制面板檢視貴組織所建立之區段的重要資訊。 '
topic-legacy: guide
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 1%

---

# （測試版）區段控制面板{#segment-dashboard}

>[!IMPORTANT]
>
>本檔案中概述的控制面板功能目前為測試版，並非所有使用者都能使用。 文件和功能可能會有所變更。

Adobe Experience Platform使用者介面(UI)提供控制面板，您可透過此控制面板檢視每日快照中擷取的區段重要資訊。 本指南概述如何存取和使用UI中的區段控制面板，並提供有關控制面板中顯示之視覺化的詳細資訊。

如需平台使用者介面中所有Adobe Experience Platform區段服務功能的概觀，請造訪[區段服務UI指南](../../segmentation/ui/overview.md)。

## 區段控制面板資料

區段控制面板會顯示您組織在「描述檔儲存在Experience Platform中」中擁有的屬性（記錄）資料快照。 快照不包含任何事件（時間系列）資料。

快照中的屬性資料與拍攝快照時在特定時間點顯示的資料完全相同。 換言之，快照不是資料的近似值或範例，而區段控制面板無法即時更新。

>[!NOTE]
>
>自快照建立以來對資料所做的任何變更或更新，在下一個快照建立之前，不會反映在控制面板中。

## 探索區段控制面板

若要導覽至「平台UI」中的區段控制面板，請在左側導軌中選取&#x200B;**[!UICONTROL Segments]**，然後選取&#x200B;**[!UICONTROL Overview]**&#x200B;標籤以顯示控制面板。

![](../images/segments/dashboard-overview.png)

### 選取區段

控制面板會自動選取要顯示的區段，但您可以變更使用下拉式功能表顯示的區段。 若要選擇不同的區段，請選取區段名稱旁的下拉式清單，然後選取您要檢視的區段。

>[!NOTE]
>
>下拉式功能表顯示您組織目前已建立的所有區段。 這可能表示您需要捲動才能檢視可用區段的完整清單。

![](../images/segments/change-segment.png)

### Widget和量度

區段控制面板由Widget組成，Widget是唯讀度量，提供您所選區段的重要資訊。 介面工具集上的「上次更新」日期和時間會顯示資料的最後快照拍攝時間。

![](../images/segments/widget-timestamp.png)

## 可用的Widget

Experience Platform提供多個Widget，您可用來視覺化與區段相關的不同量度。 選取下方介面工具集的名稱，以瞭解更多：

* [[!UICONTROL Segment size]](#segment-size)
* [[!UICONTROL Profiles added over time]](#profiles-added-over-time)
* [[!UICONTROL Profiles by namespace]](#profiles-by-namespace)

### [!UICONTROL Segment size] {#segment-size}

**[!UICONTROL Segment size]**&#x200B;介面工具集顯示拍攝快照時所選區段內合併的描述檔總數。 此數字是將區段合併原則套用至您的描述檔資料，以便將描述檔片段合併為區段中的每個個人，以形成單一描述檔的結果。

有關碎片和合併配置檔案的詳細資訊，請從閱讀[即時客戶配置檔案概述](../../profile/home.md)開始。

![](../images/segments/segment-size.png)

### [!UICONTROL Profiles added over time] {#profiles-added-over-time}

**[!UICONTROL Profiles added over time]**&#x200B;介面工具集提供有關過去30天在每日快照中擷取的區段描述檔總數的資訊。 此介面工具集會顯示當新設定檔符合區段或退出區段時，區段大小在30天期間可能發生的變化。

若要進一步瞭解區段評估以及設定檔如何符合區段並退出區段，請參閱[區段服務檔案](../../segmentation/home.md)。

![](../images/segments/profiles-added-over-time.png)

### [!UICONTROL Profiles by namespace] {#profiles-by-namespace}

**[!UICONTROL Profiles by namespace]**&#x200B;介面工具集會顯示所選區段中所有合併描述檔的名稱空間劃分。 依身分名稱空間（介面工具集中的[!UICONTROL ID namespace]）劃分的描述檔總數可能高於區段中的描述檔總數，因為一個描述檔可能有多個與其關聯的命名空間。 換言之，將每個名稱空間顯示的值加在一起，可能總計會超過區段中的描述檔總計，因為如果客戶在多個通道上與您的品牌互動，則多個名稱空間可能會與該個別客戶相關聯。

若要進一步瞭解身分名稱空間，請造訪[Adobe Experience Platform身分服務檔案](../../identity-service/home.md)。

![](../images/segments/profiles-by-namespace.png)

## 後續步驟

依照本檔案，您現在應該可以找到區段控制面板並選取要檢視的區段。 您也應瞭解可用Widget中顯示的量度。 若要進一步瞭解如何在Experience PlatformUI中使用區段，請參閱[區段服務UI指南](../../segmentation/ui/overview.md)。
