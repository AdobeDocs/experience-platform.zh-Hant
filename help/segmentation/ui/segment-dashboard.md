---
keywords: Experience Platform;profile;segment;segments;segmentation;user interface;UI;customization;segment dashboard;dashboard
title: 區段控制面板
description: '本指南概述Adobe Experience Platform UI中提供的區段控制面板。 '
topic: guide
type: Documentation
translation-type: tm+mt
source-git-commit: 63758450276d47e7e0eddeb047779222cb80a3e2
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 1%

---


# (Alpha)區段控制面板 {#segment-dashboard}

>[!IMPORTANT]
>
>本檔案中概述的控制面板功能目前為alpha版，並非所有使用者都能使用。 文件和功能可能會有所變更。

Adobe Experience Platform使用者介面(UI)提供控制面板，您可透過此控制面板檢視每日快照期間擷取的區段重要資訊。 本指南概述如何存取和使用UI中的區段控制面板，並提供有關控制面板中顯示之視覺化的詳細資訊。

如需平台使用者介面中所有Adobe Experience Platform分段服務功能的概觀，請造訪分段服 [務UI指南](overview.md)。

## 區段控制面板資料

區段控制面板會顯示您組織在Experience Platform的「設定檔」儲存區中擁有的屬性（記錄）資料快照。 快照不包含任何事件（時間系列）資料。

快照中的屬性資料與拍攝快照時在特定時間點顯示的資料完全相同。 換言之，快照不是資料的近似值或範例，而區段控制面板無法即時更新。

>[!NOTE]
>
>自快照建立以來對資料所做的任何變更或更新，在下一個快照建立之前，不會反映在控制面板中。

## 探索區段控制面板

若要導覽至「平台UI」中的區段控制面板，請選取左側邊欄中的「 **[!UICONTROL 區段]** 」，然後選取「 **[!UICONTROL 概述]** 」標籤以顯示控制面板。

![](../images/ui/segment-dashboard/dashboard-overview.png)

### 選取區段

若要選取要在控制面板中檢視的區段，請為「選取區段」文字方塊選 **[!UICONTROL 擇對話]** 選取器。

![](../images/ui/segment-dashboard/select-segment.png)

>[!NOTE]
>
>如果已選取區段，請使用先 `X` 移除區段，然後會出現對話選取器。
>
>![](../images/ui/segment-dashboard/remove-segment.png)

「選 **[!UICONTROL 取區段]** 」對話方塊隨即開啟，可讓您選擇要檢視的區段。 選擇您想要的區段後，請使 **[!UICONTROL 用]** 「選取」返回控制面板。

![](../images/ui/segment-dashboard/select-segment-dialog.png)

### 合併原則

選取區段後，合併原則文字方塊會自動填入與該區段相關的合併原則。

若要進一步瞭解如何在Experience Platform中建立區段，請造訪區 [段產生器UI指南](segment-builder.md)。 有關合併策略的更多資訊，請從閱讀即時客 [戶概要資訊開始](../../profile/home.md)。

![](../images/ui/segment-dashboard/merge-policy.png)

### Widget和量度

區段控制面板由widget組成，widget是唯讀度量，提供您所選區段的重要資訊。 介面工具集上的「上次更新」日期和時間會顯示資料的最後快照拍攝時間。

![](../images/ui/segment-dashboard/widget-timestamp.png)

## 可用的Widget

Experience Platform提供多個Widget，您可使用這些Widget來視覺化與您區段相關的不同量度。 選取下方介面工具集的名稱，以瞭解更多：

* [[!UICONTROL 區段大小]](#segment-size)
* [[!UICONTROL 依命名空間劃分的描述檔]](#profiles-by-namespace)

### [!UICONTROL 區段大小] {#segment-size}

「區 **[!UICONTROL 段大小]** 」介面工具集會顯示拍攝快照時，所選區段內合併的描述檔總數。 此數字是將區段合併原則套用至您的描述檔資料，以便將描述檔片段合併為區段中的每個個人，以形成單一描述檔的結果。

如需有關片段和合併描述檔的詳細資訊，請先閱讀即時 [客戶描述檔概觀](../home.md)。

![](../images/ui/segment-dashboard/segment-size.png)

### [!UICONTROL 依命名空間劃分的描述檔] {#profiles-by-namespace}

「依命 **[!UICONTROL 名空間]** 」介面工具集會顯示所選區段中所有合併描述檔的名稱空間劃分。 依 [!UICONTROL ID命名空間] （換言之，將每個名稱空間顯示的值加在一起）的描述檔總數通常會高於區段中的描述檔總數，因為一個描述檔可能有多個與其相關聯的名稱空間。 例如，如果客戶在多個通道上與您的品牌互動，則可能會與該個別客戶關聯多個名稱空間。

若要進一步瞭解身分名稱空間，請造訪 [Adobe Experience Platform Identity Service檔案](../../identity-service/home.md)。

![](../images/ui/segment-dashboard/profiles-by-namespace.png)

## 其他控制面板

Platform UI提供其他控制面板，以在Experience Platform中檢視資料的快照。 這些控制面板包括即時客戶個人檔案和授 [!UICONTROL 權使用]。 如需這些額外控制面板的詳細資訊，請從下列連結中選取：

* [[!DNL Profile] 控制面板](../../profile/ui/profile-dashboard.md)
* [[!UICONTROL 授權使用儀表板] (License Usage Dashboard)](../../landing/license-usage-dashboard.md)

## 後續步驟

依照本檔案，您現在應該可以找到區段控制面板並選取要檢視的區段。 您也應瞭解可用Widget中顯示的量度。 若要進一步瞭解如何在Experience Platform UI中使用區段，請參閱區段服 [務UI指南](overview.md)。