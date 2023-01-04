---
keywords: Experience Platform；首頁；熱門主題；ui;XDM; XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；結構註冊表；結構；結構；結構；結構；結構；建立；資料類型；
solution: Experience Platform
title: 使用UI建立和編輯資料類型
topic-legacy: tutorial
type: Tutorial
description: 了解如何在Experience Platform使用者介面中建立和編輯資料類型。
exl-id: 2c917154-c425-463c-b8c8-04ba37d9247b
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 0%

---

# 使用UI建立和編輯資料類型

在Experience Data Model(XDM)中，資料類型是可重複使用的欄位，包含多個子欄位。 雖然與中的架構欄位組類似，它們允許一致地使用多欄位結構，但資料類型更靈活，因為它們可以包含在架構結構中的任何位置，而欄位組只能在根級別添加。

Adobe Experience Platform提供許多標準資料類型，可用來涵蓋多種常見的體驗管理使用案例。 不過，您也可以定義自己的自訂資料類型，以符合您的獨特業務需求。

本教學課程涵蓋在Platform使用者介面中建立和編輯自訂資料類型的步驟。

## 先決條件

本指南需要妥善了解XDM系統。 請參閱 [XDM概觀](../../home.md) 了解XDM在Experience Platform生態系統中的角色，以及 [綱要構成基本知識](../../schema/composition.md) 了解資料類型對XDM結構的貢獻。

雖然本指南並非必要項目，但建議您也參照 [在UI中合成架構](../../tutorials/create-schema-ui.md) 熟悉 [!DNL Schema Editor].

## 開啟 [!DNL Schema Editor] 資料類型

在平台UI中，選取 **[!UICONTROL 結構]** 在左側導覽中，開啟 [!UICONTROL 結構] 工作區，然後選取 **[!UICONTROL 資料類型]** 標籤。 隨即顯示可用資料類型的清單，包括由Adobe定義的資料類型和由您的組織建立的資料類型。

![](../../images/ui/resources/data-types/data-types-tab.png)

從這裡，您有兩個選項：

- [建立新資料類型](#create)
- [選擇要編輯的現有資料類型](#edit)

### 建立新資料類型 {#create}

從 **[!UICONTROL 資料類型]** 索引標籤，選取 **[!UICONTROL 建立資料類型]**.

![](../../images/ui/resources/data-types/create.png)

此 [!DNL Schema Editor] ，顯示畫布中新資料類型的當前結構。 在編輯器的右側，您可以提供資料類型的顯示名稱和可選說明。 請確定您為資料類型提供唯一且簡潔的名稱，在將其新增至架構時，將如何加以識別。

本教學課程會建立描述餐廳屬性的資料類型，因此資料類型的顯示名稱為「Restaurant」。

![](../../images/ui/resources/data-types/data-type-properties.png)

從這裡，您可以跳到 [下一節](#add-fields) 開始向新資料類型添加欄位。

### 編輯現有資料類型

>[!NOTE]
>
>一旦現有資料類型用於已啟用在即時客戶設定檔中使用的結構中，之後就只能對該資料類型進行非破壞性的變更。 請參閱 [模式演化規則](../../schema/composition.md#evolution) 以取得更多資訊。

只能編輯您的組織定義的自訂資料類型。 若要縮小顯示的清單，請選取篩選圖示(![篩選圖示](../../images/ui/resources/data-types/filter.png))以顯示依據 [!UICONTROL 擁有者]. 選擇 **[!UICONTROL 客戶]** 僅顯示貴組織擁有的自訂資料類型。

從清單中選取您要編輯的資料類型，以開啟右側邊欄，顯示資料類型的詳細資訊。 在右側邊欄中選取資料類型的名稱，以在 [!DNL Schema Editor].

![](../../images/ui/resources/data-types/edit.png)

## 將欄位新增至資料類型 {#add-fields}

若要開始將欄位新增至資料類型，請選取 **加號(+)** 表徵圖。 下方會顯示新欄位，右側邊欄會更新為顯示新欄位的控制項。

![](../../images/ui/resources/data-types/new-field.png)

使用右側邊欄中的控制項，設定新欄位的詳細資訊。 請參閱 [定義UI中的欄位](../fields/overview.md#define) 以取得如何設定欄位並將欄位新增至資料類型的特定步驟。

餐廳資料類型需要字串欄位來表示餐廳的名稱。 因此， [!UICONTROL 欄位名稱] 設為&quot;name&quot;，而 [!UICONTROL 類型] 設為&quot;[!UICONTROL 字串]」。 選擇 **[!UICONTROL 套用]** 將更改應用到欄位。

![](../../images/ui/resources/data-types/name-field.png)

視需要繼續新增更多欄位至資料類型。 範例「餐廳」資料類型現在包含品牌、座位容量和地板空間的其他欄位。

![](../../images/ui/resources/data-types/more-fields.png)

除了基本欄位，您也可以在自訂資料類型中巢狀內嵌其他資料類型。 例如，Restaurant資料類型需要一個表示屬性物理地址的欄位。 在此案例中，您可以新增指派標準資料類型「 」的新「位址」欄位[!UICONTROL 郵遞區號]」。

![](../../images/ui/resources/data-types/address-field.png)

這說明在描述資料時，資料類型的彈性如何：資料類型可採用也是資料類型的欄位，這些欄位本身可包含更多資料類型，以此類推。 這可讓您在整個XDM結構中抽象和重複使用通用資料模式，更輕鬆地呈現複雜的資料結構。

將欄位添加到資料類型後，請選擇 **[!UICONTROL 儲存]** 儲存變更並將資料類型新增至 [!DNL Schema Library].

## 將資料類型添加到類或欄位組

建立資料類型後，您就可以開始在結構中使用它。 由於XDM結構由類別和零個或多個欄位群組組成，因此資料類型提供的欄位無法直接新增至結構。 而是必須包含在類別或欄位群組中。

首先，請遵循 [向類添加欄位](./classes.md#add-fields) 或 [將欄位新增至欄位群組](./field-groups.md#add-fields). 當您選擇 **[!UICONTROL 類型]** 對於新欄位，從下拉式選單中選取資料類型的名稱。

## 將多欄位物件轉換為資料類型 {#convert}

在 [!DNL Schema Editor]，您可以將該欄位轉換為資料類型，以便在不同類別或欄位群組中使用相同的欄位結構。

若要將物件類型欄位轉換為資料類型，請選取畫布中的欄位。 轉換欄位之前，請確定 **[!UICONTROL 顯示名稱]** 是物件將包含之資料的描述性，因為這會成為資料類型的名稱。 準備好轉換欄位時，請選取 **[!UICONTROL 轉換為新資料類型]** 在右側邊欄。

![](../../images/ui/resources/data-types/convert-object.png)

畫布會從「[!UICONTROL 物件]」新資料類型。 子欄位旁也有小型鎖定圖示，表示它們不再是個別欄位，而是多欄位資料類型的一部分。 現在，通過從 **[!UICONTROL 類型]** 定義新欄位時的下拉式清單。

![](../../images/ui/resources/data-types/converted.png)

## 後續步驟

本指南說明如何使用Platform UI建立和編輯資料類型。 如需功能的詳細資訊，請參閱 [!UICONTROL 結構] 工作區，請參閱 [[!UICONTROL 結構] 工作區概述](../overview.md).

了解如何使用 [!DNL Schema Registry] API，請參閱 [data types端點指南](../../api/data-types.md).
