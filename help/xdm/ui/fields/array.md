---
keywords: Experience Platform；首頁；熱門主題；API;API;XDM;XDM系統；體驗資料模型；資料模型；ui；工作區；陣列；欄位；
solution: Experience Platform
title: 在UI中定義陣列欄位
description: 了解如何在Experience Platform使用者介面中定義陣列欄位。
topic-legacy: user guide
exl-id: 9ac55554-c29b-40b2-9987-c8c17cc2c00c
source-git-commit: 39d04cf482e862569277211d465bb2060a49224a
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 2%

---

# 在UI中定義陣列欄位

在Adobe Experience Platform使用者介面中定義Experience Data Model(XDM)欄位時，您可以將該欄位指定為陣列。

陣列的內容取決於為該欄位選擇的[!UICONTROL 類型]。 例如，如果欄位的[!UICONTROL Type]設定為&quot;[!UICONTROL String]&quot;，將該欄位設定為陣列將將該欄位指定為字串的陣列。 如果欄位的[!UICONTROL Type]設定為多欄位資料類型，如&quot;[!UICONTROL 郵遞區號]&quot;，則它將成為符合資料類型的郵遞區號物件陣列。

在UI](./overview.md#define)中定義了新欄位後，您可以在右側邊欄中選取&#x200B;**[!UICONTROL Array]**&#x200B;核取方塊，將其設為陣列欄位。[

![](../../images/ui/fields/special/array.png)

選取核取方塊後，右側邊欄中會顯示其他控制項，供您選擇進一步限制陣列。 如果您不想強制執行特定限制，請將欄位留空。

陣列的其他配置控制如下：

| 欄位屬性 | 說明 |
| --- | --- |
| [!UICONTROL 最小長度] | 陣列必須包含的最小項目數，才能成功擷取。 |
| [!UICONTROL 長度上限] | 陣列必須包含的項目數上限，才能成功擷取。 |
| [!UICONTROL 僅限不重複項目] | 如果設為「[!UICONTROL True]」，陣列中的每個項目必須是唯一的，才能成功擷取。 |

{style=&quot;table-layout:auto&quot;}

完成欄位配置後，選擇&#x200B;**[!UICONTROL Apply]**&#x200B;將更改應用到架構。

![](../../images/ui/fields/special/array-config.png)

畫布會更新以反映對欄位所做的變更。 請注意，畫布中欄位名稱旁顯示的資料類型會附加一對方括弧(`[]`)，表示該欄位代表該資料類型的陣列。

![](../../images/ui/fields/special/array-applied.png)

## 後續步驟

本指南說明如何在UI中定義陣列欄位。 請參閱[定義UI](./overview.md#special)中欄位的概觀，了解如何定義[!DNL Schema Editor]中的其他XDM欄位類型。
