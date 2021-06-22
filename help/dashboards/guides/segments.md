---
keywords: Experience Platform；設定檔；區段；區段；使用者介面；UI；自訂；區段控制面板；控制面板
title: 區段控制面板
description: 'Adobe Experience Platform提供控制面板，供您檢視貴組織已建立區段的重要資訊。 '
type: Documentation
exl-id: de5e07bc-2c44-416e-99db-7607059117cb
source-git-commit: 2791c32abe582d51d05d4bf0488ba82dfadfd053
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 0%

---

# 區段控制面板{#segment-dashboard}

Adobe Experience Platform使用者介面(UI)提供控制面板，讓您透過控制面板檢視每日快照擷取之區段的重要資訊。 本指南概述如何存取和使用UI中的區段控制面板，並提供控制面板中所顯示視覺效果的詳細資訊。

如需Platform使用者介面中所有Adobe Experience Platform區段服務功能的概觀，請造訪[區段服務UI指南](../../segmentation/ui/overview.md)。

## 區段控制面板資料

區段控制面板會顯示您的組織在「設定檔」存放區內Experience Platform的屬性（記錄）資料快照。 快照不包含任何事件（時間系列）資料。

快照中的屬性資料與建立快照時在特定時間點顯示的資料完全相同。 換句話說，快照不是資料的近似值或樣本，而且區段控制面板不會即時更新。

>[!NOTE]
>
>自拍攝快照以來對資料所做的任何更改或更新都不會反映在儀表板中，直到拍攝下一個快照。

## 探索區段控制面板

若要導覽至Platform UI中的[!UICONTROL Segments]控制面板，請在左側邊欄中選取&#x200B;**[!UICONTROL Segments]**，然後選取&#x200B;**[!UICONTROL Overview]**&#x200B;標籤以顯示控制面板。

>[!NOTE]
>
>如果您的組織是初次使用Platform，且尚未建立作用中的設定檔資料集或合併原則，則不會顯示[!UICONTROL Segments]控制面板。 相反地， [!UICONTROL 概述]標籤會顯示可協助您開始使用細分的連結和檔案。

![](../images/segments/dashboard-overview.png)

### 修改[!UICONTROL 區段]控制面板

您可以選取&#x200B;**[!UICONTROL 修改控制面板]**，以修改[!UICONTROL 區段]控制面板的外觀。 這可讓您從控制面板移動、新增和移除介面工具集，以及存取[!UICONTROL 介面工具集庫]以探索可用介面工具集，並為貴組織建立自訂介面工具集。

請參閱[修改控制面板](../modify.md)和[介面工具集庫](../widget-library.md)檔案以深入了解。

## 選取區段

控制面板會自動選取要顯示的區段，但您可以使用下拉式功能表或區段選取器來變更區段。

若要選擇不同的區段，請選取區段名稱旁的下拉式清單，或使用區段選取器開啟區段選取對話方塊。

![](../images/segments/change-segment.png)

![](../images/segments/select-segment-dialog.png)

## Widget和量度

區段控制面板由Widget組成，Widget是唯讀量度，提供與您所選區段相關的重要資訊。

介面工具集上的「上次更新」日期和時間會顯示資料的最後快照拍攝時間。 快照的日期和時間以UTC提供；不在個別使用者或IMS組織的時區。

![](../images/segments/widget-timestamp.png)

## 可用介面工具集

Experience Platform提供多個小工具集，可用來視覺化與區段相關的不同量度。 選取下方介面工具集的名稱以深入了解：

* [[!UICONTROL 對象大小]](#audience-size)
* [[!UICONTROL 對象大小趨勢]](#audience-size-trend)
* [[!UICONTROL 身分重疊]](#identity-overlap)
* [[!UICONTROL 依身分設定檔]](#profiles-by-identity)

### [!UICONTROL 對象大小] {#audience-size}

**[!UICONTROL 對象大小]**&#x200B;介面工具集會顯示拍攝快照時所選區段內合併的設定檔總數。 此數字是將區段合併原則套用至您的設定檔資料的結果，以便將設定檔片段合併在一起，為區段中的每個個人形成單一設定檔。

如需片段和已合併設定檔的詳細資訊，請先閱讀[即時客戶設定檔概述](../../profile/home.md)開始。

![](../images/segments/audience-size.png)

### [!UICONTROL 對象大小趨勢] {#audience-size-trend}

**[!UICONTROL 對象大小趨勢]**&#x200B;介面工具集提供有關過去30天、90天或12個月中，在每日快照期間擷取的區段中設定檔總數的資訊。 此介面工具集顯示隨著新設定檔符合區段或退出區段，區段大小可能會隨著時間而改變。

若要進一步了解區段評估以及設定檔如何限定和退出區段，請參閱[分段服務檔案](../../segmentation/home.md)。

![](../images/segments/audience-size-trend.png)

### [!UICONTROL 身分重疊] {#identity-overlap}

**[!UICONTROL 身分重疊]**&#x200B;介面工具集會顯示Venn圖表或設定圖，顯示包含多個身分之區段中設定檔的重疊。

使用介面工具集上的下拉式功能表來選取您要比較的身分後，圓圈會顯示每個身分的相對大小，包含兩個命名空間的設定檔數目會以圓圈之間重疊的大小來表示。

如果客戶在多個管道上與您的品牌互動，則多個身分會與該個別客戶相關聯，因此您的組織可能會有多個設定檔，其中包含來自多個身分的片段。

若要進一步了解身分，請造訪[Adobe Experience Platform Identity Service檔案](../../identity-service/home.md)。

![](../images/segments/identity-overlap.png)

### [!UICONTROL 依身分設定檔] {#profiles-by-identity}

**[!UICONTROL 依身分設定檔]**&#x200B;介面工具集會顯示您所選區段中所有合併設定檔的身分劃分。 依身分劃分的設定檔總數可能高於區段中的設定檔總數，因為一個設定檔可能有多個與其相關聯的身分。 換句話說，將每個身分顯示的值加總後，可能會超過區段中的總受眾規模，因為如果客戶在多個管道上與您的品牌互動，則多個身分可能會與該個別客戶相關聯。

若要進一步了解身分，請造訪[Adobe Experience Platform Identity Service檔案](../../identity-service/home.md)。

![](../images/segments/profiles-by-identity.png)

## 後續步驟

依照本檔案操作，您現在應該能夠找到區段控制面板，並選取要檢視的區段。 您也應了解可用介面工具集中顯示的量度。 若要進一步了解如何在Experience PlatformUI中使用區段，請參閱[分段服務UI指南](../../segmentation/ui/overview.md)。
