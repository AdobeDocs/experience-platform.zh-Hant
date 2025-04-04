---
title: Advertising Pod詳細資料報表資料型別
description: 瞭解Advertising Pod詳細資料報告Experience Data Model (XDM)資料型別。
exl-id: 5164520f-8c48-4eb0-a0b0-66dc10b68356
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 5%

---

# [!UICONTROL Advertising Pod詳細資料報告]資料型別

[!UICONTROL Advertising Pod詳細資料報告]是標準的體驗資料模型(XDM)資料型別。 它會定義內容插播期間通常會連續播放的廣告順序或廣告群組。 使用[!UICONTROL Advertising Pod詳細資料報表]資料型別來擷取詳細資訊，例如，廣告插播ID、廣告插播的易記名稱、插播內廣告的索引，以及內容時間軸內廣告插播的位移（以秒為單位）。

![Advertising Pod詳細資料報告資料型別的圖表。](../images/data-types/advertising-pod-details-information.png)

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|----------------------------|------------------------|-----------|-------------------------------------------------------|
| [!UICONTROL 廣告插播ID] | `ID` | 字串 | 廣告插播的ID。 |
| [!UICONTROL Pod易記名稱] | `friendlyName` | 字串 | 容易理解的廣告插播名稱。 |
| Pod位置中的[!UICONTROL 廣告] | `index` | 整數 | 上層廣告插播開始內的廣告索引。 |
| [!UICONTROL Pod位移] | `offset` | 整數 | **必要**&#x200B;內容內的廣告插播位移（以秒為單位）。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱[公用XDM存放庫](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json)
