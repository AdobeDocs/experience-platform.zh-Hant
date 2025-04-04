---
keywords: Experience Platform；使用者介面；UI；控制面板；控制面板；設定檔；區段；目的地；授權使用情況；Widget；量度；
title: 建立儀表板的自訂Widget
description: 本指南提供建立用於Adobe Experience Platform控制面板的自訂Widget的逐步指示。
exl-id: 0168ab1e-0b7d-4faf-852e-7208a2b09a04
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '979'
ht-degree: 0%

---

# 建立儀表板的自訂Widget

在Adobe Experience Platform中，您可以使用多個儀表板檢視組織的資料並與之互動。 您也可以將新的Widget新增至儀表板檢視，以更新某些儀表板。 除了Adobe提供的標準Widget之外，您也可以建立自訂Widget，並在整個組織內共用。

本指南提供在Experience Platform UI中建立自訂Widget並新增至[!UICONTROL 設定檔]、[!UICONTROL 區段]和[!UICONTROL 目的地]儀表板的逐步指示。

>[!NOTE]
>
>控制面板的任何更新都是根據組織和沙箱進行。

若要進一步瞭解標準Widget，請參閱[將標準Widget新增至儀表板](standard-widgets.md)的指南。

## 介面工具資料庫 {#widget-library}

本指南需要存取Experience Platform中的[!UICONTROL Widget資料庫]。 若要進一步瞭解Widget程式庫，以及如何在UI中存取它，請先閱讀[Widget程式庫概觀](widget-library.md)。

## 自訂Widget快速入門

在Widget資料庫中，**[!UICONTROL 自訂]**&#x200B;標籤可讓您建立Widget並與您組織中的其他使用者共用，以自訂儀表板的外觀。

>[!IMPORTANT]
>
>貴組織可在Widget資料庫中建立最多20個自訂Widget。

選取&#x200B;**[!UICONTROL 自訂]**&#x200B;標籤，開始建立自訂Widget或檢視貴組織已建立的自訂Widget。

![反白顯示[自訂]索引標籤的Widget程式庫工作區。](../images/customization/custom-widgets.png)

## 建立自訂Widget

若要建立自訂Widget，請從Widget資料庫右上角選取「**[!UICONTROL 建立Widget]**」；或者，如果這是您組織的第一個自訂Widget，請從Widget資料庫中央選取「**[!UICONTROL 建立]**」。

![反白顯示[建立]之Widget程式庫工作區的[自訂]索引標籤。](../images/customization/create-widget.png)

在&#x200B;**[!UICONTROL 建立Widget]**&#x200B;對話方塊中，提供新Widget的標題和說明，並選擇您要讓Widget顯示的屬性。

>[!NOTE]
>
>可用屬性的清單取決於已為您的組織設定的結構。 若要深入瞭解屬性選取和結構描述設定，請閱讀[編輯結構描述以建立自訂Widget](edit-schema.md)的指南。

若要選擇屬性，請選取要新增的屬性旁的單選按鈕。

>[!NOTE]
>
>每個Widget只能選取一個屬性，且每個屬性只能建立一個Widget。 如果已為屬性建立Widget，則屬性會顯示為灰色。

![建立Widget對話方塊。](../images/customization/create-widget-dialog.png)

## 選取視覺效果

選取屬性後，新介面工具集的預覽會顯示在對話方塊中。 人工智慧用於自動選取最適合屬性資料的視覺效果，並提供您手動選取的其他視覺效果選項。

根據屬性，AI會建議不同的視覺效果選項。 完整的視覺效果清單包括：

* 水準長條圖：水平線用來表示值。
* 垂直長條圖：垂直線用來表示值。
* 環形圖：與圓形圖類似，值是以整體的部分或片段顯示。
* 散點圖：使用水平軸和垂直軸來指示值。
* 折線圖：數值是使用單一折線圖來顯示，以顯示一段期間的變更。
* 數字卡：顯示摘要數字，代表單一金鑰值。
* 資料表格：值會以表格中的列顯示。

>[!NOTE]
>
>目前所有屬性唯一支援的量度是設定檔計數。
>
>範例Widget中顯示的資料僅供說明用途。 預覽不會顯示貴組織的實際資料。

若要儲存新的Widget並返回[!UICONTROL 自訂]標籤，請選取&#x200B;**[!UICONTROL 建立]**。

![包含視覺效果選項和「建立」的建立Widget對話方塊反白顯示。](../images/customization/create-widget-select-attribute.png)

您的新介面工具集現在可從資料庫中選擇介面工具集，並選取&#x200B;**[!UICONTROL 新增Widget]**，以新增至儀表板。

![反白顯示具有新Widget和新增Widget的Widget程式庫工作區的「自訂」標籤。](../images/customization/custom-widgets-new.png)

## 隱藏自訂Widget

將Widget新增至程式庫後，可以選取Widget卡上的省略符號(`...`)，然後選取&#x200B;**[!UICONTROL 隱藏Widget]**&#x200B;來隱藏它。 您也可以從相同的下拉式清單預覽和編輯Widget。

若要檢視已隱藏的Widget，請從Widget程式庫的右上角選取&#x200B;**[!UICONTROL 顯示隱藏的Widget]**。

>[!WARNING]
>
>在程式庫中隱藏Widget並不會從個別使用者的控制面板中移除該Widget。 如果您的組織不應再使用Widget，請務必直接將此資訊傳達給所有Experience Platform使用者，因為他們需要將該Widget從儀表板上移除。

![Widget資料庫工作區的「自訂」索引標籤，其中包含Widget下拉式功能表選項和「顯示隱藏的Widget」反白顯示。](../images/customization/hide-widget.png)

## 編輯自訂Widget

您可以選取Widget卡片上的省略符號(`...`)，然後從下拉式選單中選取&#x200B;**[!UICONTROL 編輯]**，在Widget資料庫中編輯自訂Widget。

![以橢圓和「編輯」反白顯示的Widget下拉式功能表選項。](../images/customization/custom-widget-edit.png)

在&#x200B;**[!UICONTROL 編輯Widget]**&#x200B;對話方塊中，您可以編輯該Widget的標題和說明，以及預覽和選取不同的視覺效果。 完成編輯後，選取&#x200B;**[!UICONTROL 儲存]**&#x200B;以儲存變更並返回自訂Widget標籤。

>[!WARNING]
>
>編輯資料庫中的Widget不會更新個別使用者的小工具。 如果Widget已更新，請務必將此資訊直接傳達給所有Experience Platform使用者，因為他們需要從儀表板上移除過時的Widget，然後從Widget資料庫中選取並新增更新後的Widget。

![編輯Widget對話方塊。](../images/customization/edit-widget.png)

## 後續步驟

閱讀本檔案後，您就能存取Widget程式庫，並使用它為您的組織建立和新增自訂Widget。 若要修改顯示在儀表板中的介面工具的大小和位置，請參閱[修改儀表板指南](modify.md)。
