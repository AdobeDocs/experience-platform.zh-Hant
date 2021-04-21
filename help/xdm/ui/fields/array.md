---
keywords: Experience Platform;home；熱門主題；api;API;XDM;XDM系統；體驗資料模型；ui;workspace;array;field;
solution: Experience Platform
title: 在UI中定義陣列欄位
description: 瞭解如何在Experience Platform用戶介面中定義陣列欄位。
topic-legacy: user guide
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 0%

---

# 在UI中定義陣列欄位

在Adobe Experience Platform用戶介面中定義「體驗資料模型」(XDM)欄位時，您可以將該欄位指定為陣列。

陣列的內容取決於為該欄位選擇的[!UICONTROL Type]。 例如，如果欄位的[!UICONTROL Type]設定為&quot;[!UICONTROL String]&quot;，將該欄位設定為陣列將將該欄位指定為字串陣列。 如果欄位的[!UICONTROL Type]設為多欄位資料類型，例如&quot;[!UICONTROL Postal address]&quot;，則會變成符合資料類型的郵遞區址物件陣列。

在UI](./overview.md#define)中定義了新欄位後，可以通過選擇右側導軌中的&#x200B;**[!UICONTROL Array]**&#x200B;複選框將其設定為陣列欄位。[

![](../../images/ui/fields/special/array.png)

勾選核取方塊後，其他控制項會顯示在右側邊欄中，讓您可選擇進一步限制陣列。 如果不想強制實施特定約束，請將欄位留空。

陣列的其他配置控制如下：

| 欄位屬性 | 說明 |
| --- | --- |
| [!UICONTROL Minimum length] | 陣列必須包含的最小項目數，以便成功接收。 |
| [!UICONTROL Maximum length] | 陣列必須包含的項目數上限，以便接收成功。 |
| [!UICONTROL Unique items only] | 如果設定為&quot;[!UICONTROL True]&quot;，則陣列中的每個項目必須是唯一的，以便成功接收。 |

完成欄位配置後，選擇&#x200B;**[!UICONTROL Apply]**&#x200B;將更改應用到模式。

![](../../images/ui/fields/special/array-config.png)

畫布會更新，以反映對欄位所做的變更。 請注意，畫布中欄位名稱旁顯示的資料類型會附加一對方括弧(`[]`)，表示欄位代表該資料類型的陣列。

![](../../images/ui/fields/special/array-applied.png)

## 後續步驟

本指南說明如何在UI中定義陣列欄位。 請參閱[定義UI](./overview.md#special)中欄位的概觀，瞭解如何定義[!DNL Schema Editor]中的其他XDM欄位類型。
