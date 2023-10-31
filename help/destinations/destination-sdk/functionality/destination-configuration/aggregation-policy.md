---
description: 瞭解如何設定彙總原則，以判斷應如何分組和批次傳送目的地的HTTP請求。
title: 彙總原則
exl-id: 2dfa8815-2d69-4a22-8938-8ea41be8b9c5
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '995'
ht-degree: 2%

---

# 彙總原則

為確保將資料匯出至API端點時發揮最大效率，您可以使用各種設定將匯出的設定檔彙總為較大或較小的批次、依身分將其分組，以及其他使用案例。 這也允許您量身打造資料匯出以符合API端點的任何下游限制（速率限制、每個API呼叫的身分數量等）。

使用可設定的彙總來深入探討Destination SDK提供的設定，或使用盡力彙總來告知Destination SDK儘可能批次處理API呼叫。

使用Destination SDK建立即時（串流）目的地時，您可以設定應如何在產生的匯出中結合匯出的設定檔。 此行為由彙總原則設定決定。

若要瞭解此元件在何處適合使用Destination SDK建立的整合，請參閱 [設定選項](../configuration-options.md) 檔案或請參閱操作說明指南 [使用Destination SDK設定串流目的地](../../guides/configure-destination-instructions.md#create-destination-configuration).

您可以透過 `/authoring/destinations` 端點。 請參閱下列API參考頁面，以取得詳細的API呼叫範例，您可在此範例設定本頁面中顯示的元件。

* [建立目的地設定](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目的地設定](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文說明可用於目的地的所有支援彙總原則設定。

閱讀本檔案後，請參閱以下檔案： [使用範本](../../functionality/destination-server/message-format.md#using-templating) 和 [彙總索引鍵範例](../../functionality/destination-server/message-format.md#template-aggregation-key) 瞭解如何根據您選取的彙總原則，將彙總原則納入訊息轉換範本中。

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值如下 **區分大小寫**. 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 支援的整合型別 {#supported-integration-types}

如需瞭解哪些型別的整合支援本頁面所述功能的詳細資訊，請參閱下表。

| 整合型別 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 無 |

## 最大努力彙總 {#best-effort-aggregation}

盡最大努力彙總最適合以下目的地：每個請求偏好的設定檔較少，且更願意接收較少數量的請求，而非接收較少數量的請求，但資料較多時。

以下設定範例顯示最大努力彙總設定。 如需可設定的彙總範例，請參閱 [可設定的彙總](#configurable-aggregation) 區段。 下表記錄適用於最大努力彙總的引數。

```json
"aggregation":{
   "aggregationType":"BEST_EFFORT",
   "bestEffortAggregation":{
      "maxUsersPerRequest":10,
      "splitUserById":false
   }
}
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `aggregationType` | 字串 | 指示您的目的地應使用的彙總原則型別。 支援的彙總型別： <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `bestEffortAggregation.maxUsersPerRequest` | 整數 | Experience Platform可以在單一HTTP呼叫中彙總多個匯出的設定檔。 <br><br>此值表示您的端點在單一HTTP呼叫中應接收的設定檔數目上限。 請注意，這是最大努力彙總。 例如，如果您指定值100，Platform在呼叫時可能會傳送任何數量小於100的設定檔。 <br><br> 如果您的伺服器不接受每個請求多個使用者，請將此值設為 `1`. |
| `bestEffortAggregation.splitUserById` | 布林值 | 如果對目的地的呼叫應該依身分分割，請使用此旗標。 將此標幟設為 `true` 如果您的伺服器僅接受一個特定身分名稱空間之每次呼叫的身分。 |

{style="table-layout:auto"}

>[!TIP]
>
>如果您的API端點接受每個API呼叫少於100個設定檔，請使用最大努力彙總。

## 可設定的彙總 {#configurable-aggregation}

如果您偏好以大型批次進行，且同一呼叫具有數千個設定檔，可設定的彙總將最有效果。 此選項也可讓您根據複雜的彙總規則來彙總匯出的設定檔。

以下設定範例顯示可設定的彙總設定。 如需最大努力彙總的範例，請參閱 [最大努力彙總](#best-effort-aggregation) 區段。 下表記錄適用於可設定之彙總的引數。

```json
"aggregation":{
   "aggregationType":"CONFIGURABLE_AGGREGATION",
   "configurableAggregation":{
      "splitUserById":true,
      "maxBatchAgeInSecs":2400,
      "maxNumEventsInBatch":5000,
      "aggregationKey":{
         "includeSegmentId":true,
         "includeSegmentStatus":true,
         "includeIdentity":true,
         "oneIdentityPerGroup":true,
         "groups":[
            {
               "namespaces":[
                  "IDFA",
                  "GAID"
               ]
            },
            {
               "namespaces":[
                  "EMAIL"
               ]
            }
         ]
      }
   }
}
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `aggregationType` | 字串 | 指示您的目的地應使用的彙總原則型別。 支援的彙總型別： <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `configurableAggregation.splitUserById` | 布林值 | 如果對目的地的呼叫應該依身分分割，請使用此旗標。 將此標幟設為 `true` 如果您的伺服器僅接受一個特定身分名稱空間之每次呼叫的身分。 |
| `configurableAggregation.maxBatchAgeInSecs` | 整數 | 搭配使用 `maxNumEventsInBatch`，此引數會決定Experience Platform在傳送API呼叫至端點時應等候多久。 <ul><li>最小值（秒）：1800</li><li>最大值（秒）：3600</li></ul> 例如，如果您將兩個引數的最大值都使用，Experience Platform會等待3600秒或直到10000有合格的設定檔為止，再進行API呼叫（以先發生者為準）。 |
| `configurableAggregation.maxNumEventsInBatch` | 整數 | 搭配使用 `maxBatchAgeInSecs`，此引數會決定API呼叫中應該彙總多少個合格設定檔。 <ul><li>最小值： 1000</li><li>最大值： 10000</li></ul> 例如，如果您將兩個引數的最大值都使用，Experience Platform會等待3600秒或直到10000有合格的設定檔為止，再進行API呼叫（以先發生者為準）。 |
| `configurableAggregation.aggregationKey` | - | 可讓您根據下列描述引數，彙總對應至目的地的匯出設定檔。 |
| `configurableAggregation.aggregationKey.includeSegmentId` | 布林值 | 將此引數設為 `true` 如果您想要依受眾ID將匯出至目的地的設定檔分組。 |
| `configurableAggregation.aggregationKey.includeSegmentStatus` | 布林值 | 同時設定此引數和 `includeSegmentId` 至 `true`，如果您想要依受眾ID和受眾狀態，將匯出至目的地的設定檔分組。 |
| `configurableAggregation.aggregationKey.includeIdentity` | 布林值 | 將此引數設為 `true` 如果您想要依身分名稱空間將匯出至目的地的設定檔分組。 |
| `configurableAggregation.aggregationKey.oneIdentityPerGroup` | 布林值 | 將此引數設為 `true` 如果您希望匯出的設定檔根據單一身分歸入群組（GAID、IDFA、電話號碼、電子郵件等）。 |
| `configurableAggregation.aggregationKey.groups` | 陣列 | 如果您想要依身分名稱空間群組將匯出至目的地的設定檔分組，請建立身分群組清單。 例如，您可以使用上述範例中的設定，將包含IDFA和GAID行動識別碼的設定檔合併為對目的地的一次呼叫，並將電子郵件合併為另一個呼叫。 |

{style="table-layout:auto"}

## 後續步驟 {#next-steps}

閱讀本文後，您應該更瞭解如何為目的地設定彙總原則。

若要深入瞭解其他目的地元件，請參閱下列文章：

* [客戶驗證設定](customer-authentication.md)
* [OAuth2驗證](oauth2-authentication.md)
* [客戶資料欄位](customer-data-fields.md)
* [UI屬性](ui-attributes.md)
* [綱要設定](schema-configuration.md)
* [身分名稱空間設定](identity-namespace-configuration.md)
* [支援的對應設定](supported-mapping-configurations.md)
* [目的地傳遞](destination-delivery.md)
* [對象中繼資料設定](audience-metadata-configuration.md)
* [批次設定](batch-configuration.md)
* [歷史設定檔資格](historical-profile-qualifications.md)
