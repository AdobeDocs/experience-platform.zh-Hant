---
description: 瞭解如何為使用Destination SDK建立的目的地設定對象中繼資料設定。
title: 對象中繼資料設定
exl-id: ae71df4f-b753-4084-835f-03559b4986cb
source-git-commit: 20cb2dbfbfc8e73c765073818c8e7e561d4e6629
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 3%

---

# 對象中繼資料設定

將資料從Experience Platform匯出至目的地時，您可能需要在Experience Platform和目的地之間共用特定的對象中繼資料，例如對象名稱或對象ID。

Destination SDK提供的工具，可用於以程式設計方式建立、更新或刪除目的地平台中的對象。

若要瞭解此元件在何處適合使用Destination SDK建立的整合，請參閱[設定選項](../configuration-options.md)檔案中的圖表，或參閱如何[使用Destination SDK設定串流目的地](../../guides/configure-destination-instructions.md#create-destination-configuration)的指南。

您可以透過`/authoring/audience-templates`端點設定對象中繼資料範本。 建立您的對象中繼資料設定後，您可以使用`/authoring/destinations`端點來設定`audienceMetadataConfig`區段。 本節將說明目的地應將哪些對象中繼資料對應至您的對象範本。

請參閱下列API參考頁面，以取得詳細的API呼叫範例，您可在此範例設定本頁面中顯示的元件。

* [建立目的地設定](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目的地設定](../../authoring-api/destination-configuration/update-destination-configuration.md)
* [建立對象範本](../../metadata-api/create-audience-template.md)
* [更新對象範本](../../metadata-api/update-audience-template.md)

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值都區分大小寫&#x200B;****。 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 支援的整合型別 {#supported-integration-types}

如需瞭解哪些型別的整合支援本頁面所述功能的詳細資訊，請參閱下表。

| 整合型別 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 是 |

## 支援的引數 {#supported-parameters}

建立對象中繼資料設定時，您可以使用下表所述的引數來設定對象對應設定。

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
| `mapExperiencePlatformSegmentName` | 布林值 | 指出目的地啟用工作流程中的[[!UICONTROL 對應ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling)值是否應為Experience Platform對象名稱。 |
| `mapExperiencePlatformSegmentId` | 布林值 | 指出目的地啟用工作流程中的[[!UICONTROL 對應ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling)值是否應為Experience Platform的受眾識別碼。 |
| `mapUserInput` | 布林值 | 啟用或停用目的地啟用工作流程中[[!UICONTROL 對應ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling)值的使用者輸入。 若設為`true`，則無法顯示`audienceTemplateId`。 |
| `audienceTemplateId` | 字串 | [對象中繼資料範本](../../metadata-api/create-audience-template.md)的`instanceId`用於您的目的地。 |

{style="table-layout:auto"}

## 後續步驟 {#next-steps}

閱讀本文後，您應該更加瞭解如何為目的地設定對象中繼資料。

若要深入瞭解其他目的地元件，請參閱下列文章：

* [客戶驗證設定](customer-authentication.md)
* [OAuth2授權](oauth2-authorization.md)
* [客戶資料欄位](customer-data-fields.md)
* [UI屬性](ui-attributes.md)
* [綱要設定](schema-configuration.md)
* [身分名稱空間設定](identity-namespace-configuration.md)
* [支援的對應設定](supported-mapping-configurations.md)
* [目的地傳遞](destination-delivery.md)
* [彙總原則](aggregation-policy.md)
* [批次設定](batch-configuration.md)
* [歷史設定檔資格](historical-profile-qualifications.md)
