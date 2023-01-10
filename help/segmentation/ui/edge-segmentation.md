---
keywords: Experience Platform；首頁；熱門主題；邊緣分段；分段服務；分段服務；ui指南；串流邊緣；
solution: Experience Platform
title: Edge Segmentation UI指南
description: 邊緣分段是即時在邊緣上評估Platform中區段的功能，可啟用相同的頁面和下一頁個人化使用案例。
exl-id: eae948e6-741c-45ce-8e40-73d10d5a88f1
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '939'
ht-degree: 0%

---

# Edge劃分UI指南

>[!NOTE]
>
>現在所有Platform使用者都能使用邊緣區段。 如果您在測試期間建立邊緣區段，這些區段將可繼續運作。

邊緣分割是即時評估Adobe Experience Platform中區段的功能 [在邊緣](../../edge/home.md)，啟用相同頁面和下一頁個人化的使用案例。

>[!IMPORTANT]
>
> 邊緣資料會儲存在最靠近其收集位置的邊緣伺服器位置，並可儲存在指定為中樞（或主要）Adobe Experience Platform資料中心以外的位置。
>
> 此外，邊緣分段引擎只會執行邊緣上有的請求 **one** 主要標示身分，與非邊緣型主要身分一致。

## 邊緣分段查詢類型 {#query-types}

目前，只有選取的查詢類型才能透過邊緣分段來評估。 以下各節提供可透過邊緣分段評估的查詢類型清單，以及目前不支援的查詢類型。

如果查詢符合下表中列出的任何條件，則可使用邊緣分段來評估查詢。

>[!NOTE]
>
>如果查詢符合下表中的任何查詢類型，系統就會使用邊緣分段自動評估查詢。 系統會根據查詢運算式自動決定此功能。

| 查詢類型 | 詳細資訊 | 範例 | PQL示例 |
| ---------- | ------- | ------- | ----------- |
| 單一事件 | 任何區段定義，是指沒有時間限制的單一傳入事件。 | 已將項目新增至購物車的使用者。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart")])` |
| 單一設定檔 | 任何參考單一僅限設定檔屬性的區段定義 | 住在美國的人。 | `homeAddress.countryCode = "US"` |
| 參照設定檔的單一事件 | 任何區段定義，是指一或多個設定檔屬性以及沒有時間限制的單一傳入事件。 | 訪問首頁的美國居民。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")])` |
| 使用設定檔屬性否定單一事件 | 任何區段定義，是指否定的單一傳入事件和一或多個設定檔屬性 | 住在美國並擁有 **not** 造訪首頁。 | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView")]))` |
| 一個時間範圍內的單一事件 | 任何區段定義，是指在指定的時間內單一傳入事件。 | 過去24小時內造訪首頁的人。 | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)])` |
| 時間視窗內具有設定檔屬性的單一事件 | 任何區段定義，指的是一或多個設定檔屬性，以及設定時間內的單一傳入事件。 | 過去24小時內造訪首頁的美國人。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)])` |
| 在時間窗口內用配置檔案屬性否定單個事件 | 任何區段定義，指的是一或多個設定檔屬性以及一段時間內否定的單一傳入事件。 | 住在美國並擁有 **not** 在過去24小時內瀏覽了首頁。 | `homeAddress.countryCode = "US" and not(chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 8 days before now)]))` |
| 24小時時段內的頻率事件 | 任何區段定義，是指在24小時的時間範圍內發生特定次數的事件。 | 造訪首頁的人員 **至少** 24小時內五次。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 在24小時時段內具有設定檔屬性的頻率事件 | 任何區段定義，指的是一或多個設定檔屬性，以及在24小時的時間範圍內發生特定次數的事件。 | 訪問首頁的美國人 **至少** 24小時內五次。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] )` |
| 在24小時時段內使用設定檔否定頻率事件 | 任何區段定義，指的是一或多個設定檔屬性，以及在24小時的時間範圍內發生特定次數的否定事件。 | 未訪問首頁的人 **更多** 在過去的24小時里不過5次。 | `not(chain(xEvent, timestamp, [A: WHAT(eventType = "homePageView") WHEN(< 24 hours before now) COUNT(5) ] ))` |
| 在24小時的時間設定檔內傳入多個點擊 | 任何區段定義，是指在24小時的時間範圍內發生的多個事件。 | 瀏覽首頁的人員 **或** 在過去24小時內瀏覽了結帳頁面。 | `chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 在24小時時段內使用設定檔執行多個事件 | 任何區段定義，是指在24小時的時間範圍內發生的一或多個設定檔屬性和多個事件。 | 訪問首頁的美國人 **和** 在過去24小時內瀏覽了結帳頁面。 | `homeAddress.countryCode = "US" and chain(xEvent, timestamp, [X: WHAT(eventType = "homePageView") WHEN(< 24 hours before now)]) and chain(xEvent, timestamp, [X: WHAT(eventType = "checkoutPageView") WHEN(< 24 hours before now)])` |
| 區段 | 包含一或多個批次或串流區段的任何區段定義。 | 居住在美國且位於「現有區段」區段的人。 | `homeAddress.countryCode = "US" and inSegment("existing segment")` |
| 引用映射的查詢 | 任何參考屬性地圖的區段定義。 | 根據外部區段資料新增至購物車的使用者。 | `chain(xEvent, timestamp, [A: WHAT(eventType = "addToCart") WHERE(externalSegmentMapProperty.values().exists(stringProperty="active"))])` |

區段定義將 **not** 在下列情況下啟用邊緣分段功能：

- 區段定義包含單一事件和 `inSegment` 事件。
   - 不過，若 `inSegment` 事件僅限設定檔，區段定義 **will** 啟用邊緣分割功能。

## 後續步驟

本指南說明如何在Adobe Experience Platform上透過邊緣分段評估區段。 若要進一步了解如何使用Experience Platform使用者介面，請閱讀 [區段使用手冊](./overview.md). 若要了解如何使用Experience PlatformAPI執行類似動作及使用區段，請造訪 [邊緣劃分API指南](../api/edge-segmentation.md).

## 附錄

下節列出邊緣區段的常見問題：

### 邊緣網路上可用區段需要多久的時間？

在邊緣網路上可用區段最多需要1小時。