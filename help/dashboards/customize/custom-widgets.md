---
keywords: Experience Platform；使用者介面；UI；控制面板；控制面板；設定檔；區段；目的地；授權使用；Widget；量度；
title: 建立控制面板的自訂Widget
description: 本指南提供建立自訂Widget以用於Adobe Experience Platform控制面板的逐步指示。
exl-id: 0168ab1e-0b7d-4faf-852e-7208a2b09a04
source-git-commit: 386d805eadf335b95b6eac92c7663fcee17b4b2d
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 0%

---

# 建立控制面板的自訂小工具

在Adobe Experience Platform中，您可以使用多個控制面板來檢視及與組織的資料互動。 您也可以將新介面工具集新增到控制面板檢視，以更新特定控制面板。 除了由Adobe提供的標準Widget外，您還可以建立自訂Widget並在整個組織中共用它們。

本指南提供建立自訂Widget和將自訂Widget新增至 [!UICONTROL 設定檔], [!UICONTROL 區段]，和 [!UICONTROL 目的地] 平台UI中的控制面板。

若要進一步了解標準介面工具集，請參閱指南 [將標準介面工具集新增至控制面板](standard-widgets.md).

>[!NOTE]
>
>顯示於 [!UICONTROL 授權使用] 無法自訂控制面板。 若要深入了解此不重複控制面板，請閱讀 [授權使用控制面板檔案](../guides/license-usage.md).

## 介面工具集程式庫 {#widget-library}

本指南需要存取 [!UICONTROL 介面工具集程式庫] Experience Platform。 若要進一步了解Widget程式庫，以及如何在UI中存取，請先閱讀 [介面工具集程式庫概述](widget-library.md).

## 自訂Widget快速入門

在介面工具集程式庫內， **[!UICONTROL 自訂]** 索引標籤可讓您建立介面工具集並與組織中的其他使用者共用，以自訂控制面板的外觀。

>[!IMPORTANT]
>
>您的組織最多可在介面工具集資料庫中建立20個自訂介面工具集。

選取 **[!UICONTROL 自訂]** 頁簽，開始建立自定義小工具或查看貴組織已建立的自定義小工具。

![介面工具集庫工作區，「自訂」標籤會反白顯示。](../images/customization/custom-widgets.png)

## 建立自訂介面工具集

若要建立自訂介面工具集，請選取 **[!UICONTROL 建立介面工具集]** 從介面工具集庫的右上角，或如果這是貴組織的第一個自訂介面工具集，請選取 **[!UICONTROL 建立]** 從widget資料庫的中央。

![強調顯示「建立」的介面工具集庫工作區的「自訂」標籤。](../images/customization/create-widget.png)

在 **[!UICONTROL 建立介面工具集]** 對話框，請為新介面工具集提供標題和說明，並選擇要介面工具集顯示的屬性。

>[!NOTE]
>
>可用屬性的清單取決於為貴組織設定的結構。 若要進一步了解屬性選取和結構設定，請參閱 [編輯架構以建立自訂小工具](edit-schema.md).

要選擇屬性，請選擇要添加的屬性旁邊的單選按鈕。

>[!NOTE]
>
>每個Widget只能選擇一個屬性，每個屬性只能建立一個Widget。 如果已為屬性建立了介面工具集，則屬性會顯示為灰色。

![建立介面工具集對話方塊。](../images/customization/create-widget-dialog.png)

## 選取視覺效果

選取屬性後，新介面工具集的預覽會顯示在對話方塊中。 人工智慧可用來自動選取最適合屬性資料的視覺效果，以及提供其他可手動選取的視覺效果選項。

根據屬性，AI建議不同的視覺效果選項。 視覺效果的完整清單包括：

* 橫條圖：水準線用於表示值。
* 垂直條圖：垂直線用於表示值。
* 環圈圖：與圓形圖類似，值以整體的部分或部分顯示。
* 散點圖：使用水準和垂直軸來指示值。
* 折線圖：值會使用單一行來顯示一段時間內的變更。
* 號碼卡：顯示表示單鍵值的摘要數字。
* 資料表：值在表格中顯示為行。

>[!NOTE]
>
>目前所有屬性唯一支援的量度是設定檔計數。
>
>範例介面工具集中顯示的資料僅供說明之用。 預覽不會顯示貴組織的實際資料。

若要儲存新介面工具集並返回 [!UICONTROL 自訂] 索引標籤，選取 **[!UICONTROL 建立]**.

![建立介面工具集對話方塊，其中包含視覺效果選項，並反白顯示「建立」。](../images/customization/create-widget-select-attribute.png)

您的新介面工具集現在可從程式庫選擇介面工具集，然後選取 **[!UICONTROL 新增介面工具集]**.

![介面工具集庫工作區的「自訂」標籤會顯示新介面工具集，並反白顯示「新增介面工具集」。](../images/customization/custom-widgets-new.png)

## 隱藏自訂介面工具集

將介面工具集新增至程式庫後，可透過選取點(`...`)，然後選取 **[!UICONTROL 隱藏Widget]**. 您也可以從相同的下拉式清單預覽及編輯介面工具集。

要查看已隱藏的小部件，請選擇 **[!UICONTROL 顯示隱藏的小部件]** 從widget資料庫的右上角。

>[!WARNING]
>
>在資料庫中隱藏介面工具集並不會從個別使用者的控制面板中移除介面工具集。 如果貴組織中不應再使用介面工具集，請務必將此介面工具集直接傳送給所有Platform使用者，因為他們需要從控制面板中移除介面工具集。

![介面工具集庫工作區的「自訂」標籤，包含介面工具集下拉式功能表選項，並反白顯示隱藏介面工具集。](../images/customization/hide-widget.png)

## 編輯自訂介面工具集

您可以選取點(`...`)，然後選取 **[!UICONTROL 編輯]** 從下拉式功能表。

![以點和「編輯」反白顯示Widget下拉式選單選項。](../images/customization/custom-widget-edit.png)

在 **[!UICONTROL 編輯介面工具集]** 對話方塊中，您可以編輯介面工具集的標題和說明，以及預覽和選取不同的視覺效果。 完成編輯後，請選取 **[!UICONTROL 儲存]** 以保存更改並返回到「自定義小工具」頁簽。

>[!WARNING]
>
>在資料庫中編輯介面工具集時不會更新個別使用者的介面工具集。 如果Widget已更新，請務必直接向所有Platform使用者傳達此資訊，因為他們需要從控制面板中移除過時的Widget，然後從Widget資料庫中選取並新增更新的Widget。

![「編輯介面工具集」對話框。](../images/customization/edit-widget.png)

## 後續步驟

閱讀本檔案後，您可以存取介面工具集程式庫，並使用它來建立和新增貴組織的自訂介面工具集。 要修改儀表板中顯示的小部件的大小和位置，請參閱 [修改控制面板指南](modify.md).
