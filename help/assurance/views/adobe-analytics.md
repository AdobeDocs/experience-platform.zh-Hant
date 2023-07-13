---
title: 在 Assurance 中檢視 Adob​​e Analytics
description: 本指南會說明如何將 Adobe Analytics 和 Adob​​e Experience Platform Assurance 一起使用。
exl-id: e5cc72b0-d6d6-430b-9321-4835c1f77581
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: ht
source-wordcount: '359'
ht-degree: 100%

---

# 在 Assurance 中檢視 Adob&#x200B;&#x200B;e Analytics

Adobe Experience Platform Assurance 和 Adob&#x200B;&#x200B;e Analytics 的整合為對其 Ad&#x200B;&#x200B;ob&#x200B;&#x200B;e Analytics 實作進行偵錯和驗證的使用者提供了對 SDK 事件更豐富的檢視。該檢視現在會顯示從 [Adobe Experience Platform SDK](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/) 傳送至 Adob&#x200B;&#x200B;e Analytics 的生命週期和動作/狀態事件。該檢視還會顯示「回應」的詳細資料，提供有關分別套用每個報表套裝的處理規則後如何處理事件的資訊。

![](./images/adobe-analytics/overview.png)

## 快速入門

繼續進行之前，請確保您擁有以下服務：

- [Adobe Experience Platform 資料集合 UI](https://experience.adobe.com/#/data-collection/)。
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

若要了解如何在您的應用程式中安裝 Assurance，請詳閱[實作 Assurance 指南](../tutorials/implement-assurance.md)。

## 後續處理的狀態

SDK 向 Adob&#x200B;&#x200B;e Analytics 提出網路要求後，該狀態會告知您 Assurance 是否能夠擷取 Adob&#x200B;&#x200B;e Analytics 要求的後續處理資訊。

請注意，為了擷取後續處理資訊，已登入的使用者必須有權存取相對應的報表套裝。

| 狀態 | 說明 |
| :----- | :---------- |
| `Queued` | 網路要求正在擷取後續處理資訊。 |
| `Processed` | 網路要求成功，已收到後續處理資訊。 |
| `Delayed` | 已超出擷取後續處理資訊的要求重試次數上限。 |
| `Error` | 錯誤已導致網路要求失敗。有關錯誤的更多詳細資料會顯示在事件詳細資料檢視中。 |
| `Unauthorized` | 使用者無權存取 Adob&#x200B;&#x200B;e Analytics 報表套裝。 |
| `Unavailable` | Adobe Analytics 要求沒有相對應的 `AnalyticsResponse` 事件。 |
| `No Debug Flag` | 目前的 Adob&#x200B;&#x200B;e Analytics 或 Assurance SDK 版本可能不支援 Analytics 的偵錯功能。如需詳細資訊，請詳閱[疑難排解指南](../troubleshooting.md)。 |
| `Expired` | 此 `AnalyticsTrack` 或 `LifecycleStart` 事件發生時間已超過 24 小時。 |

## 事件詳細資料檢視

對 Analytics 追蹤事件的詳細檢視會包含以下有價值的部分：

- 起源的 SDK Analytics 要求事件。
- 來自要求的 OOTB 中繼和內容資料，例如報表套裝 ID、SDK 擴充功能版本、OOTB 內容資料等。
- 有關 Analytics 事件的後續處理資訊，其中會包含 Revar、eVar、Prop 等的對應。
