---
keywords: Experience Platform；主題；熱門主題；邊緣分割；分段服務；分段服務；用戶介面；流媒體；
solution: Experience Platform
title: 邊緣分割UI指南
description: 邊緣分割是指能夠即時評估平台中的邊緣段，從而實現相同的頁面和下一頁個性化使用案例。
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 0%

---

# 邊緣分段服務 UI 指南

>[!NOTE]
>
>現在，所有平台用戶都可以使用邊緣分割。 如果在測試期間建立了邊段，則這些段將繼續運行。

邊緣分割是一種即時評估Adobe Experience Platform區段的能力 [在邊緣](../../edge/home.md)，啟用相同的頁面和下一頁個性化用例。

>[!IMPORTANT]
>
> 邊緣資料將儲存在最靠近其收集位置的邊緣伺服器位置，並且可以儲存在指定為集線器（或主體）Adobe Experience Platform資料中心的位置以外的位置。
>
> 此外，邊緣分割引擎將僅處理存在邊緣的請求 **一個** 主標籤標識，與非基於邊緣的主標識一致。

## 邊緣分割查詢類型 {#query-types}

當前只能使用邊緣分割來計算所選查詢類型。 以下各節提供了查詢類型清單，這些查詢類型可通過邊緣分割和當前不支援的查詢類型進行計算。

如果查詢滿足下表中概述的任何條件，則可使用邊切分來評估該查詢。

>[!NOTE]
>
>如果查詢與下表中的任何查詢類型匹配，則將使用邊切分自動評估該查詢。 系統根據查詢表達式自動確定此功能。

| 查詢類型 | 詳細資訊 | 範例 | PQL示例 |
| ---------- | ------- | ------- | ----------- |
| 單個事件 | 任何引用無時間限制的單個傳入事件的段定義。 | 已將物料添加到購物車中的人員。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| 單個配置檔案 | 引用單個僅配置檔案屬性的任何段定義 | 住在美國的人。 | `homeAddress.countryCode = "US"` |
| 引用配置檔案的單個事件 | 引用一個或多個配置檔案屬性和單個傳入事件且沒有時間限制的任何段定義。 | 訪問首頁的美國人。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")])` |
| 使用配置檔案屬性否定單個事件 | 任何引用否定的單個傳入事件和一個或多個配置檔案屬性的段定義 | 生活在美國並擁有 **不** 已訪問首頁。 | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| 時間窗口內的單個事件 | 任何段定義，它指的是在設定的時間段內的單個傳入事件。 | 過去24小時內訪問首頁的人。 | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)])` |
| 時間窗口內具有配置檔案屬性的單個事件 | 在設定的時間段內引用一個或多個配置檔案屬性和單個傳入事件的任何段定義。 | 過去24小時內訪問首頁的美國人。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)])` |
| 在時間窗口內使用配置檔案屬性否定單個事件 | 指一個或多個配置檔案屬性和一個時間段內否定的單個傳入事件的任何段定義。 | 生活在美國並擁有 **不** 在過去24小時內訪問了首頁。 | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)]))` |
| 24小時時間窗內的頻率事件 | 任何段定義，指在24小時的時間窗口內發生一定次數的事件。 | 訪問首頁的人 **至少** 24小時內有5次。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 在24小時時間窗口內具有配置檔案屬性的頻率事件 | 指一個或多個配置檔案屬性以及在24小時的時間窗口內發生一定次數的事件的任何段定義。 | 訪問首頁的美國人 **至少** 24小時內有5次。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 在24小時時間窗口內使用配置檔案否定頻率事件 | 任何段定義，它指一個或多個配置檔案屬性以及在24小時的時間窗口內發生一定次數的已取消事件。 | 未訪問首頁的人 **更多** 比過去24小時里多了5次。 | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| 在24小時內的時間配置檔案內多次傳入命中 | 任何段定義，指在24小時的時間窗口內發生的多個事件。 | 訪問首頁的人員 **或** 在過去24小時內訪問了簽出頁面。 | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 在24小時時間窗口內使用配置檔案的多個事件 | 任何段定義，它指在24小時的時間窗口內發生的一個或多個配置檔案屬性和多個事件。 | 訪問首頁的美國人 **和** 在過去24小時內訪問了簽出頁面。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 分部 | 包含一個或多個批或流段的任何段定義。 | 居住在美國並屬於&quot;現有部門&quot;的人。 | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| 引用映射的查詢 | 任何引用屬性映射的段定義。 | 已基於外部段資料添加到購物車中的人員。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

段定義將 **不** 在以下情況下啟用邊緣分割：

- 段定義包括單個事件和 `inSegment` 的子菜單。
   - 然而，倘分部包含於 `inSegment` 事件僅是配置檔案，段定義 **會** 啟用邊緣分割。

## 後續步驟

本指南介紹如何在Adobe Experience Platform上使用邊緣分割來評估段。 要瞭解有關使用Experience Platform用戶介面的詳細資訊，請閱讀 [分段使用手冊](./overview.md)。 要瞭解如何使用Experience PlatformAPI執行類似操作和使用段，請訪問 [邊緣分割API指南](../api/edge-segmentation.md)。

## 附錄

以下部分列出了有關邊緣分割的常見問題：

### 在邊緣網路上提供一個網段需要多長時間？

在邊緣網路上可用的網段最多需要一個小時。