---
keywords: Experience Platform;home；熱門主題；api;API;XDM;XDM系統；體驗資料模型；ui;workspace;enum;field;
solution: Experience Platform
title: 在UI中定義列舉欄位
description: 瞭解如何在Experience Platform使用者介面中定義列舉欄位。
topic-legacy: user guide
exl-id: 67ec5382-31de-4f8d-9618-e8919bb5a472
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# 在UI中定義列舉欄位

在體驗資料模型(XDM)中，列舉欄位代表欄位，其受限於預先定義的可接受值清單。

當[在Adobe Experience Platform用戶介面中定義新欄位](./overview.md#define)時，可以通過選擇右邊欄中的&#x200B;**[!UICONTROL Enum]**&#x200B;複選框將其設定為枚舉欄位。

![](../../images/ui/fields/special/enum.png)

選取核取方塊後，會出現其他控制項，讓您指定列舉的值限制。 在&#x200B;**[!UICONTROL Value]**&#x200B;欄下，您必須提供要限制欄位的精確值。 此值必須符合您為枚舉欄位選擇的[!UICONTROL Type]。 您也可以選擇為約束提供人性友好的&#x200B;**[!UICONTROL Label]**。

要向枚舉添加其他約束，請選擇&#x200B;**[!UICONTROL Add row]**。

![](../../images/ui/fields/special/enum-add-row.png)

繼續將所要的限制和選用標籤新增至列舉。 完成後，選擇&#x200B;**[!UICONTROL Apply]**&#x200B;將更改應用到模式。

![](../../images/ui/fields/special/enum-configured.png)

畫布會更新以反映變更。 當您將來探索此架構時，可以檢視並編輯右邊欄中列舉欄位的限制。

![](../../images/ui/fields/special/enum-applied.png)

## 後續步驟

本指南涵蓋如何在UI中定義列舉欄位。 請參閱[定義UI](./overview.md#special)中欄位的概觀，瞭解如何定義[!DNL Schema Editor]中的其他XDM欄位類型。
