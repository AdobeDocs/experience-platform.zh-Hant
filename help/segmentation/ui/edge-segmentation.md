---
keywords: Experience Platform；首頁；熱門主題；邊緣分段；分段服務；分段服務；ui指南；串流邊緣；
solution: Experience Platform
title: Edge Segmentation UI指南
topic-legacy: ui guide
description: 邊緣分段是即時在邊緣上評估Platform中區段的功能，可啟用相同的頁面和下一頁個人化使用案例。
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: c1dc75d94774eff8ad9a7374b1fa158f737dd5a4
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 3%

---

# Edge劃分UI指南（測試版）

>[!NOTE]
>
>邊緣區段目前仍在測試階段。 文件和功能可能會有所變更。

邊緣分段是在Edge](../../edge/home.md)上即時評估Adobe Experience Platform中區段的功能，可啟用相同的頁面和下一頁個人化使用案例。[

## 邊緣分段查詢類型

如果查詢符合下列任何條件，則可使用邊緣分段來評估該查詢：

| 查詢類型 | 詳細資訊 | 範例 |
| ---------- | ------- | ------- |
| 傳入點擊 | 任何區段定義，是指沒有時間限制的單一傳入事件。 | ![](../images/ui/edge-segmentation/incoming-hit.png) |
| 參照設定檔的傳入點擊 | 任何區段定義，是指沒有時間限制的單一傳入事件，以及一或多個設定檔屬性。 | ![](../images/ui/edge-segmentation/profile-hit.png) |
| 時間窗口為24小時的傳入點擊 | 任何在24小時內參照單一傳入事件的區段定義 |  |
| 傳入點擊是指時間窗為24小時的設定檔 | 任何區段定義，是指24小時內單一傳入事件，以及一或多個設定檔屬性 |  |

如果查詢符合上述任何查詢類型，系統就會使用邊緣分段自動評估查詢。

下列查詢類型目前支援邊緣分段&#x200B;**not**:

| 查詢類型 | 詳細資訊 |
| ---------- | ------- |
| 多個事件 | 如果查詢包含多個事件，則無法使用邊緣分段來評估。 |
| 頻率查詢 | 任何區段定義，是指至少發生特定次數之事件。 |  |
| 參考設定檔的頻率查詢 | 任何區段定義，是指發生至少特定次數的事件，且具有一或多個設定檔屬性。 |  |

## 後續步驟

本使用手冊說明如何在Adobe Experience Platform上透過邊緣細分評估區段。

若要進一步了解如何使用Adobe Experience Platform使用者介面，請參閱[分段使用手冊](./overview.md)。 若要了解如何使用Adobe Experience Platform使用者介面執行類似動作及使用區段，請造訪[邊緣區段API指南](../api/edge-segmentation.md)。
