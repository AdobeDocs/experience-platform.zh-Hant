---
description: 瞭解如何為使用Destination SDK構建的目標配置目標交付設定，以指示導出的資料所在位置以及資料所在位置使用何種身份驗證規則。
title: 目標傳遞
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 1%

---


# 目標傳遞

要對導出到目標地帶的資料的位置提供更多控制，Destination SDK允許您指定目標傳遞設定。

目標傳遞部分指示導出的資料所在位置以及資料所到達位置使用的驗證規則。

<!-- When configuring a destination, you must specify an authentication rule and one or more `destinationServerId` parameters, corresponding to the destination servers that define where the data will be delivered to. In most cases, the authentication rule that you should use is `CUSTOMER_AUTHENTICATION`.  -->

要瞭解此元件在與Destination SDK建立的整合中的位置，請參閱 [配置選項](../configuration-options.md) 文檔，或參閱以下目標配置概述頁：

* [使用Destination SDK配置流目標](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [使用Destination SDK配置基於檔案的目標](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

您可以通過 `/authoring/destinations` 端點。 有關詳細的API調用示例，請參閱以下API參考頁，在這些示例中可以配置此頁中顯示的元件。

* [建立目標配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目標配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文介紹可用於目標的所有受支援的目標傳遞選項。

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

在配置目標傳遞設定時，可以使用下表中描述的參數來定義導出資料的發送位置。

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `authenticationRule` | 字串 | 指示如何 [!DNL Platform] 應該連接到目標。 支援的值：<ul><li>`CUSTOMER_AUTHENTICATION`:如果平台客戶通過所述的任何驗證方法登錄到您的系統，請使用此選項 [這裡](customer-authentication.md)。</li><li>`PLATFORM_AUTHENTICATION`:如果Adobe與目標之間存在全局身份驗證系統，則使用此選項 [!DNL Platform] 客戶不需要提供任何身份驗證憑據來連接到目標。 在這種情況下，必須使用 [憑據API](../../credentials-api/create-credential-configuration.md) 配置。 </li><li>`NONE`:如果向目標平台發送資料不需要身份驗證，則使用此選項。 </li></ul> |
| `destinationServerId` | 字串 | 的 `instanceId` 的 [目標伺服器](../../authoring-api/destination-server/create-destination-server.md) 將資料導出到。 |
| `deliveryMatchers.type` | 字串 | <ul><li>在為基於檔案的目標配置目標傳遞時，始終將其設定為 `SOURCE`。</li><li>為流目標配置目標傳遞時， `deliveryMatchers` 不需要。</li></ul> |
| `deliveryMatchers.value` | 字串 | <ul><li>在為基於檔案的目標配置目標傳遞時，始終將其設定為 `batch`。</li><li>為流目標配置目標傳遞時， `deliveryMatchers` 不需要。</li></ul> |

{style="table-layout:auto"}

## 流目標的目標傳遞設定 {#destination-delivery-streaming}

以下示例說明如何為流式傳輸目標配置目標傳遞設定。 請注意 `deliveryMatchers` 流目標不需要節。

>[!BEGINSHADEBOX]

```json
{
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

>[!ENDSHADEBOX]

## 基於檔案的目標的目標傳遞設定 {#destination-delivery-file-based}

以下示例說明如何為基於檔案的目標配置目標傳遞設定。 請注意 `deliveryMatchers` 基於檔案的目標需要節。

>[!BEGINSHADEBOX]

```json
{
   "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

>[!ENDSHADEBOX]

## 後續步驟 {#next-steps}

閱讀本文後，您應更好地瞭解如何配置目標導出資料的位置，以用於流和基於檔案的目標。

要瞭解有關其他目標元件的詳細資訊，請參閱以下文章：

* [客戶驗證](customer-authentication.md)
* [OAuth2身份驗證](oauth2-authentication.md)
* [UI屬性](ui-attributes.md)
* [客戶資料欄位](customer-data-fields.md)
* [架構配置](schema-configuration.md)
* [標識命名空間配置](identity-namespace-configuration.md)
* [支援的映射配置](supported-mapping-configurations.md)
* [受眾元資料配置](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [批配置](batch-configuration.md)
* [歷史配置檔案資格](historical-profile-qualifications.md)