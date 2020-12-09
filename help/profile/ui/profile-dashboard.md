---
keywords: Experience Platform;profile;real-time customer profile;user interface;UI;customization;profile dashboard;dashboard
title: 描述檔控制面板
description: '本指南概述Adobe Experience Platform UI中提供的即時客戶個人檔案資料控制面板。 '
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 983b357f2f17aad273f0465dc9250240a062dcd2
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 1%

---


# (Alpha)控制 [!DNL Real-time Customer Profile] 面板 {#profile-dashboard}

>[!IMPORTANT]
>
>本檔案中概述的控制面板功能目前為alpha版，並非所有使用者都能使用。 文件和功能可能會有所變更。

Adobe Experience Platform使用者介面(UI)提供控制面板，您可透過此控制面板檢視每日快照期間所擷取 [!DNL Real-time Customer Profile] 之資料的重要資訊。 本指南概述如何存取和使用UI中 [!DNL Profile] 的控制面板，並提供有關控制面板中顯示之度量的詳細資訊。

如需Experience Platform使用者介面中所有描述檔功能的概述，請造訪即時 [客戶描述檔UI指南](user-guide.md)。

## 描述檔控制面板資料

「描述檔」控制面板會顯示您組織在Experience Platform的「描述檔儲存區」中擁有的屬性（記錄）資料快照。 快照不包含任何事件（時間系列）資料。

快照中的屬性資料與拍攝快照時在特定時間點顯示的資料完全相同。 換言之，快照不是資料的近似值或範例，而「描述檔」控制面板不會即時更新。

>[!NOTE]
>
>自快照建立以來對資料所做的任何變更或更新，在下一個快照建立之前，不會反映在控制面板中。

「描述檔」控制面板中顯示的量度是根據您組織的預設合併原則。 有關合併策略以及如何選擇或更改預設合併策略的詳細資訊，請訪問合 [並策略UI指南](merge-policies.md)。

## 探索描述檔控制面板

若要導覽至「平台UI」中的「描述檔」控制面板，請選取左側邊欄中的「描述檔 **[!UICONTROL 」，然後選取「]** 概述 **** 」索引標籤以顯示控制面板。

![](../images/profile-dashboard/dashboard-overview.png)

### Widget和量度

控制面板由widget組成，widget是唯讀量度，提供您描述檔資料的重要資訊。 介面工具集上的「上次更新」日期和時間會顯示資料的最後快照拍攝時間。

![](../images/profile-dashboard/dashboard-timestamp.png)

## 可用的Widget

Experience Platform提供多個Widget，您可使用這些Widget來視覺化與您的描述檔資料相關的不同量度。 選取下方介面工具集的名稱，以瞭解更多：

* [[!UICONTROL 受眾規模]](#audience-size)
* [[!UICONTROL 依命名空間劃分的描述檔]](#profiles-by-namespace)

### [!UICONTROL 受眾規模] {#audience-size}

「對 **[!UICONTROL 像大小]** 」介面工具集會顯示拍攝快照時，「描述檔」資料儲存區內合併的描述檔總數。 此數字是貴組織預設的合併原則套用至您的描述檔資料的結果，以便將描述檔片段合併為每個個人組成單一描述檔。

如需有關片段和合併描述檔的詳細資訊，請先閱讀描述檔總 [覽的描述檔片段與合併描述檔](../home.md#profile-fragments-vs-merged-profiles) ，以 [開始](../home.md)。

![](../images/profile-dashboard/audience-size.png)

### [!UICONTROL 依命名空間劃分的描述檔] {#profiles-by-namespace}

「依命 **[!UICONTROL 名空間]** 」介面工具集會顯示描述檔儲存區中所有合併描述檔的命名空間劃分。 依 [!UICONTROL ID命名空間] （換言之，將每個名稱空間顯示的值加在一起）的描述檔總數永遠高於合併描述檔總數，因為一個描述檔可能有多個與其相關聯的名稱空間。 例如，如果客戶在多個通道上與您的品牌互動，則多個名稱空間將與該個別客戶關聯。

若要進一步瞭解身分名稱空間，請造訪 [Adobe Experience Platform Identity Service檔案](../../identity-service/home.md)。

![](../images/profile-dashboard/profiles-by-namespace.png)

## 其他控制面板

Platform UI提供其他控制面板，以在Experience Platform中檢視資料的快照。 這些儀表板包括區段和授權使用。 如需這些額外控制面板的詳細資訊，請從下列連結中選取：

* [區段控制面板](../../segmentation/ui/segment-dashboard.md)
* [授權使用儀表板](../../landing/license-usage-dashboard.md)

## 後續步驟

遵循本檔案，您現在應該可以找到描述檔控制面板，並瞭解可用Widget中顯示的量度。 若要進一步瞭解如何在 [!DNL Profile] Experience Platform UI中使用資料，請參閱 [[!DNL Profile] UI指南](user-guide.md)。