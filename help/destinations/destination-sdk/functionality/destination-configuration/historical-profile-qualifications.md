---
description: 了解透過Destination SDK建置的目的地所支援的歷史設定檔資格。
title: 歷史設定檔資格
source-git-commit: 65a658208b48a50184e55a6d64cdf7ad6de0f04f
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 1%

---


# 歷史設定檔資格

依預設，所有透過Destination SDK建立的目的地都支援歷史設定檔資格。 這表示，當使用者首次設定啟動資料流至您的目的地時，第一次匯出會包含曾符合該區段資格的區段所有成員。

此行為由 `"backfillHistoricalProfileData":true` 參數。

>[!IMPORTANT]
>
>所有透過Destination SDK建立的目的地，都會啟用歷史設定檔資格，並 `backfillHistoricalProfileData` 參數不能由用戶配置。

## 支援的整合類型 {#supported-integration-types}

如需詳細資訊，請參閱下表以了解哪些類型的整合支援本頁面所述的功能。

| 整合類型 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 是 |



<!-- 
|Parameter | Type | Description|
|---------|----------|------|
|`backfillHistoricalProfileData` | Boolean | Controls whether historical profile data is exported when segments are activated to the destination. <br> <ul><li> `true`: [!DNL Platform] sends the historical user profiles that qualified for the segment before the segment is activated. </li><li> `false`: [!DNL Platform] only includes user profiles that qualify for the segment after the segment is activated. </li></ul> |

{style="table-layout:auto"} -->


## 後續步驟 {#next-steps}

閱讀本文後，您應知道，當區段首次匯出至目的地時，Experience Platform會自動匯出所有曾符合啟動區段資格的設定檔的歷史母體。 無法在Destination SDK或Experience PlatformUI中設定此選項。

若要進一步了解其他目的地元件，請參閱下列文章：

* [客戶驗證](customer-authentication.md)
* [OAuth2驗證](oauth2-authentication.md)
* [客戶資料欄位](customer-data-fields.md)
* [UI屬性](ui-attributes.md)
* [結構配置](schema-configuration.md)
* [身分命名空間設定](identity-namespace-configuration.md)
* [支援的對應配置](supported-mapping-configurations.md)
* [目的地傳送](destination-delivery.md)
* [對象中繼資料設定](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [批次設定](batch-configuration.md)