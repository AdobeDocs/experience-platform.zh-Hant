---
keywords: Experience Platform；主題；熱門主題；ui;XDM;XDM;XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；資料模型；架構註冊；架構註冊；架構；架構；架構；架構；建立；資料類型；
solution: Experience Platform
title: 使用UI建立和編輯資料類型
type: Tutorial
description: 瞭解如何在Experience Platform用戶介面中建立和編輯資料類型。
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '1156'
ht-degree: 0%

---

# 使用UI建立和編輯資料類型

在體驗資料模型(XDM)中，資料類型是包含多個子欄位的可重用欄位。 雖然與允許一致使用多欄位結構的模式欄位組類似，但資料類型更靈活，因為它們可以包含在模式結構中的任何位置，而欄位組只能在根級別添加。

Adobe Experience Platform提供許多標準資料類型，可用於涵蓋各種常見的經驗管理使用案例。 但是，您也可以定義自己的自定義資料類型以滿足您獨特的業務需求。

本教程介紹在平台用戶介面中建立和編輯自定義資料類型的步驟。

## 先決條件

本指南要求對XDM系統有正確的瞭解。 請參閱 [XDM概述](../../home.md) 介紹XDM在Experience Platform生態系統中的作用， [架構組合基礎](../../schema/composition.md) 資料類型如何貢獻XDM架構。

雖然本指南不是必需的，但建議您也學習上的教程 [在UI中合成架構](../../tutorials/create-schema-ui.md) 熟悉 [!DNL Schema Editor]。

## 開啟 [!DNL Schema Editor] 資料類型

在平台UI中，選擇 **[!UICONTROL 架構]** 的下界 [!UICONTROL 架構] 工作區，然後選擇 **[!UICONTROL 資料類型]** 頁籤。 將顯示可用資料類型的清單，包括由Adobe定義的資料類型和由您的組織建立的資料類型。

![](../../images/ui/resources/data-types/data-types-tab.png)

從這裡，您有兩個選擇：

- [建立新資料類型](#create)
- [選擇要編輯的現有資料類型](#edit)

### 建立新資料類型 {#create}

從 **[!UICONTROL 資料類型]** 頁籤 **[!UICONTROL 建立資料類型]**。

![](../../images/ui/resources/data-types/create.png)

的 [!DNL Schema Editor] 顯示畫布中新資料類型的當前結構。 在編輯器的右側，可以為資料類型提供顯示名稱和可選說明。 確保為資料類型提供唯一且簡潔的名稱，因為在將其添加到架構時，將如此標識它。

本教程建立描述restaurant屬性的資料類型，因此資料類型的顯示名稱為「Restaurant」。

![](../../images/ui/resources/data-types/data-type-properties.png)

從這裡，您可以跳到 [下一部分](#add-fields) 開始向新資料類型添加欄位。

### 編輯現有資料類型

>[!NOTE]
>
>一旦現有資料類型在已啟用用於即時客戶配置檔案的方案中使用，則以後只能對該資料類型進行非破壞性更改。 查看 [模式演化規則](../../schema/composition.md#evolution) 的子菜單。

只能編輯由您的組織定義的自定義資料類型。 要縮小顯示清單的範圍，請選擇篩選器表徵圖(![篩選器表徵圖](../../images/ui/resources/data-types/filter.png))根據 [!UICONTROL 所有者]。 選擇 **[!UICONTROL 客戶]** 只顯示您的組織擁有的自定義資料類型。

從清單中選擇要編輯的資料類型以開啟右滑軌，並顯示資料類型的詳細資訊。 選擇右滑軌中資料類型的名稱，以在 [!DNL Schema Editor]。

![](../../images/ui/resources/data-types/edit.png)

## 將欄位添加到資料類型 {#add-fields}

要開始向資料類型添加欄位，請選擇 **加(+)** 表徵圖。 下面將顯示一個新欄位，右滑軌將更新以顯示新欄位的控制項。

![](../../images/ui/resources/data-types/new-field.png)

使用右滑軌中的控制項配置新欄位的詳細資訊。 請參閱上的指南 [定義UI中的欄位](../fields/overview.md#define) 有關如何配置欄位並將其添加到資料類型的特定步驟。

Restaurant資料類型需要一個字串欄位來表示餐廳的名稱。 因此， [!UICONTROL 欄位名] 設定為&quot;name&quot;, [!UICONTROL 類型] 設定為&quot;[!UICONTROL 字串]。 選擇 **[!UICONTROL 應用]** 按鈕。

![](../../images/ui/resources/data-types/name-field.png)

根據需要繼續向資料類型添加更多欄位。 Restaurant資料類型示例現在包含品牌、座位容量和佔地面積的附加欄位。

![](../../images/ui/resources/data-types/more-fields.png)

除基本欄位外，您還可以在自定義資料類型中嵌套其他資料類型。 例如，Restaurant資料類型需要一個表示該屬性物理地址的欄位。 在此方案中，可以添加新的「地址」欄位，該欄位已分配標準資料類型「」[!UICONTROL 郵政地址]。

![](../../images/ui/resources/data-types/address-field.png)

這演示了在描述資料時，可以如何靈活地使用資料類型：資料類型可以使用欄位，這些欄位也是資料類型，它們本身可以包含更多資料類型等。 這樣，您就可以在整個XDM架構中抽象和重用通用資料模式，從而更容易地表示複雜的資料結構。

將欄位添加到資料類型後，選擇 **[!UICONTROL 保存]** 保存更改並將資料類型添加到 [!DNL Schema Library]。

## 將資料類型添加到架構

建立資料類型後，可以開始在架構中使用它。 由於XDM架構由類和零個或多個欄位組組成，因此不能將資料類型提供的欄位直接添加到架構中。 相反，它們必須包含在類或欄位組中。

開始執行與 [將欄位添加到類](./classes.md#add-fields) 或 [將欄位添加到欄位組](./field-groups.md#add-fields)。 或者，您可以 [將欄位直接添加到模式](./schemas.md#add-individual-fields) 並從中選擇父類或欄位組。 選擇 **[!UICONTROL 類型]** 對於新欄位，從下拉菜單中選擇資料類型的名稱。

## 將多欄位對象轉換為資料類型 {#convert}

建立對象類型欄位時，在 [!DNL Schema Editor]，可以將該欄位轉換為資料類型，以便可以在其他類或欄位組中使用相同的欄位結構。

要將對象類型欄位轉換為資料類型，請在畫布中選擇該欄位。 在轉換欄位之前，請確保 **[!UICONTROL 顯示名稱]** 描述對象將包含的資料，因為這將成為資料類型的名稱。 準備轉換欄位時，選擇 **[!UICONTROL 轉換為新資料類型]** 右欄。

![](../../images/ui/resources/data-types/convert-object.png)

畫布從「」更新欄位的資料類型[!UICONTROL 對象]」到新資料類型。 現在，通過從 **[!UICONTROL 類型]** 下拉清單。

![](../../images/ui/resources/data-types/converted.png)

## 後續步驟

本指南介紹如何使用平台UI建立和編輯資料類型。 有關功能的詳細資訊 [!UICONTROL 架構] 工作區，請參閱 [[!UICONTROL 架構] 工作區概述](../overview.md)。

瞭解如何使用 [!DNL Schema Registry] API，請參見 [資料類型終結點指南](../../api/data-types.md)。
