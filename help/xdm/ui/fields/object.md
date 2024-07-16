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

在Adobe Experience Platform使用者介面中定義[新欄位](./overview.md#define)時，請使用&#x200B;**[!UICONTROL Type]**&#x200B;下拉式清單，並從清單中選取[!UICONTROL 物件]。

![](../../images/ui/fields/special/object.png)

選取&#x200B;**[!UICONTROL 套用]**&#x200B;以將物件加入結構描述。 畫布更新以顯示套用[!UICONTROL 物件]資料型別的新欄位，包括編輯和新增子欄位到物件的控制項。

![](../../images/ui/fields/special/object-applied.png)

若要新增子欄位，請選取畫布中物件欄位旁的&#x200B;**加號(+)**&#x200B;圖示。 物件下方會顯示新欄位，其中含有在右側邊欄中設定子欄位的控制項。

![](../../images/ui/fields/special/object-add-field.png)

設定子欄位並選取&#x200B;**[!UICONTROL 套用]**&#x200B;後，您就可以繼續使用相同的程式將欄位新增至物件。 您也可以新增本身為物件的子欄位，讓您可以將欄位巢狀化得儘可能深。

完成物件的建構後，您可能會發現想要在不同類別和欄位群組中重複使用它的結構。 在此情況下，您可以選擇將物件轉換為資料型別。 如需詳細資訊，請參閱資料型別UI指南中[將物件轉換為資料型別](../resources/data-types.md#convert)的相關章節。

## 後續步驟

本指南說明如何在UI中定義物件欄位。 請參閱[在UI](./overview.md#special)中定義欄位的概觀，瞭解如何在[!DNL Schema Editor]中定義其他XDM欄位型別。
