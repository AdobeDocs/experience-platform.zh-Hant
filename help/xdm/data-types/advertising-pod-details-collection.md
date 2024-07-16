---
title: Advertising Pod詳細資料集合資料型別
description: 瞭解Advertising Pod詳細資料收集Experience Data Model (XDM)資料型別。
exl-id: 401c393f-aeda-4ecd-89f4-458833190ced
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 8%

---

# [!UICONTROL Advertising Pod詳細資料]集合資料型別

[!UICONTROL Advertising Pod詳細資料]集合是標準的體驗資料模型(XDM)資料型別。 它會定義內容插播期間通常會連續播放的廣告順序或廣告群組。 使用[!UICONTROL Advertising Pod詳細資料]集合資料型別來擷取詳細資料，例如廣告插播ID、廣告插播的易記名稱、插播內廣告的索引，以及內容時間軸內廣告插播的位移（以秒為單位）。

![Advertising Pod詳細資訊集合資料型別的圖表。](../images/data-types/advertising-pod-details-collection.png)

| 顯示名稱 | 屬性 | 資料類型 | 必要 | 說明 |
|-----------------------------------------|-----------------|-----------|--------------------------------------------------------------------|
| Pod位置中的[!UICONTROL 廣告] | `index` | 整數 | 是 | 上層廣告插播開始內的廣告索引。 |
| [!UICONTROL Pod易記名稱] | `friendlyName` | 字串 | 無 | 容易理解的廣告插播名稱。 |
| [!UICONTROL Pod位移] | `offset` | 整數 | 是 | 內容內的廣告插播位移（以秒為單位）。 |
