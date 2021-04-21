---
keywords: Experience Platform；首頁；熱門主題；資料攝取；收錄資料；流；概述；串流攝取；延遲；串流延遲；
solution: Experience Platform
title: 串流擷取概觀
topic-legacy: overview
description: Adobe Experience Platform的串流擷取為使用者提供一種方法，可即時從用戶端和伺服器端裝置傳送資料至Experience Platform。
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 3%

---

# 串流擷取概觀

Adobe Experience Platform的串流擷取為使用者提供一種方法，可即時從用戶端和伺服器端裝置傳送資料至[!DNL Experience Platform]。

## 您可以使用串流擷取功能做什麼？

Adobe Experience Platform可讓您為每位客戶產生[!DNL Real-time Customer Profile]，以推動協調、一致且相關的體驗。 串流擷取功能可讓您盡可能少的延遲，將[!DNL Profile]資料傳送至[!DNL Data Lake]，在建立這些描述檔時起到關鍵作用。

以下視訊旨在協助您瞭解串流擷取，並概述上述概念。

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### 串流描述檔記錄和[!DNL ExperienceEvents]

透過串流擷取，使用者可在數秒內將描述檔記錄和[!DNL ExperienceEvents]串流至[!DNL Platform]，以協助推動即時個人化。 傳送至串流擷取API的所有資料都會自動保留在[!DNL Data Lake]中。

請閱讀[建立串流連線指南](../tutorials/create-streaming-connection.md)以取得詳細資訊。

### 串流至資料集

一旦您確信資料是乾淨的，就可以為[!DNL Real-time Customer Profile]和[!DNL Identity Service]啟用資料集。

有關為[!DNL Profile]和[!DNL Identity Service]啟用資料集的詳細資訊，請閱讀[配置資料集指南](../../profile/tutorials/dataset-configuration.md)。

## [!DNL Platform]上串流擷取的預期延遲為何？

| 目的地 | 預期延遲 |
| --------- | ---------------- |
| 即時客戶個人檔案 | &lt; 1=&quot;&quot; minute=&quot;&quot;> |
| Data Lake | &lt; 60 分鐘 |

## Adobe Experience Platform 擴充功能

您可以使用Adobe Experience Platform擴充功能建立新的串流連線。 [!DNL Experience Platform]擴充功能提供動作，可傳送以[!DNL Experience Data Model](XDM)格式的信標，以便即時擷取至[!DNL Experience Platform]。 請造訪[Experience Platform擴充功能](https://experienceleague.adobe.com/docs/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html)檔案，以取得詳細資訊。
