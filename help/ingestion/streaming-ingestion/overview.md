---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform串流擷取概觀
topic: overview
translation-type: tm+mt
source-git-commit: 3f1c3c77a0755a3e305da0fb8a234be0f0ee1863
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 3%

---


# 串流擷取概觀

Adobe Experience Platform的串流擷取為使用者提供一種方法，可即時從用戶端和伺服器端裝置傳送資料至Experience Platform。

## 您可以使用串流擷取功能做什麼？

Adobe Experience Platform可讓您針對個別客戶建立即時客戶個人檔案，以推動協調、一致且相關的體驗。 串流擷取在建立這些描述檔時扮演了關鍵角色，讓您盡可能少的延遲將描述檔資料傳送至資料湖。

以下視訊旨在協助您瞭解串流擷取，並概述上述概念。

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### 串流描述檔記錄和ExperienceEvents

透過串流擷取，使用者只需數秒即可將描述檔記錄和ExperienceEvents串流至Platform，以協助推動即時個人化。 傳送至串流擷取API的所有資料都會自動保留在資料湖中。

請閱讀建立 [串流連線指南](../tutorials/create-streaming-connection.md) ，以取得詳細資訊。

### 串流至資料集

一旦您確信您的資料是乾淨的，您就可以啟用資料集以用於即時客戶個人檔案和身分服務。

如需啟用描述檔與身分服務資料集的詳細資訊，請閱讀設定 [資料集指南](../../profile/tutorials/dataset-configuration.md)。

## 平台上串流擷取的預期延遲為何？

| 目的地 | 預期延遲 |
| --------- | ---------------- |
| 即時客戶個人檔案 | &lt; 1分鐘 |
| Data Lake | &lt; 60 分鐘 |

## Adobe Experience Platform 擴充功能

您可以使用Adobe Experience Platform擴充功能建立新的串流連線。 Experience Platform擴充功能可提供動作，以傳送Experience Data Model(XDM)格式的信標，以便即時擷取至Experience Platform。 請造訪 [Experience Platform Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) 檔案，以取得詳細資訊。