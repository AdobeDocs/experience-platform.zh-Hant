---
description: 瞭解使用Destination SDK構建的目標支援的歷史配置檔案資格。
title: 歷史配置檔案資格
source-git-commit: 65a658208b48a50184e55a6d64cdf7ad6de0f04f
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 1%

---


# 歷史配置檔案資格

預設情況下，通過Destination SDK建立的所有目標都支援歷史配置檔案資格。 這意味著當用戶首次將激活資料流設定到目標時，第一次導出將包含該段中曾經限定的所有成員。

此行為由 `"backfillHistoricalProfileData":true` 目標配置中的參數。

>[!IMPORTANT]
>
>為通過Destination SDK和 `backfillHistoricalProfileData` 參數不可用戶配置。

## 支援的整合類型 {#supported-integration-types}

有關哪些類型的整合支援本頁所述功能的詳細資訊，請參閱下表。

| 整合類型 | 支援功能 |
|---|---|
| 即時（流）整合 | 是 |
| 基於檔案（批處理）的整合 | 是 |



<!-- 
|Parameter | Type | Description|
|---------|----------|------|
|`backfillHistoricalProfileData` | Boolean | Controls whether historical profile data is exported when segments are activated to the destination. <br> <ul><li> `true`: [!DNL Platform] sends the historical user profiles that qualified for the segment before the segment is activated. </li><li> `false`: [!DNL Platform] only includes user profiles that qualify for the segment after the segment is activated. </li></ul> |

{style="table-layout:auto"} -->


## 後續步驟 {#next-steps}

在閱讀本文之後，您應該知道，當段首次導出到目標時，Experience Platform會自動導出所有符合激活段條件的配置檔案的歷史總體。 在Destination SDK或Experience PlatformUI中不能配置此選項。

要瞭解有關其他目標元件的詳細資訊，請參閱以下文章：

* [客戶驗證](customer-authentication.md)
* [OAuth2身份驗證](oauth2-authentication.md)
* [客戶資料欄位](customer-data-fields.md)
* [UI屬性](ui-attributes.md)
* [架構配置](schema-configuration.md)
* [標識命名空間配置](identity-namespace-configuration.md)
* [支援的映射配置](supported-mapping-configurations.md)
* [目標傳遞](destination-delivery.md)
* [受眾元資料配置](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [批配置](batch-configuration.md)