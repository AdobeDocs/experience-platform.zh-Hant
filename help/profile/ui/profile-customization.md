---
keywords: Experience Platform；配置檔案；即時客戶配置檔案；用戶介面；UI；自定義；配置檔案詳細資訊；詳細資訊
title: UI中的配置檔案詳細資訊自定義
description: 本指南提供了逐步說明，用於自定義即時客戶配置檔案資料在Adobe Experience PlatformUI中的顯示方式。
exl-id: 76cf8420-cc50-4a56-9f6d-5bfc01efcdb3
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1350'
ht-degree: 0%

---

# [!DNL Real-Time Customer Profile] 細節定制 {#profile-detail-customization}

在Adobe Experience Platform用戶介面中，您可以查看和與 [!DNL Real-Time Customer Profile] 以客戶配置檔案的形式顯示資料。 UI中顯示的配置檔案資訊已從多個配置檔案片段中合併在一起，以形成每個客戶的單個視圖。 這包括基本屬性、連結標識和渠道首選項等詳細資訊。 配置檔案中顯示的預設欄位也可以在組織級別更改以顯示首選欄位 [!DNL Profile] 屬性。 本指南提供了逐步說明，用於自定義 [!DNL Profile] 資料顯示在平台UI中。

有關配置式UI的完整指南，請訪問 [配置檔案UI指南](user-guide.md)。

## 重新排序和調整卡片大小 {#reorder-and-resize-cards}

從 **[!UICONTROL 詳細資訊]** 的子菜單，您可以選擇 **[!UICONTROL 自定義配置檔案詳細資訊]** 以調整現有卡的大小並重新排序。

![「定制配置檔案詳細資訊」(Customize profile details)按鈕在「配置檔案」(Profile)操控板上突出顯示。](../images/profile-customization/customize-profile-details.png)

選擇修改儀表板後，可以通過選擇卡片標題並將卡片拖放到所需的順序來重新排序卡片。 也可以通過選擇卡右下角的角度符號來調整卡的大小(`⌟`)並將卡拖到所需的大小。 在此示例中， **[!UICONTROL 基本屬性]** 正在調整卡的大小。

![調整大小按鈕在基本屬性卡中突出顯示。](../images/profile-customization/resize.png)

所選卡調整到所需尺寸，並動態地重新定位周圍的卡。 這可能會導致某些卡被移動到其他行，這要求您向下滾動以查看所有卡。 例如，當「」[!UICONTROL 基本屬性]&quot;卡的大小已調整為&quot;[!UICONTROL 連結的身份]&quot;卡在頂行上不再可見，現在顯示在配置檔案中的新第二行（未顯示）上。 返回「」[!UICONTROL 連結的身份]&quot;卡到頂行，可將其拖放到「 」的當前位置[!UICONTROL 頻道首選項]」卡。

![選中重新調整大小的卡。](../images/profile-customization/resized.png)

## 編輯和刪除卡

除了調整卡片大小和重新排序外，您還可以編輯某些卡片的內容並從儀表板中完全刪除某些卡片。 選取橢圓(`...`)，以便編輯或刪除該卡。 此時將開啟一個下拉清單，其中包含編輯或刪除卡的選項，具體取決於所選卡的屬性。

>[!NOTE]
>
>並非所有卡都可以編輯或刪除。 這是因為某些卡包含只讀或必需的資訊。 如果卡片右上角沒有橢圓，則它包含只讀AND所需資訊，無法編輯，也不能刪除。 如果某張卡在拐角處有省略號，並且選擇它只顯示了刪除該卡的選項，則該卡資訊是只讀的，無法編輯。

![將突出顯示編輯卡下拉清單。 這包括編輯或刪除卡的選項。](../images/profile-customization/edit-card.png)

選擇 **[!UICONTROL 編輯]** 中開啟 **[!UICONTROL 編輯小部件]** 工作區，您可以在其中更新卡標題、重新排序或刪除可見屬性，或使用 **[!UICONTROL 添加屬性]** 按鈕

![將顯示「基本屬性」卡。](../images/profile-customization/basic-attributes.png)

## 添加屬性 {#add-attributes}

從 **[!UICONTROL 編輯小部件]** 螢幕，選擇 **[!UICONTROL 添加屬性]** 在卡的右上角，開始向該卡添加屬性。

![「基本屬性」卡中的「添加屬性」按鈕將突出顯示。](../images/profile-customization/add-attributes.png)

當 **[!UICONTROL 選擇聯合架構欄位]** 對話框開啟，對話框的左側顯示 [!UICONTROL XDM個人配置檔案] 聯合架構，其下嵌套有欄位。 有關聯合架構的詳細資訊，請參閱 [聯合架構部分 [!DNL Profile] 使用手冊](user-guide.md#union-schema)。

的 **[!UICONTROL 所選屬性]** 對話框右側的部分顯示了當前包含在您正在編輯的卡中的屬性。 您也可以刪除屬性並重新排序。 顯示所選屬性的總數以及可添加到單個卡的最大屬性數(20)。

![當前構成卡上屬性的屬性會突出顯示。](../images/profile-customization/select-before.png)

您可以選擇任何可用的聯合架構欄位來自定義正在編輯的卡上的屬性。 選定欄位旁邊顯示複選標籤，並自動添加到選定屬性清單中。 添加了希望在卡上顯示的所有屬性後，選擇 **[!UICONTROL 選擇]** 返回 **[!UICONTROL 編輯小部件]** 的上界。

![新添加的屬性被加亮。](../images/profile-customization/select-after.png)

當您返回 **[!UICONTROL 編輯小部件]** 螢幕中，卡上的屬性清單應立即更新以反映您的選擇。 您仍然可以根據需要刪除或重新排序卡屬性或編輯卡標題。 編輯完成後，選擇 **[!UICONTROL 保存]** 的子菜單。

![新添加的屬性顯示在編輯的卡上。](../images/profile-customization/new-attributes.png)

保存後，您將返回 **[!UICONTROL 詳細資訊]** 的子菜單。

![新添加的屬性顯示在「配置檔案」操控板中的卡上。](../images/profile-customization/added-attributes.png)

## 添加新卡 {#add-a-new-card}

要進一步自定義Experience Platform中配置檔案的外觀，您可以選擇將新卡添加到儀表板並選擇要在這些卡上顯示的屬性。 要開始，請選擇 **[!UICONTROL 修改儀表板]** 的 **[!UICONTROL 詳細資訊]** 頁籤。

![「自定義配置檔案詳細資訊」按鈕將突出顯示。](../images/profile-customization/customize-profile-details.png)

下一步，選擇 **[!UICONTROL 添加小部件]** 的下界。

![「添加小部件」按鈕將突出顯示。](../images/profile-customization/add-widget.png)

選擇添加新卡將開啟 **[!UICONTROL 編輯小部件]** 螢幕，您可以在其中為新卡提供標題並選擇希望該卡顯示的屬性。 要開始向卡添加屬性，請選擇 **[!UICONTROL 添加屬性]**。

![「編輯小部件」螢幕中將顯示空白的新小部件卡。](../images/profile-customization/edit-widget.png)

當 **[!UICONTROL 選擇聯合架構欄位]** 對話框開啟，對話框的左側顯示 [!UICONTROL XDM個人配置檔案] 聯合架構和 **[!UICONTROL 所選屬性]** 對話框右側的部分顯示您為卡選擇的屬性。 有關添加屬性的詳細資訊，請參閱 [添加屬性一節](#add-attributes) 的子菜單。

顯示所選屬性的總數以及可添加到單個卡的最大屬性數(20)。 也可以從此螢幕中刪除和重新排序所選屬性。 添加了希望顯示在卡上的所有屬性後，選擇 **[!UICONTROL 選擇]** 返回 **[!UICONTROL 編輯小部件]** 的上界。

![您要添加到卡的欄位將突出顯示。](../images/profile-customization/add-widget-attributes.png)

當您返回 **[!UICONTROL 編輯小部件]** 螢幕中，卡上的屬性清單應反映您在上一螢幕中的選擇。 您還可以根據需要重新排序和刪除卡屬性。

要保存新卡，您必須首先提供 **[!UICONTROL 卡片標題]**，您將能夠選擇 **[!UICONTROL 保存]** 完成卡的建立過程。

![在「編輯小部件」螢幕中預覽新小部件。](../images/profile-customization/new-widget.png)

保存後，您將返回 **[!UICONTROL 詳細資訊]** 的子菜單。

![新小部件將添加到「配置檔案」儀表板。](../images/profile-customization/added-widget.png)

## 還原預設卡

如果您在任何時候都決定要恢復已刪除的預設卡，則您可以快速輕鬆地執行此操作。 首先，選擇 **[!UICONTROL 修改儀表板]**，然後選擇 **[!UICONTROL 還原預設卡]**。 當預設卡可見後，可以選擇 **[!UICONTROL 保存]** 保存更改或選擇 **[!UICONTROL 取消]** 的子菜單。

![「恢復預設卡」按鈕在「配置檔案」操控板中突出顯示。](../images/profile-customization/restore-default.png)

## 後續步驟

通過遵循本文檔，您現在應該能夠更新組織的配置檔案視圖，包括添加和刪除卡、編輯卡詳細資訊和屬性以及重新排序和調整卡大小。 瞭解有關使用的詳細資訊 [!DNL Profile] Experience PlatformUI中的資料，請參閱 [[!DNL Profile] 使用手冊](user-guide.md)。
