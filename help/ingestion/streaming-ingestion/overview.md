---
keywords: Experience Platform；首頁；熱門主題；資料擷取；擷取的資料；串流；概觀；串流擷取；延遲；串流延遲；
solution: Experience Platform
title: 串流擷取概觀
description: Adobe Experience Platform的串流擷取為使用者提供從使用者端和伺服器端裝置傳送資料以即時Experience Platform的方法。
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: 008537dffff4cc428de9070964446f4e7ebf039f
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 3%

---

# 串流擷取概觀

Adobe Experience Platform的串流擷取為使用者提供一種從使用者端和伺服器端裝置傳送資料至的方法 [!DNL Experience Platform] 即時。

## 您可以使用串流擷取做什麼？

Adobe Experience Platform可讓您透過產生 [!DNL Real-Time Customer Profile] 適用於每個個別客戶。 串流擷取可讓您傳送，因此在建立這些設定檔時扮演關鍵角色 [!DNL Profile] 資料進入 [!DNL Data Lake] 儘可能縮短延遲時間。

以下影片旨在協助您瞭解串流擷取，並概述上述概念。

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### 串流設定檔記錄和 [!DNL ExperienceEvents]

透過串流擷取，使用者可以串流設定檔記錄並 [!DNL ExperienceEvents] 至 [!DNL Platform] 幾秒鐘內即可協助推動即時個人化。 所有傳送至串流獲取API的資料都會自動儲存在 [!DNL Data Lake].

請閱讀 [建立串流連線指南](../tutorials/create-streaming-connection.md) 以取得詳細資訊。

### 資料集的資料流

一旦您確定您的資料是乾淨的，就可以為以下專案啟用資料集 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service].

如需啟用資料集的詳細資訊，請參閱 [!DNL Profile] 和 [!DNL Identity Service]，請閱讀 [設定資料集指南](../../profile/tutorials/dataset-configuration.md).

## 串流擷取的預期延遲為何？ [!DNL Platform]？

| 目的地 | 預期延遲 |
| --------- | ---------------- |
| 即時客戶設定檔 | &lt; 1分鐘 |
| 資料湖 | &lt; 60 分鐘 |

## 串流擷取的每秒要求(RPS)指引

下表顯示串流擷取的請求秒數限制指南。

| RPS限制 | 附註 |
| --- | --- |
| 每秒1000個請求 | 使用時，這些可包含多則訊息 `/collection/batch` 端點。 |
| 每秒10000傳個別訊息 | 使用時，可將訊息分組為較少的實際請求 `/collection/batch` 端點。 |

>[!IMPORTANT]
>
>強制限制會變成 **每分鐘60個請求** 使用預期用於偵錯用途的同步驗證時。

## Adobe Experience Platform 擴充功能

您可以使用Adobe Experience Platform擴充功能來建立新的串流連線。 此 [!DNL Experience Platform] 擴充功能提供傳送信標的動作，格式化方式為 [!DNL Experience Data Model] (XDM)用於即時擷取至 [!DNL Experience Platform]. 造訪 [Experience Platform擴充功能](../../tags/extensions/client/web-sdk/overview.md) 檔案以取得詳細資訊。
