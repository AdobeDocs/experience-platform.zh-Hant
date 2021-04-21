---
keywords: Experience Platform;home；熱門主題；api;API;XDM;XDM系統；體驗資料模型；ui;workspace;object;field;
solution: Experience Platform
title: 在UI中定義物件欄位
description: 瞭解如何在Experience Platform用戶介面中定義對象類型欄位。
topic-legacy: user guide
exl-id: 5b7b3cf0-7f11-4e15-af87-09127f4423a5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# 在UI中定義物件欄位

Adobe Experience Platform可讓您完全自訂自訂體驗資料模型(XDM)類別、混合和資料類型的結構。 為了在自訂XDM資源中組織和巢狀內嵌相關欄位，您可以定義物件類型欄位，其中可包含其他子欄位。

當[在Adobe Experience Platform用戶介面中定義新欄位](./overview.md#define)時，使用&#x200B;**[!UICONTROL Type]**&#x200B;下拉式清單並從清單中選擇&quot;[!UICONTROL Object]&quot;。

![](../../images/ui/fields/special/object.png)

選擇&#x200B;**[!UICONTROL Apply]**&#x200B;將對象添加到方案。 畫布會更新，顯示已套用[!UICONTROL Object]資料類型的新欄位，包括編輯和新增子欄位至物件的控制項。

![](../../images/ui/fields/special/object-applied.png)

若要新增子欄位，請選取畫布中物件欄位旁的&#x200B;**加號(+)**&#x200B;圖示。 物件下方會出現新欄位，並提供在右側欄位中設定子欄位的控制項。

![](../../images/ui/fields/special/object-add-field.png)

在配置子欄位並選擇&#x200B;**[!UICONTROL Apply]**&#x200B;後，可以繼續使用相同的進程向對象添加欄位。 您也可以新增子欄位，這些子欄位本身就是物件，讓您可以視需要將欄位巢狀內嵌。

![](../../images/ui/fields/special/object-nested.png)

在完成物件建構後，您可能會發現想要在不同的類別和混合中重複使用其結構。 在這種情況下，您可以選擇將對象轉換為資料類型。 如需詳細資訊，請參閱資料類型UI指南中有關將物件轉換為資料類型](../resources/data-types.md#convert)的章節。[

## 後續步驟

本指南說明如何在UI中定義物件欄位。 請參閱[定義UI](./overview.md#special)中欄位的概觀，瞭解如何定義[!DNL Schema Editor]中的其他XDM欄位類型。
