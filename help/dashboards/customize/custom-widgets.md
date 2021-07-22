---
keywords: Experience Platform；使用者介面；UI；控制面板；控制面板；設定檔；區段；目的地；授權使用；Widget；量度；
title: 建立控制面板的自訂Widget
description: '本指南提供建立自訂Widget以用於Adobe Experience Platform控制面板的逐步指示。 '
exl-id: 1d33e3ea-a8a8-4a09-8bd9-2e04ecedebdc
source-git-commit: a07eb2baec48ad514ff0afc0548f53baf34da561
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---


# 建立控制面板的自訂小工具

在Adobe Experience Platform中，您可以使用多個控制面板來檢視及與組織的資料互動。 您也可以將新介面工具集新增到控制面板檢視，以更新特定控制面板。 除了由Adobe提供的標準Widget外，您還可以建立自訂Widget並在整個組織中共用它們。

本指南提供逐步指示，說明如何在Platform UI中建立自訂Widget，並將其新增至[!UICONTROL Profiles]、[!UICONTROL Segments]和[!UICONTROL Destinations]控制面板。

若要進一步了解標準介面工具集，請參閱[將標準介面工具集新增至控制面板](standard-widgets.md)的指南。

>[!NOTE]
>
>無法自訂[!UICONTROL 授權使用]控制面板中顯示的介面工具集。 若要深入了解此唯一控制面板，請參閱[授權使用控制面板檔案](../guides/license-usage.md)。

## 介面工具集程式庫 {#widget-library}

本指南需要存取Experience Platform內的[!UICONTROL Widget程式庫]。 若要進一步了解Widget程式庫，以及如何在UI中存取，請先閱讀[Widget程式庫概述](widget-library.md)開始。

## 自訂Widget快速入門

在介面工具集程式庫中， **[!UICONTROL Custom]**&#x200B;標籤可讓您建立介面工具集，並與組織中的其他使用者共用介面工具集，以便自訂控制面板的外觀。

>[!IMPORTANT]
>
>您的組織最多可在介面工具集資料庫中建立20個自訂介面工具集。

選擇&#x200B;**[!UICONTROL Custom]**&#x200B;頁簽以開始建立自定義小部件或查看貴組織已建立的自定義小部件。

![](../images/customization/custom-widgets.png)

## 建立自訂介面工具集

若要建立自訂介面工具集，請從介面工具集庫的中心選擇「**[!UICONTROL 建立]**」，或如果已建立自訂介面工具集，請從介面工具集庫的右上角選擇「**[!UICONTROL 建立介面工具集]**」。

![](../images/customization/create-widget.png)

在&#x200B;**[!UICONTROL 建立Widget]**&#x200B;對話方塊中，您可以提供新Widget的標題和說明，並選擇要顯示該Widget的屬性。

>[!NOTE]
>
>可用屬性的清單取決於為貴組織設定的結構。 要了解有關屬性選擇和架構配置的詳細資訊，請閱讀[編輯架構以建立自定義小部件](edit-schema.md)的指南。

要選擇屬性，請選擇要添加的屬性旁邊的單選按鈕。

>[!NOTE]
>
>每個Widget只能選擇一個屬性，每個屬性只能建立一個Widget。 如果已為屬性建立了介面工具集，則屬性會顯示為灰色。

![](../images/customization/create-widget-dialog.png)

## 預覽自訂介面工具集

對話方塊中會顯示新介面工具集的預覽，其中會顯示包含模擬資料的水準長條圖。

>[!NOTE]
>
>目前所有屬性唯一支援的量度是設定檔計數，而自訂Widget目前唯一支援的視覺效果是水準長條圖。
>
>範例介面工具集中顯示的資料僅供說明之用。 預覽不會顯示貴組織的實際資料。

![](../images/customization/create-widget-select-attribute.png)

若要儲存新介面工具集並返回[!UICONTROL Custom]標籤，請選取&#x200B;**[!UICONTROL Create]**。 您的新介面工具集現在可從資料庫選擇介面工具集，然後選取&#x200B;**[!UICONTROL 「新增介面工具集」]**，即可新增至控制面板。

## 封存自訂Widget

將介面工具集新增至程式庫後，可使用&#x200B;**[!UICONTROL Archive]**&#x200B;按鈕進行封存。 您也可以編輯介面工具集以更新標題或說明欄位。

## 後續步驟

閱讀本檔案後，您可以存取介面工具集程式庫，並使用它來建立和新增貴組織的自訂介面工具集。 要修改儀表板中顯示的小部件的大小和位置，請參閱[modify儀表板指南](modify.md)。
