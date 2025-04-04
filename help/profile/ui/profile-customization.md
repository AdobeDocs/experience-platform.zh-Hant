---
keywords: Experience Platform；設定檔；即時客戶設定檔；使用者介面；UI；自訂；設定檔詳細資料；詳細資料
title: UI中的設定檔詳細資料自訂
description: 本指南逐步說明如何自訂Adobe Experience Platform UI中顯示即時客戶設定檔資料的方式。
exl-id: 76cf8420-cc50-4a56-9f6d-5bfc01efcdb3
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile]詳細資料自訂 {#profile-detail-customization}

在Adobe Experience Platform使用者介面中，您可以檢視客戶設定檔形式的[!DNL Real-Time Customer Profile]資料並與之互動。 UI中顯示的設定檔資訊已從多個設定檔片段合併在一起，以形成每個個別客戶的單一檢視。 這包括基本屬性、連結的身分和管道偏好設定等詳細資訊。 設定檔中顯示的預設欄位也可以在組織層級變更以顯示偏好的[!DNL Profile]屬性。 本指南提供逐步指示，說明如何自訂[!DNL Profile]資料在Experience Platform UI中的顯示方式。

如需設定檔UI的完整指南，請造訪[設定檔UI指南](user-guide.md)。

## 重新排序卡片並調整其大小 {#reorder-and-resize-cards}

從客戶設定檔的&#x200B;**[!UICONTROL 詳細資料]**&#x200B;索引標籤中，您可以選取&#x200B;**[!UICONTROL 自訂設定檔詳細資料]**，以調整現有卡片大小並重新排序。

![[自訂設定檔詳細資料]按鈕在[設定檔儀表板]上反白顯示。](../images/profile-customization/customize-profile-details.png)

選擇修改控制面板後，您可以選取卡片標題並將卡片拖放至所需順序來重新排序卡片。 您也可以選取卡片右下角的角度符號(`⌟`)，並將卡片拖曳到想要的大小來調整卡片大小。 在此範例中，正在調整&#x200B;**[!UICONTROL 基本屬性]**&#x200B;卡片的大小。

![基本屬性卡中會醒目顯示調整大小按鈕。](../images/profile-customization/resize.png)

選取的卡片會調整至所需的大小，而周圍的卡片會動態重新定位。 這可能會導致某些卡片被移動到其他列，需要您向下捲動才能看到所有卡片。 例如，當「[!UICONTROL 基本屬性]」卡片調整大小時，「[!UICONTROL 連結的身分]」卡片就不再會顯示在最上列，而現在會顯示在設定檔內的第二個新列上（未顯示）。 若要將「[!UICONTROL 連結的身分]」卡片傳回頂列，您可以將其拖放至「[!UICONTROL 頻道偏好設定]」卡片的目前位置。

![重新調整大小的卡片已反白顯示。](../images/profile-customization/resized.png)

## 編輯與移除卡片

除了調整卡片大小並重新排序之外，您還可以編輯特定卡片的內容並從儀表板中完全移除某些卡片。 選取卡片右上角的省略符號(`...`)，以便編輯或移除它。 這會開啟一個下拉式清單，內含編輯或移除卡片的選項，視所選卡片的屬性而定。

>[!NOTE]
>
>並非所有卡片都可以編輯或移除。 這是因為有些卡片包含唯讀或必要的資訊。 如果卡片右上角沒有橢圓，則包含唯讀的AND必要資訊，無法編輯或移除。 如果卡片在角落有橢圓形，選取它時只顯示移除卡片的選項，則卡片資訊為唯讀狀態且無法編輯。

![編輯卡片下拉式清單會反白顯示。 這包含編輯或移除卡片的選項。](../images/profile-customization/edit-card.png)

在下拉式清單中選取「**[!UICONTROL 編輯]**」以開啟「**[!UICONTROL 編輯Widget]**」工作區，您可以在其中更新卡片標題、重新排序或移除可見的屬性，或使用「**[!UICONTROL 新增屬性]**」按鈕新增其他屬性。

![顯示基本屬性卡。](../images/profile-customization/basic-attributes.png)

## 新增屬性 {#add-attributes}

在&#x200B;**[!UICONTROL 編輯Widget]**&#x200B;畫面中，選取卡片右上角的&#x200B;**[!UICONTROL 新增屬性]**&#x200B;以開始向該卡片新增屬性。

![基本屬性卡中的[新增屬性]按鈕會反白顯示。](../images/profile-customization/add-attributes.png)

當&#x200B;**[!UICONTROL 選取聯合結構描述欄位]**&#x200B;對話方塊開啟時，對話方塊的左側會顯示完整的[!UICONTROL XDM個別設定檔]聯合結構描述，其欄位巢狀位於下方。 如需聯合結構描述的詳細資訊，請參閱 [!DNL Profile] 使用手冊](user-guide.md#union-schema)的[聯合結構描述區段。

對話方塊右側的&#x200B;**[!UICONTROL 選取的屬性]**&#x200B;區段會顯示目前包含在您正在編輯的卡片中的屬性。 您也可以在此移除及重新排序屬性。 畫面會顯示選取的屬性總數，以及可新增至單一卡片的屬性數目上限(20)。

![目前組成卡片屬性的屬性會反白顯示。](../images/profile-customization/select-before.png)

您可以選取任何可用的聯合結構描述欄位，以自訂您正在編輯的卡片上的屬性。 選取欄位時，您可以選擇檢視檔案路徑名稱或顯示名稱。 若要在這兩個顯示之間切換，請選取&#x200B;**[!UICONTROL 顯示顯示名稱]**&#x200B;切換按鈕。

![設定檔詳細資訊頁面中會反白顯示[!UICONTROL 顯示名稱]切換。](../images/profile-customization/show-display-names.png)

選取的欄位旁邊會顯示核取標籤，且會自動新增至選取的屬性清單中。 新增您要顯示在卡片上的所有屬性後，請選擇&#x200B;**[!UICONTROL 選取]**&#x200B;以返回&#x200B;**[!UICONTROL 編輯Widget]**&#x200B;畫面。

![新加入的屬性會反白顯示。](../images/profile-customization/select-after.png)

現在當您返回&#x200B;**[!UICONTROL 編輯Widget]**&#x200B;畫面時，卡片上的屬性清單應該會更新以反映您的選擇。 您仍可移除或重新排序卡片屬性，或視需要編輯卡片標題。 完成編輯後，選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存變更。

![新加入的屬性會顯示在編輯的卡片上。](../images/profile-customization/new-attributes.png)

儲存後，您會返回&#x200B;**[!UICONTROL 詳細資料]**&#x200B;標籤，其中會顯示更新的卡片和屬性。

![新新增的屬性會顯示在設定檔控制面板的卡片上。](../images/profile-customization/added-attributes.png)

## 新增卡片 {#add-a-new-card}

若要進一步自訂Experience Platform中設定檔的外觀，您可以選取將新卡片新增至控制面板，並選取您想在這些卡片顯示的屬性。 若要開始，請在&#x200B;**[!UICONTROL 詳細資料]**&#x200B;索引標籤上選取&#x200B;**[!UICONTROL 修改儀表板]**。

![[自訂設定檔詳細資料]按鈕已反白顯示。](../images/profile-customization/customize-profile-details.png)

接著，選取儀表板左上角的&#x200B;**[!UICONTROL 新增Widget]**。

![[新增Widget]按鈕已反白顯示。](../images/profile-customization/add-widget.png)

選擇新增卡片會開啟&#x200B;**[!UICONTROL 編輯Widget]**&#x200B;畫面，您可以在其中提供新卡片的標題，並選擇您希望卡片顯示的屬性。 若要開始新增屬性至卡片，請選取&#x200B;**[!UICONTROL 新增屬性]**。

![「編輯Widget」畫面中顯示空白的新Widget卡片。](../images/profile-customization/edit-widget.png)

當&#x200B;**[!UICONTROL 選取聯合結構描述欄位]**&#x200B;對話方塊開啟時，對話方塊的左側會顯示完整的[!UICONTROL XDM個別設定檔]聯合結構描述，而對話方塊右側的&#x200B;**[!UICONTROL 選取的屬性]**&#x200B;區段會顯示您為卡片選取的屬性。 如需新增屬性的詳細資訊，請參閱本檔案中關於新增屬性](#add-attributes)的[一節。

畫面會顯示選取的屬性總數，以及可新增至單一卡片的屬性數目上限(20)。 您也可以從此畫面移除並重新排序您選取的屬性。 新增您要顯示在卡片上的所有屬性後，請選擇&#x200B;**[!UICONTROL 選取]**&#x200B;以返回&#x200B;**[!UICONTROL 編輯Widget]**&#x200B;畫面。

![您新增至卡片的欄位會反白顯示。](../images/profile-customization/add-widget-attributes.png)

當您返回&#x200B;**[!UICONTROL 編輯Widget]**&#x200B;畫面時，卡片上的屬性清單應該會反映您在上一個畫面所做的選擇。 您也可以視需要重新排序及移除卡片屬性。

若要儲存新卡片，您必須先提供&#x200B;**[!UICONTROL 卡片標題]**，然後您就可以選取&#x200B;**[!UICONTROL 儲存]**&#x200B;並完成卡片建立程式。

![新的Widget已在「編輯Widget」畫面中預覽。](../images/profile-customization/new-widget.png)

儲存後，您會回到&#x200B;**[!UICONTROL 詳細資料]**&#x200B;標籤，您的新卡片和屬性會在此顯示。

![新Widget已新增至設定檔儀表板。](../images/profile-customization/added-widget.png)

## 還原預設卡片

如果在任何時候您決定要還原已移除的預設卡片，則可以快速輕鬆地加以還原。 首先，選取&#x200B;**[!UICONTROL 修改儀表板]**，然後選取&#x200B;**[!UICONTROL 還原預設卡片]**。 顯示預設卡片後，您可以選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存您的變更，或選取&#x200B;**[!UICONTROL 取消]** （如果您不想還原預設卡片）。

![設定檔儀表板中會醒目顯示[還原預設卡片]按鈕。](../images/profile-customization/restore-default.png)

## 後續步驟

依照此檔案，您現在應該能夠更新組織的設定檔檢視，包括新增和移除卡片，編輯卡片詳細資料和屬性，以及重新排序卡片並重新調整其大小。 若要進一步瞭解如何在Experience Platform UI中使用[!DNL Profile]資料，請參閱[[!DNL Profile] 使用手冊](user-guide.md)。
