---
title: Adobe Analytics在保障中的觀點
description: 本指南說明如何將Adobe Analytics與Adobe Experience Platform保證公司配合使用。
exl-id: e5cc72b0-d6d6-430b-9321-4835c1f77581
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '359'
ht-degree: 3%

---

# Adobe Analytics在保障中的觀點

與Adobe Analytics的Adobe Experience Platform保障整合為用戶調試和驗證其Adobe Analytics實施提供了更豐富的SDK事件視圖。 此視圖現在顯示從 [Adobe Experience PlatformSDK](https://developer.adobe.com/client-sdks/documentation/adobe-analytics/)。 該視圖還具有「響應」詳細資訊，提供有關在應用每個相應報告套件的處理規則之後如何處理事件的資訊。

![](./images/adobe-analytics/overview.png)

## 快速入門

在繼續之前，請確保您有以下服務：

- 的 [Adobe Experience Platform資料收集UI](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

要瞭解如何在應用程式中安裝Assurance，請閱讀 [實施保障指南](../tutorials/implement-assurance.md)。

## 後處理狀態

SDK向Adobe Analytics發出網路請求後，狀態將告訴您Assurance是否能夠檢索Adobe Analytics請求的後處理資訊。

請注意，要檢索後處理資訊，登錄用戶必須有權訪問相應的報告套件。

| 狀態 | 說明 |
| :----- | :---------- |
| `Queued` | 網路請求正在獲取後處理資訊。 |
| `Processed` | 網路請求成功，並且接收後處理資訊。 |
| `Delayed` | 已超過獲取後處理資訊的請求重試的最大次數。 |
| `Error` | 錯誤導致網路請求失敗。 有關該錯誤的詳細資訊顯示在事件詳細資訊視圖中。 |
| `Unauthorized` | 用戶無權訪問Adobe Analytics報告套件。 |
| `Unavailable` | Adobe Analytics請求沒有 `AnalyticsResponse` 的子菜單。 |
| `No Debug Flag` | 當前的Adobe Analytics或Assurance SDK版本可能不支援分析調試功能。 有關詳細資訊，請閱讀 [故障排除指南](../troubleshooting.md)。 |
| `Expired` | 的 `AnalyticsTrack` 或 `LifecycleStart` 事件超過24小時。 |

## 事件詳細資訊視圖

對於分析跟蹤事件，詳細視圖包含以下重要部分：

- 發起的SDK分析請求事件。
- 來自請求的OOTB元和上下文資料，如報表套件ID、SDK擴展版本、OOTB上下文資料等。
- 有關分析事件的後處理資訊，該事件包含revars、evars、props等的映射。
