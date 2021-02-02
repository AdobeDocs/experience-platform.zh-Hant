---
keywords: Experience Platform;profile;real-time customer profile;user interface;UI;customization;profile details;details
title: 自訂您在UI中檢視描述檔的方式
description: '本指南提供逐步指示，以自訂在Adobe Experience Platform UI中顯示即時客戶個人檔案資料的方式。 '
topic: guide
translation-type: tm+mt
source-git-commit: e6ecc5dac1d09c7906aa7c7e01139aa194ed662b
workflow-type: tm+mt
source-wordcount: '1185'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] 詳細定制  {#profile-detail-customization}

在Adobe Experience Platform使用者介面中，您可以以客戶個人檔案的形式檢視並與[!DNL Real-time Customer Profile]資料互動。 UI中顯示的描述檔資訊已從多個描述檔片段合併在一起，以形成每個客戶的單一檢視。 這包括基本屬性、連結身分和頻道偏好設定等詳細資訊。 配置檔案中顯示的預設欄位也可以在組織級別更改，以顯示首選的[!DNL Profile]屬性。 本指南提供逐步說明，以自訂在平台UI中顯示[!DNL Profile]資料的方式。

如需描述檔UI的完整指南，請造訪[描述檔UI指南](user-guide.md)。

## 重新排序卡片並調整卡片大小{#reorder-and-resize-cards}

從客戶個人檔案的&#x200B;**[!UICONTROL Detail]**&#x200B;標籤中，您可以選取&#x200B;**[!UICONTROL Modify dashboard]**&#x200B;來調整現有卡片的大小和重新排序。

![](../images/profile-customization/profiles-modify-dashboard.png)

在選擇修改控制面板後，您可以選取卡片標題並將卡片拖放至所需順序，以重新排序卡片。 您也可以選取卡片右下角的角度符號(`⌟`)，並將卡片拖曳至所需的大小，以調整卡片的大小。 在此示例中，**[!UICONTROL 基本屬性]**&#x200B;卡的大小正在調整。

![](../images/profile-customization/profiles-resize-cards.png)

所選卡片調整為所需大小，並動態地重新定位周圍的卡片。 這可能會導致某些卡片移至其他列，因此您必須向下捲動才能查看所有卡片。 例如，當&quot;[!UICONTROL 基本屬性]&quot;卡片重新調整大小時，&quot;[!UICONTROL 連結身分]&quot;卡片不再顯示在頂端列上，現在會顯示在描述檔中的新第二列上（未顯示）。 若要將「[!UICONTROL 連結的身分識別]」卡傳回至最上方的列，您可將它拖放至「[!UICONTROL 頻道偏好設定]」卡的目前位置。

![](../images/profile-customization/profiles-card-resized.png)

## 編輯和移除卡片

除了調整卡片大小和重新排序外，您還可以編輯特定卡片的內容，並完全從控制面板移除某些卡片。 選取卡片右上角的省略號(`...`)以進行編輯或移除。 這會開啟下拉式清單，其中包含編輯或移除卡片的選項，視所選卡片的屬性而定。

>[!NOTE]
>
>並非所有卡片都可以編輯或移除。 這是因為有些卡片包含唯讀或必要的資訊。 如果卡片的右上角沒有橢圓形，它會包含唯讀AND必要資訊，而且無法編輯，也無法移除。 如果卡片的角落有橢圓形，並選取它時，只會顯示移除卡片的選項，卡片資訊是唯讀的，無法編輯。

![](../images/profile-customization/profiles-edit-remove-resized.png)

在下拉式清單中選取「編輯」**[!UICONTROL 「編輯」]**&#x200B;以開啟「編輯介面工具集」工作區，您可在此處更新卡片標題、重新排序或移除可見屬性，或使用「新增屬性」按鈕新增其他屬性。********

![](../images/profile-customization/profiles-edit-widget-basic-attributes.png)

## 添加屬性{#add-attributes}

從&#x200B;**[!UICONTROL 編輯介面工具集]**&#x200B;畫面中，選擇卡片右上角的&#x200B;**[!UICONTROL 新增屬性]**，開始新增屬性至該卡片。

![](../images/profile-customization/profiles-edit-widget-basic-add-attributes.png)

當&#x200B;**[!UICONTROL 選擇聯合模式欄位]**&#x200B;對話框開啟時，對話框的左側顯示完整的[!UICONTROL XDM單個配置檔案]聯合模式，其下嵌有欄位。 有關聯合架構的詳細資訊，請參閱 [!DNL Profile] 使用手冊](user-guide.md#union-schema)的[聯合架構部分。

對話框右側的&#x200B;**[!UICONTROL 選定屬性]**&#x200B;部分顯示當前包含在您正在編輯的卡片中的屬性。 您也可以在這裡移除和重新排序屬性。 顯示所選屬性的總數，以及可添加到單張卡的最大屬性數(20)。

![](../images/profile-customization/profiles-select-field-before.png)

您可以選擇任何可用的聯合架構欄位，以自定義正在編輯的卡上的屬性。 選定欄位旁帶有複選標籤，並自動添加到選定屬性的清單中。 在您新增要在卡片上顯示的所有屬性後，選擇&#x200B;**[!UICONTROL 選擇]**&#x200B;以返回&#x200B;**[!UICONTROL 編輯介面工具集]**&#x200B;畫面。

![](../images/profile-customization/profiles-select-field-after.png)

當您返回&#x200B;**[!UICONTROL 編輯介面工具集]**&#x200B;畫面時，現在應更新資訊卡上的屬性清單，以反映您的選擇。 您仍可以移除或重新排序卡片屬性，或視需要編輯卡片標題。 完成編輯後，選擇&#x200B;**[!UICONTROL Save]**&#x200B;以保存更改。

![](../images/profile-customization/profiles-edit-widget-new-attributes.png)

儲存後，您會返回至&#x200B;**[!UICONTROL Detail]**&#x200B;標籤，其中會顯示更新的卡片和屬性。

![](../images/profile-customization/profiles-resized-card-new-attributes.png)

## 新增卡片{#add-a-new-card}

若要進一步自訂Experience Platform中描述檔的外觀，您可以選擇將新卡片新增至控制面板，並選取您要在這些卡片上顯示的屬性。 首先，在&#x200B;**[!UICONTROL Detail]**&#x200B;標籤上選擇&#x200B;**[!UICONTROL Modify dashboard]**。

![](../images/profile-customization/profiles-modify-dashboard.png)

接著，在控制面板左上角選擇「新增Widget ]**」。**[!UICONTROL 

![](../images/profile-customization/profiles-add-widget.png)

選擇新增卡片會開啟&#x200B;**[!UICONTROL 編輯介面工具集]**&#x200B;畫面，您可在其中提供新卡片的標題，並選擇您希望卡片顯示的屬性。 要開始向卡中添加屬性，請選擇&#x200B;**[!UICONTROL 添加屬性]**。

![](../images/profile-customization/profiles-edit-new-widget.png)

當&#x200B;**[!UICONTROL 選擇聯合模式欄位]**&#x200B;對話框開啟時，對話框的左側顯示完整的[!UICONTROL XDM單個配置檔案]聯合模式，對話框右側的&#x200B;**[!UICONTROL 選擇的屬性]**&#x200B;部分顯示您為卡選擇的屬性。 有關添加屬性的詳細資訊，請參閱本文檔前面顯示的有關添加屬性](#add-attributes)的[部分。

顯示所選屬性的總數，以及可添加到單張卡的最大屬性數(20)。 您也可以從此畫面移除和重新排序選取的屬性。 在您新增想要顯示在資訊卡上的所有屬性後，選擇&#x200B;**[!UICONTROL 選擇]**&#x200B;以返回至&#x200B;**[!UICONTROL 編輯介面工具集]**&#x200B;畫面。

![](../images/profile-customization/profiles-add-fields-new-widget.png)

當您返回&#x200B;**[!UICONTROL 編輯介面工具集]**&#x200B;畫面時，卡片上的屬性清單應反映您在上一個畫面中的選擇。 您也可以視需要重新排序及移除卡片屬性。

若要儲存新卡片，您必須先提供&#x200B;**[!UICONTROL 卡片標題]**，然後您就可以選取&#x200B;**[!UICONTROL 儲存]**&#x200B;並完成卡片建立程式。

![](../images/profile-customization/profiles-edit-new-widget-with-fields.png)

儲存後，您會返回至&#x200B;**[!UICONTROL Detail]**&#x200B;標籤，其中會顯示新卡片和屬性。

![](../images/profile-customization/profiles-detail-new-widget.png)

## 還原預設卡片

如果您決定要復原已移除的預設卡片，則可快速輕鬆地完成。 首先，選擇「修改儀表板」**[!UICONTROL ，然後選擇「恢復預設卡片」]**。 ]****[!UICONTROL &#x200B;在顯示預設卡片後，您可以選擇&#x200B;**[!UICONTROL 保存]**&#x200B;以保存更改，或者選擇&#x200B;**[!UICONTROL 取消]**（如果不希望恢復預設卡片）。

![](../images/profile-customization/profiles-restore-default.png)

## 後續步驟

遵循本檔案，您現在應該可以更新組織的描述檔檢視，包括新增和移除卡片、編輯卡片詳細資料和屬性，以及重新排序和調整卡片大小。 若要進一步瞭解如何在Experience Platform UI中使用[!DNL Profile]資料，請參閱[[!DNL Profile] 使用指南](user-guide.md)。