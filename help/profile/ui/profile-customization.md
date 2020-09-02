---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: 設定檔詳細資訊自訂
description: '本指南提供逐步指示，以自訂在Adobe Experience Platform UI中顯示即時客戶個人檔案資料的方式。 '
topic: guide
translation-type: tm+mt
source-git-commit: b08644102e6455d4c4c8b03e747411d3c05c7deb
workflow-type: tm+mt
source-wordcount: '1224'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] 詳細定制 {#profile-detail-customization}

在Adobe Experience Platform使用者介面中，您可以以客戶個人檔案的形 [!DNL Real-time Customer Profile] 式檢視資料並與之互動。 UI中顯示的描述檔資訊已從多個描述檔片段合併在一起，以形成每個客戶的單一檢視。 這包括基本屬性、連結身分和頻道偏好設定等詳細資訊。 配置檔案中顯示的預設欄位也可以在組織級別進行更改以顯示首選 [!DNL Profile] 屬性。 本指南提供逐步指示，以自訂資料在平台UI [!DNL Profile] 中的顯示方式。

如需描述檔UI的完整 [!UICONTROL 指南] ，請造訪 [Profile使用指南](user-guide.md)。

## 重新排序卡片並調整其大小 {#reorder-and-resize-cards}

從客戶個 [!UICONTROL 人檔案的] 「詳細資訊」標籤中，您可以選取「修改控制面板 **** 」，以調整現有卡片的大小並重新排序。

![](../images/profile-customization/profiles-modify-dashboard.png)

在選擇修改控制面板後，您可以選取卡片標題並將卡片拖放至所需順序，以重新排序卡片。 您也可以選取卡片(`⌟`)右下角的角度符號，並將卡片拖曳至所要的大小，以調整卡片的大小。 在此範例中， **[!UICONTROL Basic屬性]** (Basic attributes)卡會重新調整大小。

![](../images/profile-customization/profiles-resize-cards.png)

所選卡片調整為所需大小，並動態地重新定位周圍的卡片。 這可能會導致某些卡片移至其他列，因此您必須向下捲動才能查看所有卡片。 例如，當 [!UICONTROL Basic attributes] card重新調整大小時，Linked identifities  card將不再顯示在頂端列上，而現在會顯示在描述檔內的新第二列上（未顯示）。 若要將 [!UICONTROL Linked Identities] card傳回至最上方的列，您可將它拖放至Channel偏好設定卡的 [!UICONTROL 目前位置] 。

![](../images/profile-customization/profiles-card-resized.png)

## 編輯和移除卡片

除了調整卡片大小和重新排序外，您還可以編輯特定卡片的內容，並完全從控制面板移除某些卡片。 選取卡片右上`...`角的橢圓形()，以進行編輯或移除。 這會開啟下拉式清單，其中包含編輯或移除卡片的選項，視所選卡片的屬性而定。

>[!NOTE]
>
>並非所有卡片都可以編輯或移除。 這是因為有些卡片包含唯讀或必要的資訊。 如果卡片的右上角沒有橢圓形，它會包含唯讀AND必要資訊，而且無法編輯，也無法移除。 如果卡片的角落有橢圓形，並選取它時，只會顯示移除卡片的選項，卡片資訊是唯讀的，無法編輯。

![](../images/profile-customization/profiles-edit-remove-resized.png)

在下拉 **[!UICONTROL 式清單中選取「編輯]** 」以開啟「編輯介面工具集 **[!UICONTROL 」工作區，您可在此處更新卡片標題、重新排序或移除可見屬性，或使用「新增屬性」按鈕新增其他屬性]** 。

![](../images/profile-customization/profiles-edit-widget-basic-attributes.png)

## 新增屬性 {#add-attributes}

從「編 [!UICONTROL 輯介面工具集] 」畫面中，選 **[!UICONTROL 取卡片右上角的「新增屬性]** 」，開始新增屬性至該卡片。

![](../images/profile-customization/profiles-edit-widget-basic-add-attributes.png)

當「選 [!UICONTROL 擇聯合模式」欄位] ，對話框的左側顯示完整 [!UICONTROL XDM Individual Profile] union模式，其下嵌有欄位。 有關聯合方案的詳細資訊，請參閱 [使用手冊的聯合 [!DNL Profile] 方案部分](user-guide.md#union-schema)。

對 **[!UICONTROL 話方塊右側的「選取的屬性]** 」區段會顯示目前包含在您編輯的卡片中的屬性。 您也可以在這裡移除和重新排序屬性。 顯示所選屬性的總數，以及可添加到單張卡的最大屬性數(20)。

![](../images/profile-customization/profiles-select-field-before.png)

您可以選擇任何可用的聯合架構欄位，以自定義正在編輯的卡上的屬性。 選定欄位旁帶有複選標籤，並自動添加到選定屬性的清單中。 在您新增要在卡片上顯示的所有屬性後，選擇「選取」 **** ，返回「編輯介面工具集 [!UICONTROL 」畫面] 。

![](../images/profile-customization/profiles-select-field-after.png)

當您返回「編輯 [!UICONTROL 介面工具集] 」畫面時，現在應更新資訊卡上的屬性清單，以反映您的選擇。 您仍可以移除或重新排序卡片屬性，或視需要編輯卡片標題。 編輯完成後，請選取「 **[!UICONTROL 儲存]** 」以儲存變更。

![](../images/profile-customization/profiles-edit-widget-new-attributes.png)

儲存後，您會返回「詳細資 [!UICONTROL 訊] 」標籤，其中會顯示更新的資訊卡和屬性。

![](../images/profile-customization/profiles-resized-card-new-attributes.png)

## Add a new card {#add-a-new-card}

若要進一步自訂Experience Platform中描述檔的外觀，您可以選擇將新卡片新增至控制面板，並選取您要在這些卡片上顯示的屬性。 首先，在「詳細信 **[!UICONTROL 息」頁籤上]** ，選擇「修 [!UICONTROL 改控制面板] 」。

![](../images/profile-customization/profiles-modify-dashboard.png)

接著，選 **[!UICONTROL 取控制面板左上角]** 「新增介面工具集」。

![](../images/profile-customization/profiles-add-widget.png)

選擇新卡片會開啟「編輯介面工具集  」畫面，您可在其中提供新卡片的標題，並選擇您要顯示該卡片的屬性。 若要開始新增屬性至卡片，請選取「新 **[!UICONTROL 增屬性」]**。

![](../images/profile-customization/profiles-edit-new-widget.png)

當「選 **[!UICONTROL 擇聯合模式]** 」欄位對話框開啟時，對話框的左側顯示完整的 **** XDM單個配置檔案聯合模式，對話框右側的「選定屬性」部分顯示您為卡選擇的屬性。 有關添加屬性的詳細資訊，請參 [閱有關添加屬性的一節](#add-attributes) ，該節在本文檔前面部分顯示。

顯示所選屬性的總數，以及可添加到單張卡的最大屬性數(20)。 您也可以從此畫面移除和重新排序選取的屬性。 新增您想要顯示在資訊卡上的所有屬性後，選擇「選取」 **** ，返回「編輯介 [!UICONTROL 面工具集] 」畫面。

![](../images/profile-customization/profiles-add-fields-new-widget.png)

當您返回「編輯介 [!UICONTROL 面工具集] 」畫面時，卡片上的屬性清單應反映您在上一個畫面中的選擇。 您也可以視需要重新排序及移除卡片屬性。

若要儲存新卡片 **[!UICONTROL ，您必須先提供卡片標題]**，然後才能選取「 **[!UICONTROL Save]** 」（儲存）並完成卡片建立程式。

![](../images/profile-customization/profiles-edit-new-widget-with-fields.png)

儲存後，您會返回「詳細資 [!UICONTROL 料] 」標籤，其中會顯示新卡片和屬性。

![](../images/profile-customization/profiles-detail-new-widget.png)

## 還原預設卡片

如果您決定要移除您的編輯並返回預設檢視，則可以快速輕鬆地還原所有預設卡片和屬性。 若要這麼做，請選取「修 **[!UICONTROL 改控制面板]**」，然後選 **[!UICONTROL 取「還原預設卡片」]**。 這會移除您進行的所有自訂（包括重新調整大小）。 然後，您可以選 **[!UICONTROL 取「儲存]****** 」以儲存變更，或如果您不想復原預設值，請選取「取消」以保留您所做的編輯。

>[!NOTE]
>
>在還原預設卡片和屬性時請格外小心。 在還原並儲存預設值後，返回檢視自訂項目的唯一方式，就是使用本檔案中概述的步驟，重新建立自訂項目。

![](../images/profile-customization/profiles-restore-default.png)

## 後續步驟

遵循本檔案，您現在應該可以更新組織的描述檔檢視，包括新增和移除卡片、編輯卡片詳細資料和屬性，以及重新排序和調整卡片大小。 若要進一步瞭解如何在 [!DNL Profile] Experience Platform UI中使用資料，請參閱使 [[!DNL Profile] 用指南](user-guide.md)。