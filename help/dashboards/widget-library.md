---
keywords: Experience Platform；用戶介面；UI；儀表板；概要檔案；段；目標；許可證使用
title: 使用介面工具集程式庫來新增和建立控制面板介面工具集
description: '本指南提供逐步指示，說明如何新增標準Widget以及建立自訂Widget，以視覺化Adobe Experience Platform的控制面板資料。 '
topic-legacy: guide
exl-id: 1d33e3ea-a8a8-4a09-8bd9-2e04ecedebdc
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 1%

---

# （測試版）Widget程式庫{#widget-library}

>[!IMPORTANT]
>
>儀表板功能目前處於測試階段，並非所有使用者都能使用。 文件和功能可能會有所變更。

在Adobe Experience Platform的使用者介面中，您可以使用多個儀表板來檢視組織的資料並與之互動。 您也可以新增Widget至控制面板檢視，以更新其中一些控制面板。 除了Adobe提供的標準Widget外，您還可以建立自訂Widget，並在整個組織內共用這些Widget。

本指南提供新增標準介面工具集和建立自訂介面工具集的逐步指示，以自訂平台UI中[!UICONTROL Profiles]和[!UICONTROL Segments]控制面板中顯示的資訊。

有關如何修改[!UICONTROL Profiles]、[!UICONTROL Destinations]和[!UICONTROL Segments]控制面板中Widget的位置和大小的資訊，請參閱[修改控制面板指南](modify.md)。

>[!NOTE]
>
>無法自訂[!UICONTROL License usage]控制面板中顯示的Widget。 若要進一步瞭解此唯一的控制面板，請閱讀[授權使用控制面板檔案](guides/license-usage.md)。

## 存取介面工具集程式庫

從任何控制面板（例如，「描述檔」控制面板）中，您可以選取&#x200B;**[!UICONTROL Modify dashboard]**&#x200B;後接&#x200B;**[!UICONTROL Widget library]**，以存取介面工具集程式庫。

>[!NOTE]
>
>[!UICONTROL Widget library]按鈕只會在選取[!UICONTROL Modify dashboard]後顯示。

![](images/customization/modify-dashboard.png)

![](images/customization/widget-library-button.png)

[!UICONTROL Widget library]包含兩個標籤， [!UICONTROL Standard]和[!UICONTROL Custom]。

* **[!UICONTROL Standard]**&#x200B;標籤包含由Adobe建立的介面工具集，可讓您使用這些標準度量來更新控制面板。 若要進一步瞭解如何新增標準介面工具集至控制面板，請參閱本指南的[標準介面工具集](#standard-widgets)一節。
* **[!UICONTROL Custom]**&#x200B;標籤可讓您在組織內建立和共用Widget。 有關建立自己的Widget的完整步驟，請參閱本指南中的[自定義Widget](#custom-widgets)部分。

![](images/customization/widget-library.png)

## 標準Widget {#standard-widgets}

**[!UICONTROL Standard]**&#x200B;標籤包含由Adobe建立的Widget，分為類別。 選取類別會顯示該控制面板的可用介面工具集。 每個介面工具集都會以卡片的形式顯示，提供度量的標題、說明和範例視覺化。

>[!NOTE]
>
>Widget只能新增至符合所選類別的控制面板。 例如，[!UICONTROL Profiles]類別中的Widget只能新增至[!UICONTROL Profiles]控制面板。

![](images/customization/standard-widgets.png)

若要選擇要新增至控制面板的標準介面工具集，請反白標示介面工具集並選取該介面工具集的核取方塊。 在至少選取一個Widget時，**[!UICONTROL Add widget]**&#x200B;按鈕會亮起。

>[!NOTE]
>
>介面工具集程式庫右上角的計數器會顯示選取的介面工具集總數。

選取&#x200B;**[!UICONTROL Add widget]**，將選取的介面工具集新增至控制面板。

![](images/customization/add-widget.png)

## 自訂介面工具集{#custom-widgets}

>[!IMPORTANT]
>
>您的組織在介面工具集程式庫中最多可建立20個自訂介面工具集。

若要進一步自訂Experience Platform中控制面板的外觀，您可以建立Widget並與組織中的其他使用者共用。 從介面工具集庫中，選擇&#x200B;**[!UICONTROL Custom]**&#x200B;標籤以開始建立自訂介面工具集。 在[!UICONTROL Custom]標籤中，您的組織所建立的所有Widget都會顯示。 在此範例中，尚未建立自訂Widget。

![](images/customization/custom-widgets.png)

### 選擇屬性

為了建立自訂Widget，必須識別即時客戶描述檔屬性，以確保資料會納入每日快照的一部分。 如果您的組織未選擇任何配置檔案屬性，則[!UICONTROL Configure schema]按鈕會顯示在Widget庫的右上角。

當至少已選取一個自訂屬性時，[!UICONTROL Edit schema]按鈕會顯示在介面工具集資料庫的右上角。 選擇&#x200B;**[!UICONTROL Edit schema]**&#x200B;以開啟&#x200B;**[!UICONTROL Select union schema field]**&#x200B;對話框，查看所選屬性並添加更多屬性。

>[!IMPORTANT]
>
>組織最多可以選擇20個屬性。

![](images/customization/edit-schema.png)

要選擇屬性，請導航到聯合方案中的屬性（或使用搜索），然後選擇屬性旁的複選框。 選中該複選框也會將屬性添加到對話框右側的&#x200B;**[!UICONTROL Selected Attributes]**&#x200B;清單中。

>[!NOTE]
>
>要使屬性在選擇中可見，它必須是以下屬性之一：字串、日期、日期——時間、布林值、短、長、整數或位元組。 地圖和雙重資料類型不受支援，且呈灰色顯示，因此無法選取它們。

選擇要添加的屬性後，選擇&#x200B;**[!UICONTROL Save]**&#x200B;以保存屬性並返回自定義Widget頁籤。

重新整理資料時，新選取的屬性會在每日快照之後使用。

![](images/customization/select-attribute.png)

### 建立自訂介面工具集

若要建立自訂介面工具集，請從介面工具集庫的中央選取&#x200B;**[!UICONTROL Create]**，或如果已建立自訂介面工具集，請從介面工具集庫的右上角選取&#x200B;**[!UICONTROL Create widget]**。

![](images/customization/create-widget.png)

在&#x200B;**[!UICONTROL Create widget]**&#x200B;對話方塊中，您可以提供新介面工具集的標題和說明，並選擇您要顯示介面工具集的屬性。 要選擇屬性，請選擇要添加的屬性旁邊的單選按鈕。

>[!NOTE]
>
>每個Widget只能選取一個屬性。 此外，如果已為屬性建立介面工具集，則屬性會顯示為灰色。

![](images/customization/create-widget-dialog.png)

新介面工具集的預覽會顯示在對話方塊中，顯示含模擬資料的水準長條圖。

>[!NOTE]
>
>目前所有屬性唯一支援的量度是描述檔計數，而自訂Widget目前唯一支援的視覺化是水準橫條圖。
>
>範例介面工具集中顯示的資料僅供圖解之用。 預覽不會顯示您組織的實際資料。

![](images/customization/create-widget-select-attribute.png)

要保存新介面工具集並返回[!UICONTROL Custom]頁籤，請選擇&#x200B;**[!UICONTROL Create]**。 您的新介面工具集現在可以從程式庫中選擇介面工具集，然後選取&#x200B;**[!UICONTROL Add widget]**，以新增至控制面板。

### 封存自訂Widget

將介面工具集新增至程式庫後，就可使用&#x200B;**[!UICONTROL Archive]**&#x200B;按鈕加以封存。 您也可以編輯介面工具集以更新標題或說明欄位。

## 後續步驟

閱讀本檔案後，您現在可以存取[!UICONTROL Widget library]，並使用它將Widget新增至控制面板，或為組織建立自訂Widget。 要修改儀表板中Widget的大小和位置，請參閱[修改儀表板指南](modify.md)。
