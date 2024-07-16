---
title: Advertising詳細資料集合資料型別
description: 瞭解Advertising詳細資料收集Experience Data Model (XDM)資料型別。
exl-id: 3f6bf1f9-c728-46af-804a-cb41eb29951b
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 14%

---

# [!UICONTROL Advertising詳細資料]集合資料型別

[!UICONTROL Advertising詳細資料]集合是標準的體驗資料模型(XDM)資料型別，可擷取與廣告相關的關鍵屬性。 其中包括廣告ID、廣告商和促銷活動ID、長度、序列中的位置、有關轉譯廣告之播放器的詳細資訊等資訊。 您可以使用此資料型別來追蹤和分析廣告績效和參與度的各個層面，並提供受眾如何與不同廣告互動和回應的深入見解。 您提供的這項資訊會用於追蹤您的串流資料。

+++選取此項可顯示Advertising詳細資料收集資料型別的圖表。
![Advertising詳細資料集合資料型別的圖表。](../images/data-types/advertising-details-collection.png)
+++

>[!NOTE]
>
>每個顯示名稱都包含一個連結，可讓您進一步瞭解其音訊和視訊引數。 連結的頁面包含由Adobe、實作值、網路引數、報表和重要考量收集之視訊廣告資料的詳細資訊。

| 顯示名稱 | 屬性 | 資料類型 | 必要 | 說明 |
|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|-----------|----------------------------------------------------------------------------------------------------------------------------------|
| [[!UICONTROL 廣告商]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#advertiser) | `advertiser` | 字串 | 無 | 廣告中精選產品的公司或品牌。 |
| [[!UICONTROL 廣告行銷活動]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#campaign-id) | `campaignID` | 字串 | 無 | 廣告行銷活動的ID。 |
| [[!UICONTROL 廣告創意ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-id) | `creativeID` | 字串 | 無 | 廣告創意的 ID。 |
| [[!UICONTROL 廣告創意URL]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#creative-url) | `creativeURL` | 字串 | 無 | 廣告創意的 URL。 |
| Pod位置中的[[!UICONTROL 廣告（廣告開始）]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-start) | `podPosition` | 整數 | 是 | 父級廣告開始內的廣告索引，例如，第一個廣告索引為0，第二個廣告索引為1。 |
| [[!UICONTROL 廣告長度或持續時間]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-length) | `length` | 整數 | 是 | 視訊廣告的秒數長度。 |
| [[!UICONTROL 廣告名稱]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-name) | `friendlyName` | 字串 | 是 | 人類看得懂的廣告名稱。 在報表中，「廣告名稱」為分類，而「廣告名稱（變數）」為eVar。 |
| [[!UICONTROL 廣告位置ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#placement-id) | `placementID` | 字串 | 無 | 廣告版位ID。 |
| [[!UICONTROL 廣告播放器名稱]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#ad-player-name) | `playerName` | 字串 | 是 | 負責轉譯廣告的播放器名稱。 |
| [[!UICONTROL 廣告網站ID]](https://experienceleague.adobe.com/docs/media-analytics/using/implementation/variables/ad-parameters.html#site-id) | `siteID` | 字串 | 無 | 廣告網站ID。 |
