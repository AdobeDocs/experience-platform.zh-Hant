---
keywords: Experience Platform；首頁；熱門主題；API；API；XDM；XDM系統；體驗資料模型；資料模型；ui；工作區；物件；欄位；
solution: Experience Platform
title: 在UI中定義物件欄位
description: 瞭解如何在Experience Platform使用者介面中定義物件型別欄位。
exl-id: 5b7b3cf0-7f11-4e15-af87-09127f4423a5
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# 在UI中定義物件欄位

Adobe Experience Platform可讓您完全自訂自訂Experience Data Model (XDM)類別、結構描述欄位群組和資料型別的結構。 為了在自訂XDM資源中組織和巢狀相關欄位，您可以定義可包含其他子欄位的物件型別欄位。

時間 [定義新欄位](./overview.md#define) 在Adobe Experience Platform使用者介面中，使用 **[!UICONTROL 型別]** 下拉式清單並選取「[!UICONTROL 物件]」從清單中。

![](../../images/ui/fields/special/object.png)

選取 **[!UICONTROL 套用]** 將物件新增至結構描述。 畫布會更新，以顯示含有的新欄位 [!UICONTROL 物件] 套用的資料型別，包括編輯和新增子欄位到物件的控制項。

![](../../images/ui/fields/special/object-applied.png)

若要新增子欄位，請選取 **加(+)** 圖示加以存取（位於畫布中的物件欄位旁）。 物件下方會顯示新欄位，其中含有在右側邊欄中設定子欄位的控制項。

![](../../images/ui/fields/special/object-add-field.png)

設定子欄位並選取後 **[!UICONTROL 套用]**，您可使用相同的程式繼續將欄位新增至物件。 您也可以新增本身為物件的子欄位，讓您可以將欄位巢狀化得儘可能深。

完成物件的建構後，您可能會發現想要在不同類別和欄位群組中重複使用它的結構。 在此情況下，您可以選擇將物件轉換為資料型別。 請參閱以下小節： [將物件轉換為資料型別](../resources/data-types.md#convert) 詳細資訊，請參閱資料型別UI指南。

## 後續步驟

本指南說明如何在UI中定義物件欄位。 請參閱以下主題的概觀： [在UI中定義欄位](./overview.md#special) 瞭解如何在中定義其他XDM欄位型別 [!DNL Schema Editor].
