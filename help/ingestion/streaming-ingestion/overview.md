---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform串流擷取概觀
topic: overview
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '249'
ht-degree: 3%

---


# 串流擷取概觀

Adobe Experience Platform的串流擷取為使用者提供即時從用戶端和伺服器端裝置傳送資料 [!DNL Experience Platform] 的方法。

## 您可以使用串流擷取功能做什麼？

Adobe Experience Platform可讓您為個別客戶產生一致、一致且相關的 [!DNL Real-time Customer Profile] 協調體驗。 串流擷取在建立這些描述檔時扮演了關鍵角色，讓您在盡可能 [!DNL Profile] 少的延遲 [!DNL Data Lake] 下，將資料傳送至其中。

以下視訊旨在協助您瞭解串流擷取，並概述上述概念。

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### 串流描述檔記錄和 [!DNL ExperienceEvents]

透過串流擷取，使用者可以在數秒 [!DNL ExperienceEvents] 內串流 [!DNL Platform] 個人檔案記錄，協助推動即時個人化。 傳送至串流擷取API的所有資料都會自動保留在 [!DNL Data Lake]中。

請閱讀建立 [串流連線指南](../tutorials/create-streaming-connection.md) ，以取得詳細資訊。

### 串流至資料集

一旦您確信資料是乾淨的，您就可以為和啟用資料 [!DNL Real-time Customer Profile] 集 [!DNL Identity Service]。

有關為和啟用資料集的更 [!DNL Profile] 多信 [!DNL Identity Service]息，請閱 [讀配置資料集指南](../../profile/tutorials/dataset-configuration.md)。

## What is the expected latency for streaming ingestion on [!DNL Platform]?

| 目的地 | 預期延遲 |
| --------- | ---------------- |
| 即時客戶個人檔案 | &lt; 1分鐘 |
| Data Lake | &lt; 60 分鐘 |

## Adobe Experience Platform 擴充功能

您可以使用Adobe Experience Platform擴充功能建立新的串流連線。 擴充 [!DNL Experience Platform] 功能可提供動作，讓您傳送格式 [!DNL Experience Data Model] 為(XDM)的信標，以便即時擷取 [!DNL Experience Platform]至。 請造訪 [Experience Platform Extension](https://docs.adobe.com/content/help/en/launch/using/extensions-ref/adobe-extension/adobe-experience-platform-extension.html) 檔案，以取得詳細資訊。