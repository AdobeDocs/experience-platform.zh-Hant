---
keywords: Experience Platform; home；熱門主題；邊緣分割；分段服務；分段服務；ui指南；流媒體邊緣；
solution: Experience Platform
title: 邊緣區段UI指南
topic-legacy: ui guide
description: 邊緣區段是指能夠即時在邊緣上評估平台中的區段，讓相同的頁面和下一頁個人化使用案例。
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 4%

---

# 邊緣區段UI指南（測試版）

>[!NOTE]
>
>邊緣區段目前為測試版。 文件和功能可能會有所變更。

邊緣區段是指能夠即時評估Adobe Experience Platform邊緣區段的能力，讓相同的頁面和下一頁個人化使用案例。

## 邊緣分割查詢類型

如果查詢符合下列任何條件，則可使用邊緣分段來評估該查詢：

| 查詢類型 | 詳細資料 | 範例 |
| ---------- | ------- | ------- |
| 傳入點擊 | 任何區段定義，是指沒有時間限制的單一傳入事件。 | ![](../images/ui/edge-segmentation/incoming-hit.png) |
| 參照描述檔的傳入點擊 | 任何區段定義，是指單一傳入事件（無時間限制）以及一或多個描述檔屬性。 | ![](../images/ui/edge-segmentation/profile-hit.png) |
| 頻率查詢 | 任何區段定義，指發生至少特定次數之事件。 |  |
| 參照描述檔的頻率查詢 | 任何區段定義，是指發生至少特定次數且具有一或多個描述檔屬性的事件。 |  |

如果查詢與上述任何查詢類型相符，您可以通過開啟&#x200B;**[!UICONTROL Evaluate as streaming segment on the edge]**&#x200B;切換來啟用該查詢以進行邊緣分割。

![](../images/ui/edge-segmentation/mark-on-edge.png)

下列查詢類型目前支援&#x200B;**not**&#x200B;進行邊緣分段：

| 查詢類型 | 詳細資料 |
| ---------- | ------- |
| 相對時間窗口 | 如果查詢引用時間窗口，則無法使用邊緣分割來評估該查詢。 |
| 否定 | 如果查詢包含否定，則無法使用邊緣分段來評估。 |
| 多個事件 | 如果查詢包含多個事件，則無法使用邊緣分段來評估。 |

## 後續步驟

本使用指南說明如何在Adobe Experience Platform使用邊緣區段來評估區段。

若要進一步瞭解使用Adobe Experience Platform使用者介面，請閱讀[區段使用指南](./overview.md)。 若要瞭解如何使用Adobe Experience Platform使用者介面執行類似動作及使用區段，請造訪[edge分段API指南](../api/edge-segmentation.md)。
