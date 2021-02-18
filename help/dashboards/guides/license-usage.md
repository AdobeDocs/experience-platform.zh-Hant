---
keywords: Experience Platform；用戶介面；UI;customization;license usage dashboard;dashboard;license usage;entitlement；衝減
title: 授權使用儀表板
description: Adobe Experience Platform提供儀表板，您可以透過儀表板檢視有關貴組織授權使用的重要資訊。
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 084aaa315f694d696abee7f078be3a121111f6cc
workflow-type: tm+mt
source-wordcount: '594'
ht-degree: 1%

---


# （測試版）[!UICONTROL 授權使用]控制面板{#license-usage-dashboard}

>[!IMPORTANT]
>
>本檔案中概述的控制面板功能目前為測試版，並非所有使用者都能使用。 文件和功能可能會有所變更。

Adobe Experience Platform使用者介面(UI)提供儀表板，您可透過儀表板檢視有關組織授權使用情況的重要資訊，如每日快照中所擷取。 本指南概述如何存取和使用UI中的授權使用控制面板，並提供有關控制面板中顯示視覺化的詳細資訊。

如需平台UI的一般概觀，請造訪[體驗平台UI指南](../../landing/ui-guide.md)。

## 授權使用資料板資料

授權使用控制面板會顯示貴組織Experience Platform授權相關資料的快照。 儀表板中的資料與拍攝快照時在特定時間點顯示的資料完全相同。 換言之，快照不是資料的近似值或範例，而且控制面板不會即時更新。

>[!NOTE]
>
>自快照建立以來對資料所做的任何變更或更新，在下一個快照建立之前，不會反映在控制面板中。

## 探索授權使用儀表板

若要導覽至平台UI中的授權使用控制面板，請在左側導軌中選取「**[!UICONTROL 授權使用]**」。 此時會開啟&#x200B;**[!UICONTROL 概述]**&#x200B;標籤，顯示控制面板。

![](../images/license-usage/dashboard-overview.png)

### 選取沙盒

若要選擇要在儀表板中查看的沙盒，請選擇[!UICONTROL Production]或[!UICONTROL Development]。 選取的沙盒會以沙盒名稱旁的選項按鈕來指示。

>[!NOTE]
>
>相同類型的所有沙盒會累積沙盒的耗用量報告。 換言之，選擇[!UICONTROL Production]或[!UICONTROL Development]將分別報告所有生產或開發沙盒。

![](../images/license-usage/select-sandbox.png)

### 選擇日期範圍

選取沙盒後，您可以使用日期範圍下拉式清單來選取要在控制面板中顯示的時段。 有三種可用選項：[!UICONTROL 最近30天]、[!UICONTROL 最近90天]和[!UICONTROL 最近12個月]。 預設會選取最近30天。

![](../images/license-usage/select-date-range.png)

### Widget和量度

授權使用控制面板由Widget組成，其中顯示唯讀量度，提供有關貴組織授權使用的重要資訊。 若要進一步瞭解這些Widget，請參閱本指南中的可用Widget區段。

## 可用Widget {#available-widgets}

Experience Platform目前提供一個Widget，您可用來視覺化授權使用，並且很快推出更多Widget。

### [!UICONTROL 可定址的觀眾] {#addressable-audiences}

**[!UICONTROL 可定址對象]**&#x200B;介面工具集會在套用系統產生的合併原則後，使用確定（私用）圖形演算法來合併所有目前資料集的描述檔片段，顯示描述檔資料儲存區內的合併描述檔總數。

有關片段和合併配置檔案的詳細資訊，請首先閱讀[配置檔案概述](../../profile/home.md)的&#x200B;*配置檔案片段與合併配置檔案*&#x200B;部分。

>[!NOTE]
>
>用於計算此量度的合併原則是由Experience Platform產生且無法編輯，也無法選取不同的合併原則。 此系統產生的合併原則與[!DNL Profile]控制面板中用於計算[!UICONTROL 觀眾大小]的預設合併原則不同，因此[!UICONTROL 授權使用]和[!DNL Profile]控制面板中的觀眾計數不太可能完全相同。

![](../images/license-usage/addressable-audiences.png)

## 後續步驟

依照本檔案，您現在應該可以找到授權使用控制面板，並選取要檢視的沙盒。 您也應瞭解可用Widget中顯示的量度。 若要進一步瞭解Experience Platform UI，請參閱[平台UI指南](../../landing/ui-guide.md)。