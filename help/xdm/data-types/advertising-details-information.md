---
title: 廣告詳細資訊資料型別
description: 瞭解廣告詳細資訊體驗資料模型(XDM)資料型別。
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '342'
ht-degree: 11%

---

# [!UICONTROL 廣告詳細資訊] 資料型別

[!UICONTROL 廣告詳細資訊] 是標準的體驗資料模型(XDM)資料型別，可擷取與廣告相關的關鍵屬性。 其中包括廣告ID、廣告商和促銷活動ID、長度、序列中的位置、有關轉譯廣告之播放器的詳細資訊等資訊。 您可以使用此資料型別來追蹤和分析廣告績效和參與度的各個層面，並提供受眾如何與不同廣告互動和回應的深入見解。

+++選取此項可顯示「廣告詳細資訊」資料型別的圖表。
![廣告詳細資訊資料型別的圖表。](../images/data-types/advertising-details-information.png)
+++

| 顯示名稱 | 屬性 | 資料類型 | 說明 |
|----------------------------|-----------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL 廣告名稱] | `friendlyName` | 字串 | **必填** 人類看得懂的廣告名稱。 在報表中，「廣告名稱」為分類，而「廣告名稱 (變數)」為 eVar。 |
| [!UICONTROL 廣告ID] | `name` | 字串 | 廣告ID。 任何整數和/或字母的組合。 |
| [!UICONTROL 廣告長度或持續時間] | `length` | 整數 | **必填** 視訊廣告的秒數長度。 |
| [!UICONTROL Pod位置中的廣告（廣告開始）] | `podPosition` | 整數 | **必填** 父級廣告開始內的廣告索引，例如，第一個廣告索引為0，第二個廣告索引為1。 |
| [!UICONTROL 廣告播放器名稱] | `playerName` | 字串 | **必填** 負責轉譯廣告之播放器的名稱。 |
| [!UICONTROL 廣告商] | `advertiser` | 字串 | 廣告中精選產品的公司或品牌。 |
| [!UICONTROL 廣告行銷活動] | `campaignID` | 字串 | 廣告行銷活動的ID。 |
| [!UICONTROL 廣告創意ID] | `creativeID` | 字串 | 廣告創意的ID。 |
| [!UICONTROL 廣告網站ID] | `siteID` | 字串 | 廣告網站ID。 |
| [!UICONTROL 廣告創意URL] | `creativeURL` | 字串 | 廣告創意的URL。 |
| [!UICONTROL 廣告刊登ID] | `placementID` | 字串 | 廣告版位ID。 |
| [!UICONTROL 廣告完成] | `isCompleted` | 布林值 | 追蹤廣告是否已完成。 |
| [!UICONTROL 廣告開始] | `isStarted` | 布林值 | 追蹤廣告是否已開始。 |
| [!UICONTROL 廣告播放時間] | `timePlayed` | 整數 | 觀看廣告花費的總秒數（即播放的總秒數）。 |

{style="table-layout:auto"}

如需欄位群組的詳細資訊，請參閱 [公用XDM存放庫](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingdetails.schema.json)
