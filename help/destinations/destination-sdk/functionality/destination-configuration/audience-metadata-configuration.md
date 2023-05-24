---
description: 瞭解如何為使用Destination SDK構建的目標配置訪問群體元資料設定。
title: 受眾元資料配置
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 2%

---


# 受眾元資料配置

將資料從Experience Platform導出到目標時，可能需要特定的受眾元資料（如段名稱或段ID）在Experience Platform與目標之間共用。

Destination SDK提供了一些工具，您可以使用這些工具以寫程式方式在目標平台中建立、更新或刪除受眾。

要瞭解此元件在與Destination SDK建立的整合中的位置，請參閱 [配置選項](../configuration-options.md) 文檔，或參閱有關如何 [使用Destination SDK配置流目標](../../guides/configure-destination-instructions.md#create-destination-configuration)。

您可以通過 `/authoring/audience-templates` 端點。 建立受眾元資料配置後，可以使用 `/authoring/destinations` 要配置的終結點 `audienceMetadataConfig` 的子菜單。 本部分將告訴您的目標元資料應映射到您的受眾模板。

有關詳細的API調用示例，請參閱以下API參考頁，在這些示例中可以配置此頁中顯示的元件。

* [建立目標配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目標配置](../../authoring-api/destination-configuration/update-destination-configuration.md)
* [建立受眾模板](../../metadata-api/create-audience-template.md)
* [更新受眾模板](../../metadata-api/update-audience-template.md)

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名和值均 **區分大小寫**。 為避免區分大小寫錯誤，請完全按文檔所示使用參數名稱和值。

## 支援的整合類型 {#supported-integration-types}

有關哪些類型的整合支援本頁所述功能的詳細資訊，請參閱下表。

| 整合類型 | 支援功能 |
|---|---|
| 即時（流）整合 | 是 |
| 基於檔案（批處理）的整合 | 是 |

## 支援的參數 {#supported-parameters}

建立受眾元資料配置時，可以使用下表中描述的參數配置段映射設定。

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
| `mapExperiencePlatformSegmentName` | 布林值 | 指示 [[!UICONTROL 映射ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) 目標激活工作流中的值應為Experience Platform段名稱。 |
| `mapExperiencePlatformSegmentId` | 布林值 | 指示 [[!UICONTROL 映射ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) 目標激活工作流中的值應為Experience Platform段ID。 |
| `mapUserInput` | 布林值 | 啟用或禁用 [[!UICONTROL 映射ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) 目標激活工作流中的值。 如果設定為 `true`。 `audienceTemplateId` 不能存在。 |
| `audienceTemplateId` | 布林值 | 的 `instanceId` 的 [受眾元資料模板](../../metadata-api/create-audience-template.md) 用於你的目的地。 |

{style="table-layout:auto"}

## 後續步驟 {#next-steps}

閱讀本文後，您應更好地瞭解如何為目標配置受眾元資料。

要瞭解有關其他目標元件的詳細資訊，請參閱以下文章：

* [客戶身份驗證配置](customer-authentication.md)
* [OAuth2身份驗證](oauth2-authentication.md)
* [客戶資料欄位](customer-data-fields.md)
* [UI屬性](ui-attributes.md)
* [架構配置](schema-configuration.md)
* [標識命名空間配置](identity-namespace-configuration.md)
* [支援的映射配置](supported-mapping-configurations.md)
* [目標傳遞](destination-delivery.md)
* [聚合策略](aggregation-policy.md)
* [批配置](batch-configuration.md)
* [歷史配置檔案資格](historical-profile-qualifications.md)