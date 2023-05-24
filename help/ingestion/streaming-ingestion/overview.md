---
keywords: Experience Platform；首頁；熱門主題；資料接收；接收資料；流；概述；流接收；延遲；流處理；流處理；；首頁；熱門主題；資料接收；接收；流處理；流處理；概述；流處理；延遲；流處理；
solution: Experience Platform
title: 流式接收概述
description: Adobe Experience Platform的流接收為用戶提供了一種從客戶端和伺服器端設備向Experience Platform即時發送資料的方法。
exl-id: 851f15fd-7ac5-4a9f-934d-6b907057da87
source-git-commit: e802932dea38ebbca8de012a4d285eab691231be
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 3%

---

# 串流擷取概觀

Adobe Experience Platform的流接收為用戶提供了從客戶端和伺服器端設備向 [!DNL Experience Platform] 即時。

## 你能用流式攝入做什麼？

Adobe Experience Platform通過建立 [!DNL Real-Time Customer Profile] 為每個客戶。 流式接收在構建這些配置檔案中起著關鍵作用，它使您能夠提供 [!DNL Profile] 資料 [!DNL Data Lake] 盡可能少的延遲。

以下視頻旨在幫助您理解流攝入，並概述上述概念。

>[!VIDEO](https://video.tv.adobe.com/v/28425?quality=12&learn=on)

### 流配置檔案記錄和 [!DNL ExperienceEvents]

通過流式接收，用戶可以流式傳輸配置檔案記錄和 [!DNL ExperienceEvents] 至 [!DNL Platform] 幫助即時個性化。 發送到流式接收API的所有資料將自動保留在 [!DNL Data Lake]。

請閱讀 [建立流連接指南](../tutorials/create-streaming-connection.md) 的子菜單。

### 流到資料集

一旦您確信資料是乾淨的，就可以為 [!DNL Real-Time Customer Profile] 和 [!DNL Identity Service]。

有關為 [!DNL Profile] 和 [!DNL Identity Service]，請閱讀 [配置資料集指南](../../profile/tutorials/dataset-configuration.md)。

## 上的流式接收預期延遲是什麼 [!DNL Platform]?

| 目的地 | 預期延遲 |
| --------- | ---------------- |
| 即時客戶設定檔 | &lt;1分鐘 |
| 達塔湖 | &lt; 60 分鐘 |

## 每秒請求(RPS)流接收指導

下表顯示關於流式接收的每秒請求限制的指導。

| RPS限制 | 附註 |
| --- | --- |
| 每秒1000次請求 | 當使用 `/collection/batch` 端點。 |
| 每秒10000條單條消息 | 使用 `/collection/batch` 端點。 |

>[!IMPORTANT]
>
>強制限制將變為 **每分鐘60次請求** 使用同步驗證時，將其用於調試。

## Adobe Experience Platform 擴充功能

可以使用Adobe Experience Platform擴展建立新的流連接。 的 [!DNL Experience Platform] 擴展提供了在中發送格式化的信標的操作 [!DNL Experience Data Model] (XDM)，用於即時接收 [!DNL Experience Platform]。 訪問 [Experience Platform擴展](../../tags/extensions/client/sdk/overview.md) 的子菜單。
