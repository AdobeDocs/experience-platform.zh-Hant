---
description: 了解如何為使用Destination SDK建置的目的地配置對象中繼資料設定。
title: 對象中繼資料設定
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 2%

---


# 對象中繼資料設定

從Experience Platform匯出資料至目的地時，您可能需要特定的對象中繼資料，例如區段名稱或區段ID，才能在Experience Platform與目的地之間共用。

Destination SDK提供工具，可供您以程式設計方式建立、更新或刪除目的地平台中的對象。

若要了解此元件在透過Destination SDK建立的整合中的插入位置，請參閱 [配置選項](../configuration-options.md) 檔案，或參閱如何 [使用Destination SDK來設定串流目的地](../../guides/configure-destination-instructions.md#create-destination-configuration).

您可以透過 `/authoring/audience-templates` 端點。 建立對象中繼資料設定後，您可以使用 `/authoring/destinations` 要配置的端點 `audienceMetadataConfig` 區段。 本區段會告訴您的目的地應對應至對象範本的區段中繼資料。

如需詳細API呼叫範例，請參閱下列API參考頁面，您可在其中設定本頁面所示的元件。

* [建立目標配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目標配置](../../authoring-api/destination-configuration/update-destination-configuration.md)
* [建立受眾範本](../../metadata-api/create-audience-template.md)
* [更新對象範本](../../metadata-api/update-audience-template.md)

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名稱和值均為 **區分大小寫**. 為避免區分大小寫錯誤，請使用參數名稱和值，如說明檔案所示。

## 支援的整合類型 {#supported-integration-types}

如需詳細資訊，請參閱下表以了解哪些類型的整合支援本頁面所述的功能。

| 整合類型 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 是 |

## 支援的參數 {#supported-parameters}

建立對象中繼資料設定時，您可以使用下表所述的參數來設定區段對應設定。

```json
  "audienceMetadataConfig":{
   "mapExperiencePlatformSegmentName":false,
   "mapExperiencePlatformSegmentId":false,
   "mapUserInput":false,
   "audienceTemplateId":"YOUR_AUDIENCE_TEMPLATE_ID"
}
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `mapExperiencePlatformSegmentName` | 布林值 | 指出 [[!UICONTROL 對應ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) 目標啟動工作流程中的值應為Experience Platform區段名稱。 |
| `mapExperiencePlatformSegmentId` | 布林值 | 指出 [[!UICONTROL 對應ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) 目標啟動工作流程中的值應為Experience Platform區段ID。 |
| `mapUserInput` | 布林值 | 啟用或停用 [[!UICONTROL 對應ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) 值。 若設為 `true`, `audienceTemplateId` 不能存在。 |
| `audienceTemplateId` | 布林值 | 此 `instanceId` 的 [對象中繼資料範本](../../metadata-api/create-audience-template.md) 用於目的地。 |

{style="table-layout:auto"}

## 後續步驟 {#next-steps}

閱讀本文後，您應該更清楚了解如何設定目的地的對象中繼資料。

若要進一步了解其他目的地元件，請參閱下列文章：

* [客戶驗證配置](customer-authentication.md)
* [OAuth2驗證](oauth2-authentication.md)
* [客戶資料欄位](customer-data-fields.md)
* [UI屬性](ui-attributes.md)
* [結構配置](schema-configuration.md)
* [身分命名空間設定](identity-namespace-configuration.md)
* [支援的對應配置](supported-mapping-configurations.md)
* [目的地傳送](destination-delivery.md)
* [聚合策略](aggregation-policy.md)
* [批次設定](batch-configuration.md)
* [歷史設定檔資格](historical-profile-qualifications.md)