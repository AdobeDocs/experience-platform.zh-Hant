---
description: 瞭解如何設定聚合策略以確定對目標的HTTP請求應如何分組和批處理。
title: 聚合策略
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '996'
ht-degree: 2%

---


# 聚合策略

為確保將資料導出到API端點時達到最高效率，您可以使用各種設定將導出的配置檔案聚合到更大或更小的批中，按身份和其他使用情形對它們進行分組。 這還允許您定制資料導出到API端點上的任何下游限制（速率限制、每個API調用的標識數等）。

使用可配置的聚合深入到Destination SDK提供的設定中，或使用盡力聚合告訴Destination SDK盡可能地對API調用進行批處理。

在構建帶Destination SDK的即時（流）目標時，可以配置導出的配置檔案在生成的導出中如何組合。 此行為由聚合策略設定決定。

要瞭解此元件在與Destination SDK建立的整合中的位置，請參閱 [配置選項](../configuration-options.md) 文檔，或參閱有關如何 [使用Destination SDK配置流目標](../../guides/configure-destination-instructions.md#create-destination-configuration)。

您可以通過 `/authoring/destinations` 端點。 有關詳細的API調用示例，請參閱以下API參考頁，在這些示例中可以配置此頁中顯示的元件。

* [建立目標配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目標配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文介紹可用於目標的所有支援的聚合策略設定。

閱讀完本文檔後，請參閱 [使用模板](../../functionality/destination-server/message-format.md#using-templating) 和 [聚合鍵示例](../../functionality/destination-server/message-format.md#template-aggregation-key) 瞭解如何根據所選聚合策略將聚合策略包含在消息轉換模板中。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名和值均 **區分大小寫**。 為避免區分大小寫錯誤，請完全按文檔所示使用參數名稱和值。

## 支援的整合類型 {#supported-integration-types}

有關哪些類型的整合支援本頁所述功能的詳細資訊，請參閱下表。

| 整合類型 | 支援功能 |
|---|---|
| 即時（流）整合 | 是 |
| 基於檔案（批處理）的整合 | 無 |

## 盡力聚合 {#best-effort-aggregation}

盡力聚合最適合於每個請求更喜歡較少配置檔案的目標，而更願意接收更多資料較少的請求，而不是更少資料較多的請求。

下面的示例配置顯示了盡力的聚合配置。 有關可配置聚合的示例，請參見 [可配置聚合](#configurable-aggregation) 的子菜單。 下表列出了適用於最佳工作聚合的參數。

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
| `bestEffortAggregation.maxUsersPerRequest` | 整數 | Experience Platform可以在單個HTTP調用中聚合多個導出的配置檔案。 <br><br>此值指示終結點在單個HTTP調用中應接收的最大配置檔案數。 請注意，這是一種盡力的聚合。 例如，如果指定值100，平台可能會在呼叫時發送小於100的任意數量的配置檔案。 <br><br> 如果伺服器不接受每個請求多個用戶，請將此值設定為 `1`。 |
| `bestEffortAggregation.splitUserById` | 布林值 | 如果應按標識拆分到目標的調用，則使用此標誌。 將此標誌設定為 `true` 如果伺服器每次調用只接受一個標識，則指定的標識名稱空間為。 |

{style="table-layout:auto"}

>[!TIP]
>
>如果API終結點每個API調用接受的配置檔案少於100個，則使用盡力聚合。

## 可配置聚合 {#configurable-aggregation}

如果您更願意大批處理同一呼叫上的數千個配置檔案，則可配置的聚合效果最好。 此選項還允許您基於複雜的聚合規則聚合導出的配置檔案。

下面的示例配置顯示了可配置的聚合配置。 有關盡力匯總的示例，請參見 [最佳工作聚合](#best-effort-aggregation) 的子菜單。 下表列出了適用於可配置聚合的參數。

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
| `configurableAggregation.splitUserById` | 布林值 | 如果應按標識拆分到目標的調用，則使用此標誌。 將此標誌設定為 `true` 如果伺服器每次調用只接受一個標識，則指定的標識名稱空間為。 |
| `configurableAggregation.maxBatchAgeInSecs` | 整數 | 用於與 `maxNumEventsInBatch`，此參數確定Experience Platform應等待多長時間，直到將API調用發送到您的終結點。 <ul><li>最小值（秒）:1800</li><li>最大值（秒）:3600</li></ul> 例如，如果對這兩個參數都使用最大值，Experience Platform將等待3600秒或直到有10000個限定配置檔案才進行API調用（以先發生的情況為準）。 |
| `configurableAggregation.maxNumEventsInBatch` | 整數 | 與 `maxBatchAgeInSecs`，此參數確定在API調用中應聚合多少個合格配置檔案。 <ul><li>最小值：1000</li><li>最大值：10000</li></ul> 例如，如果對這兩個參數都使用最大值，Experience Platform將等待3600秒或直到有10000個限定配置檔案才進行API調用（以先發生的情況為準）。 |
| `configurableAggregation.aggregationKey` | - | 允許您根據下面描述的參數聚合映射到目標的導出配置檔案。 |
| `configurableAggregation.aggregationKey.includeSegmentId` | 布林值 | 將此參數設定為 `true` 按段ID對導出到目標的配置檔案進行分組。 |
| `configurableAggregation.aggregationKey.includeSegmentStatus` | 布林值 | 設定此參數和 `includeSegmentId` 至 `true`，如果要按段ID和段狀態將導出到目標的配置檔案分組。 |
| `configurableAggregation.aggregationKey.includeIdentity` | 布林值 | 將此參數設定為 `true` 按標識名稱空間將導出到目標的配置檔案分組。 |
| `configurableAggregation.aggregationKey.oneIdentityPerGroup` | 布林值 | 將此參數設定為 `true` 如果希望將導出的配置檔案根據單個身份（GAID、IDFA、電話號碼、電子郵件等）聚合到組中。 |
| `configurableAggregation.aggregationKey.groups` | 陣列 | 如果要按標識命名空間的組將導出到目標的配置檔案分組，請建立標識組清單。 例如，您可以使用上例中所示的配置將包含IDFA和GAID移動標識符的配置檔案合併為到目標的一個呼叫和電子郵件，再將電子郵件合併為另一個。 |

{style="table-layout:auto"}

## 後續步驟 {#next-steps}

閱讀這篇文章後，您應更好地瞭解如何為目標配置聚合策略。

要瞭解有關其他目標元件的詳細資訊，請參閱以下文章：

* [客戶身份驗證配置](customer-authentication.md)
* [OAuth2身份驗證](oauth2-authentication.md)
* [客戶資料欄位](customer-data-fields.md)
* [UI屬性](ui-attributes.md)
* [架構配置](schema-configuration.md)
* [標識命名空間配置](identity-namespace-configuration.md)
* [支援的映射配置](supported-mapping-configurations.md)
* [目標傳遞](destination-delivery.md)
* [受眾元資料配置](audience-metadata-configuration.md)
* [批配置](batch-configuration.md)
* [歷史配置檔案資格](historical-profile-qualifications.md)