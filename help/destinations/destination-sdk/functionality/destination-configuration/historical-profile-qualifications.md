---
description: 瞭解使用Destination SDK建立的目的地支援的歷史設定檔資格。
title: 歷史設定檔資格
exl-id: 8880cff9-865b-4d45-a24d-a78e77419670
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 2%

---

# 歷史設定檔資格

依預設，透過Destination SDK建立的所有目的地都支援歷史設定檔資格。 這表示當使用者首次設定啟動資料流至您的目的地時，第一次匯出會包含符合該區段資格的受眾所有成員。

此行為是由目的地組態中的`"backfillHistoricalProfileData":true`引數所定義。

>[!IMPORTANT]
>
>已針對透過Destination SDK建立的所有目的地啟用歷史設定檔資格，且使用者無法設定`backfillHistoricalProfileData`引數。

## 支援的整合型別 {#supported-integration-types}

如需瞭解哪些型別的整合支援本頁面所述功能的詳細資訊，請參閱下表。

| 整合型別 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 是 |



<!-- 
|Parameter | Type | Description|
|---------|----------|------|
|`backfillHistoricalProfileData` | Boolean | Controls whether historical profile data is exported when audiences are activated to the destination. <br> <ul><li> `true`: [!DNL Experience Platform] sends the historical user profiles that qualified for the audience before the audience is activated. </li><li> `false`: [!DNL Experience Platform] only includes user profiles that qualify for the audience after the audience is activated. </li></ul> |

{style="table-layout:auto"} -->


## 後續步驟 {#next-steps}

閱讀本文後，您應該知道，Experience Platform會在對象首次匯出至目的地時，自動匯出曾符合啟用對象資格的所有設定檔歷史母體。 此選項無法在Destination SDK或Experience Platform UI中設定。

若要深入瞭解其他目的地元件，請參閱下列文章：

* [客戶驗證](customer-authentication.md)
* [OAuth2授權](oauth2-authorization.md)
* [客戶資料欄位](customer-data-fields.md)
* [UI屬性](ui-attributes.md)
* [結構描述設定](schema-configuration.md)
* [身分名稱空間設定](identity-namespace-configuration.md)
* [支援的對應設定](supported-mapping-configurations.md)
* [目的地傳遞](destination-delivery.md)
* [對象中繼資料設定](audience-metadata-configuration.md)
* [彙總原則](aggregation-policy.md)
* [批次設定](batch-configuration.md)
