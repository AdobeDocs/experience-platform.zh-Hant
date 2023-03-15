---
keywords: Experience Platform；首頁；熱門主題；資料擷取；擷取資料；串流；概觀；串流擷取；延遲；串流延遲；
solution: Experience Platform
title: 串流擷取概述
description: Adobe Experience Platform的串流內嵌功能可讓使用者透過用戶端和伺服器端裝置，即時傳送資料至Experience Platform。
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 2%

---

# 串流獲取概觀

Adobe Experience Platform的串流內嵌功能可讓使用者以方法將資料從用戶端和伺服器端裝置傳送至 [!DNL Experience Platform] 即時。

## 您可以透過串流獲取做什麼？

Adobe Experience Platform可讓您透過產生 [!DNL Real-Time Customer Profile] 針對每個客戶。 串流內嵌功能可讓您提供內容，在建立這些設定檔時發揮關鍵作用 [!DNL Profile] 資料 [!DNL Data Lake] 盡可能縮短延遲時間。

以下影片旨在協助您了解串流擷取，並概述上述概念。

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### 資料流設定檔記錄和 [!DNL ExperienceEvents]

透過串流內嵌，使用者可以串流設定檔記錄和 [!DNL ExperienceEvents] to [!DNL Platform] 以秒為單位，協助推動即時個人化。 所有傳送至串流獲取API的資料都會自動保存在 [!DNL Data Lake].

請閱讀 [建立串流連線指南](../tutorials/create-streaming-connection.md) 以取得更多資訊。

### 串流至資料集

確信資料乾淨後，即可為 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service].

如需啟用資料集的詳細資訊，請參閱 [!DNL Profile] 和 [!DNL Identity Service]，請閱讀 [設定資料集指南](../../profile/tutorials/dataset-configuration.md).

## 串流擷取的預期延遲為何 [!DNL Platform]?

| 目的地 | 預期延遲 |
| --------- | ---------------- |
| 即時客戶設定檔 | &lt; 1分鐘 |
| 資料湖 | &lt; 60 分鐘 |

## 流獲取的每秒請求數(RPS)指導

下表顯示串流獲取的要求每秒限制指引。

| RPS限制 | 附註 |
| --- | --- |
| 每秒1000個請求 | 若使用 `/collection/batch` 端點。 |
| 每秒10000條個人報文 | 使用 `/collection/batch` 端點。 |

>[!IMPORTANT]
>
>強制限制會變成 **每分鐘60次請求** 將同步驗證用於偵錯用途時。

## Adobe Experience Platform 擴充功能

您可以使用Adobe Experience Platform擴充功能建立新的串流連線。 此 [!DNL Experience Platform] 擴充功能提供傳送中格式之信標的動作 [!DNL Experience Data Model] (XDM)，即時擷取至 [!DNL Experience Platform]. 造訪 [Experience Platform擴充功能](../../tags/extensions/client/sdk/overview.md) 檔案以取得詳細資訊。
