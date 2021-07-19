---
keywords: Experience Platform；首頁；熱門主題；資料擷取；擷取資料；串流；概觀；串流擷取；延遲；串流延遲；
solution: Experience Platform
title: 串流擷取概述
topic-legacy: overview
description: Adobe Experience Platform的串流內嵌功能可讓使用者透過用戶端和伺服器端裝置，即時傳送資料至Experience Platform。
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: 12c3f440319046491054b3ef3ec404798bb61f06
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 3%

---

# 串流獲取概觀

Adobe Experience Platform的串流內嵌為使用者提供了一種方法，可即時將資料從用戶端和伺服器端裝置傳送至[!DNL Experience Platform]。

## 您可以透過串流獲取做什麼？

Adobe Experience Platform可讓您為每個個別客戶產生[!DNL Real-time Customer Profile] ，借此促進協調、一致和相關的體驗。 串流內嵌可讓您將[!DNL Profile]資料盡可能少的延遲傳送至[!DNL Data Lake]，在建立這些設定檔時起到關鍵作用。

以下影片旨在協助您了解串流擷取，並概述上述概念。

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### 資料流配置檔案記錄和[!DNL ExperienceEvents]

透過串流內嵌，使用者可以在數秒內將設定檔記錄和[!DNL ExperienceEvents]串流至[!DNL Platform]，以協助推動即時個人化。 所有傳送至串流獲取API的資料都會自動保存在[!DNL Data Lake]中。

請閱讀[建立串流連接指南](../tutorials/create-streaming-connection.md)以了解詳細資訊。

### 串流至資料集

確信資料已清除後，您就可以為[!DNL Real-time Customer Profile]和[!DNL Identity Service]啟用資料集。

有關為[!DNL Profile]和[!DNL Identity Service]啟用資料集的詳細資訊，請參閱[配置資料集指南](../../profile/tutorials/dataset-configuration.md)。

## [!DNL Platform]上串流擷取的預期延遲為何？

| 目的地 | 預期延遲 |
| --------- | ---------------- |
| 即時客戶個人檔案 | &lt; 1=&quot;&quot; minute=&quot;&quot;> |
| 資料湖 | &lt; 60 分鐘 |

## Adobe Experience Platform 擴充功能

您可以使用Adobe Experience Platform擴充功能建立新的串流連線。 [!DNL Experience Platform]擴充功能提供可傳送[!DNL Experience Data Model](XDM)格式化信標以即時擷取至[!DNL Experience Platform]的動作。 如需詳細資訊，請參閱[Experience Platform擴充功能](../../tags/extensions/web/sdk/overview.md)檔案。
