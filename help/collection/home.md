---
solution: Experience Platform
title: 資料彙集概觀
description: 瞭解如何將資料傳送至Adobe Experience Platform。
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 3d51f01d314587510d900d335dc92fedb8ac31e8
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 2%

---

# 資料彙集概觀

Adobe Experience Platform提供了一套技術，可讓您從各種來源收集客戶體驗資料，並將其傳送到Adobe Experience Platform Edge Network。 然後，這些資料就可以擴充、轉換並分發到Adobe或非Adobe目的地。

Adobe透過資料收集的專用程式庫支援下列程式碼語言：

* **JavaScript**：適用於網站與網頁型應用程式
* **Kotlin**：適用於Android裝置
* **Swift**：適用於iOS裝置
* **Brightscript**：適用於Roku裝置
* **顫動**：適用於使用Flutter的Android + iOS應用程式
* **React Native**：適用於使用React Native的Android + iOS應用程式

Adobe Experience Platform資料彙集中的標籤UI包含Web SDK和Mobile SDK擴充功能。

如果上述SDK皆未因應您專案的需求，您可以使用[Adobe Experience Platform Edge Network API](https://developer.adobe.com/data-collection-apis/docs/)，直接將資料傳送至Adobe。

## 資料收集程式

您可以實作上述其中一個SDK或標籤擴充功能，將所有所需資料彙總至單一裝載，而不需為每個Adobe產品安裝和實作個別的程式庫。 該裝載會傳送至Adobe Experience Platform Edge Network中的[資料串流](/help/datastreams/overview.md)。

![資料彙集圖表](assets/tags-sdks.png)

Adobe Experience Platform Edge Network是遍佈全球、快速且可靠的伺服器網路，能以驚人的規模接收及處理資料。 當資料流收到資料時，會將該資料分發到您已設定的每個解決方案。 資料會以每個個別產品可瞭解的格式傳遞。

![Adobe解決方案圖表](assets/adobe-solutions.png)

您也可以使用[事件轉送](/help/tags/ui/event-forwarding/overview.md)來轉換、擴充資料，以及以低延遲將資料傳送至任何非Adobe目的地，而不需要任何使用者端實作程式碼。

![事件轉送圖表](assets/event-forwarding.png)
