---
keywords: Experience Platform;user interface;UI;customization;license usage dashboard;dashboard;license usage;entitlement;consumption
title: 授權使用儀表板
description: '本指南概述Adobe Experience Platform UI中提供的授權使用控制面板。 '
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 63758450276d47e7e0eddeb047779222cb80a3e2
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 2%

---


# (Alpha)授權 [!UICONTROL 使用儀表板] {#license-usage-dashboard}

>[!IMPORTANT]
>
>本檔案中概述的控制面板功能目前為alpha版，並非所有使用者都能使用。 文件和功能可能會有所變更。

Adobe Experience Platform使用者介面(UI)提供儀表板，您可透過儀表板檢視有關組織授權使用情況的重要資訊，如每日快照中所擷取。 本指南概述如何存取和使用UI中的授權使用控制面板，並提供有關控制面板中顯示視覺化的詳細資訊。

如需平台UI的一般概觀，請造訪 [Experience Platform UI指南](ui-guide.md)。

## 授權使用資料板資料

授權使用控制面板會顯示貴組織Experience Platform授權相關資料的快照。 儀表板中的資料與拍攝快照時在特定時間點顯示的資料完全相同。 換言之，快照不是資料的近似值或範例，而且控制面板不會即時更新。

>[!NOTE]
>
>自快照建立以來對資料所做的任何變更或更新，在下一個快照建立之前，不會反映在控制面板中。

## 探索授權使用儀表板

若要導覽至「平台UI」中的「授權使用情況」控制面板，請選取 **[!UICONTROL 左側導軌中的]** 「授權使用情況」。 此頁籤隨即開啟， **[!UICONTROL 其中顯示]** 「概述」頁籤。

![](images/license-usage-dashboard/dashboard-overview.png)

### 選取沙盒

若要選擇要在儀表板中檢視的沙盒，請選取「 [!UICONTROL Production] 」或「 [!UICONTROL Development」]。 選取的沙盒會以沙盒名稱旁的選項按鈕來指示。

>[!NOTE]
>
>相同類型的所有沙盒會累積沙盒的耗用量報告。 換言之，選取「 [!UICONTROL Production] 」（製作）或「 [!UICONTROL Development] 」（開發）將分別報告所有生產或開發沙盒。

![](images/license-usage-dashboard/select-sandbox.png)

### 選擇日期範圍

選取沙盒後，您可以使用日期範圍下拉式清單來選取要在控制面板中顯示的時段。 有三種可用選項： [!UICONTROL 最近30天]、 [!UICONTROL 最近90天], [!UICONTROL 以及最近12個月]。 預設會選取最近30天。

![](images/license-usage-dashboard/select-date-range.png)

### Widget和量度

授權使用控制面板由Widget組成，其中顯示唯讀量度，提供有關貴組織授權使用的重要資訊。 若要進一步瞭解這些Widget，請參閱本指南中的可用Widget區段。

## 可用的Widget {#available-widgets}

Experience Platform目前提供一個Widget，您可用來視覺化授權使用，並且很快推出更多Widget。

### [!UICONTROL 可定址的觀眾] {#addressable-audiences}

「可定 **[!UICONTROL 址對象]** 」介面工具集會在套用系統產生的合併原則後，使用確定（私用）圖形演算法來結合所有現有資料集，測量「描述檔」商店中存在的對象總數。 用於計算此量度的合併原則是由平台產生且無法編輯，也無法選取不同的合併原則。

![](images/license-usage-dashboard/addressable-audiences.png)

## 其他控制面板

Platform UI提供其他控制面板，以在Experience Platform中檢視資料的快照。 這些控制面板包括即時客戶個人檔案和區段。 如需這些控制面板的詳細資訊，請從下列連結中選取：

* [[!DNL Profile] 控制面板](../profile/ui/profile-dashboard.md)
* [區段控制面板](../segmentation/ui/segment-dashboard.md)

## 後續步驟

依照本檔案，您現在應該可以找到授權使用控制面板，並選取要檢視的沙盒。 您也應瞭解可用Widget中顯示的量度。 若要進一步瞭解Experience Platform UI，請參閱「平台UI [指南」](ui-guide.md)。