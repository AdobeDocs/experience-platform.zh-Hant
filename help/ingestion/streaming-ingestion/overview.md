---
keywords: Experience Platform；首頁；熱門主題；資料擷取；擷取的資料；串流；概觀；串流擷取；延遲；串流延遲；
solution: Experience Platform
title: 串流擷取概觀
description: 瞭解Adobe Experience Platform中的串流擷取。
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: 58f69a78fb3c622c8741d7a1618f15509c160a5b
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 2%

---

# 串流攝取概觀

Adobe Experience Platform的串流擷取為使用者提供一種方法，可即時從使用者端和伺服器端裝置傳送資料至Experience Platform。

## 您可以使用串流擷取做什麼？

Adobe Experience Platform可讓您為每個個別客戶產生即時客戶設定檔，藉此推動協調、一致且相關的體驗。 串流擷取可讓您以儘可能少的延遲將設定檔資料傳送至Data Lake，因此在建立這些設定檔的過程中扮演關鍵角色。

以下影片旨在協助您瞭解串流擷取，並概述上述概念。

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### 串流設定檔記錄和[!DNL ExperienceEvents]

透過串流擷取，使用者可在數秒內將設定檔記錄和[!DNL ExperienceEvents]串流到Experience Platform，以推動即時個人化。 所有傳送至串流獲取API的資料都會自動保留在資料湖中。

如需詳細資訊，請參閱[建立串流連線指南](../tutorials/create-streaming-connection.md)。

### 資料集的資料流

一旦您確定您的資料是乾淨的，就可以為Real-Time Customer Profile和[!DNL Identity Service]啟用資料集。

如需為設定檔和[!DNL Identity Service]啟用資料集的詳細資訊，請參閱[設定資料集指南](/help/profile/tutorials/dataset-configuration.md)。

## 在Experience Platform上串流擷取預計會延遲多久？

>[!IMPORTANT]
>
>串流擷取的護欄會繫結至與整個組織對應的授權使用權益總計。 此外，開發沙箱中的資料使用量限製為您的設定檔總數的10%。 如需授權使用權益的詳細資訊，請閱讀[資料管理最佳實務指南](/help/landing/license-usage-and-guardrails/data-management-best-practices.md)。 若要瞭解如何設定串流輸送量的限制，請閱讀[容量概觀](../../landing/license-usage-and-guardrails/capacity.md)。

| 目標 | 預期延遲 |
| --------- | ---------------- |
| 即時客戶輪廓 | <ul><li>&lt; B2C資料擷取的第95百分位數為15分鐘。</li><li>&lt; B2B資料擷取的第95百分位數為30分鐘。</li></ul> |
| 資料湖 | &lt; 60分鐘 |

## 串流擷取的每秒要求(RPS)指引

下表顯示串流擷取的請求秒數限制指南。

| RPS限制 | 附註 |
| --- | --- |
| 每秒1000個請求 | 這些可在使用`/collection/batch`端點時包含多個訊息。 |
| 每秒10000傳個別訊息 | 使用`/collection/`端點時，可將訊息分組為較少的實際要求。 |

>[!IMPORTANT]
>
>使用同步驗證時，強制限制變成每分鐘&#x200B;**60個要求**，因為它是用於偵錯目的。

## Adobe Experience Platform擴充功能

您可以使用Adobe Experience Platform擴充功能來建立新的串流連線。 [!DNL Experience Platform]擴充功能提供動作，可傳送格式化為[!DNL Experience Data Model] (XDM)的信標以即時擷取至[!DNL Experience Platform]。 如需詳細資訊，請造訪[Experience Platform擴充功能](/help/tags/extensions/client/web-sdk/overview.md)檔案。
