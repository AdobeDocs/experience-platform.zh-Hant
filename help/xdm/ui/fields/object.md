---
keywords: Experience Platform；首頁；熱門主題；API;API;XDM;XDM系統；體驗資料模型；資料模型；ui；工作區；物件；欄位；
solution: Experience Platform
title: 在UI中定義物件欄位
description: 了解如何在Experience Platform使用者介面中定義物件類型欄位。
exl-id: 5b7b3cf0-7f11-4e15-af87-09127f4423a5
source-git-commit: 5caa4c750c9f786626f44c3578272671d85b8425
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# 在UI中定義物件欄位

Adobe Experience Platform可讓您完全自訂自訂Experience Data Model(XDM)類別、結構欄位群組和資料類型的結構。 若要在自訂XDM資源中組織與巢狀內嵌相關欄位，您可以定義物件類型欄位，其中可包含其他子欄位。

當 [定義新欄位](./overview.md#define) 在Adobe Experience Platform使用者介面中，使用 **[!UICONTROL 類型]** 下拉式清單，選取「[!UICONTROL 物件]」。

![](../../images/ui/fields/special/object.png)

選擇 **[!UICONTROL 套用]** 將對象添加到架構中。 畫布會更新，以使用 [!UICONTROL 物件] 套用的資料類型，包括編輯子欄位和新增子欄位至物件的控制項。

![](../../images/ui/fields/special/object-applied.png)

若要新增子欄位，請選取 **加號(+)** 表徵圖。 物件下方會顯示新欄位，並提供右側邊欄中設定子欄位的控制項。

![](../../images/ui/fields/special/object-add-field.png)

設定子欄位並選取後 **[!UICONTROL 套用]**，您可以繼續使用相同程式將欄位新增至物件。 您也可以新增屬於物件本身的子欄位，讓您盡可能深地巢狀內嵌欄位。

完成對象的構建後，您可能會發現要在不同的類和欄位組中重複使用其結構。 在此情況下，您可以選擇將對象轉換為資料類型。 請參閱 [將對象轉換為資料類型](../resources/data-types.md#convert) （位於資料類型UI指南中）以取得詳細資訊。

## 後續步驟

本指南說明如何在UI中定義物件欄位。 請參閱 [定義UI中的欄位](./overview.md#special) 若要了解如何定義 [!DNL Schema Editor].
