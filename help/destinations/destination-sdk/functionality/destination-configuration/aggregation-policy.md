---
description: 了解如何設定匯總原則，以決定對您目的地的HTTP請求進行分組和批次處理的方式。
title: 聚合策略
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 2%

---


# 聚合策略

若要確保將資料匯出至API端點時能有最高效率，您可以使用各種設定，將匯出的設定檔匯總為較大或較小的批次、依身分和其他使用案例加以分組。 這也可讓您量身打造資料匯出，使其符合API端點的任何下游限制（速率限制、每個API呼叫的身分數量等）。

使用可設定的匯總功能深入探討Destination SDK提供的設定，或使用最佳的匯總功能告知Destination SDK盡可能將API呼叫分批。

使用Destination SDK建立即時（串流）目的地時，您可以設定匯出的設定檔應如何結合到產生的匯出中。 此行為由聚合策略設定確定。

若要了解此元件在透過Destination SDK建立的整合中的插入位置，請參閱 [配置選項](../configuration-options.md) 檔案，或參閱如何 [使用Destination SDK來設定串流目的地](../../guides/configure-destination-instructions.md#create-destination-configuration).

您可以通過 `/authoring/destinations` 端點。 如需詳細API呼叫範例，請參閱下列API參考頁面，您可在其中設定本頁面所示的元件。

* [建立目標配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目標配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文介紹可用於目標的所有支援的聚合策略設定。

閱讀本檔案後，請參閱 [使用模板](../../functionality/destination-server/message-format.md#using-templating) 和 [聚合鍵示例](../../functionality/destination-server/message-format.md#template-aggregation-key) 了解如何根據所選聚合策略將聚合策略包含在消息轉換模板中。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名稱和值均為 **區分大小寫**. 為避免區分大小寫錯誤，請使用參數名稱和值，如說明檔案所示。

## 支援的整合類型 {#supported-integration-types}

如需詳細資訊，請參閱下表以了解哪些類型的整合支援本頁面所述的功能。

| 整合類型 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 無 |

## 最佳成果匯總 {#best-effort-aggregation}

「最佳工作匯總」最適合每個請求偏好較少設定檔的目的地，而且寧可接收資料較少的請求，也不願接收資料較少的請求。

以下示例配置顯示了最佳的聚合配置。 有關可配置聚合的示例，請參見 [可配置聚合](#configurable-aggregation) 區段。 下表記錄了適用於最佳工作匯總的參數。

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
| `aggregationType` | 字串 | 指示目標應使用的聚合策略的類型。 支援的聚合類型： <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `bestEffortAggregation.maxUsersPerRequest` | 整數 | Experience Platform可以在單一HTTP呼叫中匯總多個匯出的設定檔。 <br><br>此值表示端點在單一HTTP呼叫中應接收的設定檔數目上限。 請注意，這是最佳的匯總方式。 例如，如果您指定值100,Platform可能會在呼叫中傳送小於100的任何設定檔數量。 <br><br> 如果您的伺服器不接受每個請求的多個使用者，請將此值設為 `1`. |
| `bestEffortAggregation.splitUserById` | 布林值 | 如果目標的呼叫應依身分分割，請使用此標幟。 將此標幟設為 `true` 如果您的伺服器在每次呼叫中僅接受一個身分識別，則會接受指定的身分命名空間。 |

{style="table-layout:auto"}

>[!TIP]
>
>如果您的API端點接受的每個API呼叫少於100個設定檔，請盡量匯總。

## 可配置聚合 {#configurable-aggregation}

如果您偏好以大批次執行，且同一呼叫上有數千個設定檔，可設定的匯總最能運作。 此選項也可讓您根據複雜的匯總規則匯總匯出的設定檔。

下面的示例配置顯示了可配置的聚合配置。 如需最佳努力匯總的範例，請參閱 [最佳成果匯總](#best-effort-aggregation) 區段。 下表介紹了適用於可配置聚合的參數。

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
| `aggregationType` | 字串 | 指示目標應使用的聚合策略的類型。 支援的聚合類型： <ul><li>`BEST_EFFORT`</li><li>`CONFIGURABLE_AGGREGATION`</li></ul> |
| `configurableAggregation.splitUserById` | 布林值 | 如果目標的呼叫應依身分分割，請使用此標幟。 將此標幟設為 `true` 如果您的伺服器在每次呼叫中僅接受一個身分識別，則會接受指定的身分命名空間。 |
| `configurableAggregation.maxBatchAgeInSecs` | 整數 | 用於與 `maxNumEventsInBatch`，此參數會決定Experience Platform應等待多久，直到傳送API呼叫至您的端點。 <ul><li>最小值（秒）:1800</li><li>最大值（秒）:3600</li></ul> 例如，如果您對這兩個參數使用最大值，Experience Platform會等待3600秒或直到有10000個合格設定檔才進行API呼叫（以先發生者為準）。 |
| `configurableAggregation.maxNumEventsInBatch` | 整數 | 與 `maxBatchAgeInSecs`，此參數會決定API呼叫中應匯總多少個合格設定檔。 <ul><li>最小值：1000</li><li>最大值：10000</li></ul> 例如，如果您對這兩個參數使用最大值，Experience Platform會等待3600秒或直到有10000個合格設定檔才進行API呼叫（以先發生者為準）。 |
| `configurableAggregation.aggregationKey` | - | 可讓您根據下列參數，匯總對應至目的地的匯出設定檔。 |
| `configurableAggregation.aggregationKey.includeSegmentId` | 布林值 | 將此參數設為 `true` 如果您想要依區段ID將匯出至目的地的設定檔分組。 |
| `configurableAggregation.aggregationKey.includeSegmentStatus` | 布林值 | 同時設定此參數和 `includeSegmentId` to `true`，如果您想要依區段ID和區段狀態將匯出至目的地的設定檔分組。 |
| `configurableAggregation.aggregationKey.includeIdentity` | 布林值 | 將此參數設為 `true` 如果您想要依身分命名空間將匯出至目的地的設定檔分組。 |
| `configurableAggregation.aggregationKey.oneIdentityPerGroup` | 布林值 | 將此參數設定為 `true` 如果您希望匯出的設定檔能根據單一身分（GAID、IDFA、電話號碼、電子郵件等）匯總至群組。 |
| `configurableAggregation.aggregationKey.groups` | 陣列 | 如果您想要依身分識別命名空間的群組，將匯出至目的地的設定檔分組，請建立身分群組清單。 例如，您可以使用上述範例中的設定，將包含IDFA和GAID行動識別碼的設定檔，合併至對您目的地的呼叫和電子郵件中。 |

{style="table-layout:auto"}

## 後續步驟 {#next-steps}

閱讀本文後，您應該更了解如何為目標配置聚合策略。

若要進一步了解其他目的地元件，請參閱下列文章：

* [客戶驗證配置](customer-authentication.md)
* [OAuth2驗證](oauth2-authentication.md)
* [客戶資料欄位](customer-data-fields.md)
* [UI屬性](ui-attributes.md)
* [結構配置](schema-configuration.md)
* [身分命名空間設定](identity-namespace-configuration.md)
* [支援的對應配置](supported-mapping-configurations.md)
* [目的地傳送](destination-delivery.md)
* [對象中繼資料設定](audience-metadata-configuration.md)
* [批次設定](batch-configuration.md)
* [歷史設定檔資格](historical-profile-qualifications.md)