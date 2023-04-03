---
title: Adobe Analytics在保障中的檢視
description: 本指南說明如何搭配Adobe Experience Platform Assurance使用Adobe Analytics。
source-git-commit: 07dc01c11c79ac2dad05d89309cabb5715c0b63c
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 2%

---


# Adobe Analytics在保障中的檢視

Adobe Experience Platform保證與Adobe Analytics的整合為除錯及驗證其Adobe Analytics實作的使用者提供SDK事件的更豐富檢視。 檢視現在會顯示從 [Adobe Experience Platform SDK](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/). 此檢視也提供「回應」詳細資訊，提供在應用每個報表套裝處理規則後，事件的處理方式資訊。

![](./images/adobe-analytics/overview.png)

## 快速入門

繼續之前，請確定您有下列服務：

- 此 [Adobe Experience Platform資料收集UI](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform保障](https://experience.adobe.com/assurance)

若要了解如何在您的應用程式中安裝Assurance，請閱讀 [實作保證指南](../tutorials/implement-assurance.md).

## 處理後狀態

SDK使用Adobe Analytics提出網路要求後，狀態會告訴您「保證」是否能擷取Adobe Analytics要求的後置處理資訊。

請注意，若要擷取後續處理資訊，登入的使用者必須擁有對應報表套裝的存取權。

| 狀態 | 說明 |
| :----- | :---------- |
| `Queued` | 網路請求正在獲取後處理資訊。 |
| `Processed` | 網路請求已成功，並且接收了後處理資訊。 |
| `Delayed` | 已超過重試擷取後續處理資訊的請求數上限。 |
| `Error` | 錯誤導致網路請求失敗。 有關錯誤的更多詳細資料會顯示在事件詳細資料檢視中。 |
| `Unauthorized` | 使用者無法存取Adobe Analytics報表套裝。 |
| `Unavailable` | Adobe Analytics要求沒有對應的 `AnalyticsResponse` 事件。 |
| `No Debug Flag` | 目前的Adobe Analytics或Assurance SDK版本可能不支援Analytics除錯功能。 欲知更多資訊，請閱讀 [疑難排解指南](../troubleshooting.md). |
| `Expired` | 此 `AnalyticsTrack` 或 `LifecycleStart` 事件超過24小時。 |

## 事件詳細資料檢視

對於Analytics追蹤事件，詳細檢視包含下列重要部分：

- 原始SDK Analytics請求事件。
- 請求的OOTB中繼和內容資料，例如報表套裝ID、SDK擴充功能版本、OOTB內容資料等。
- Analytics事件的後置處理資訊，包含revar、evar、prop等的對應。
