---
description: 了解如何為使用Destination SDK建置的目的地設定目的地傳送設定，以指出匯出的資料所在位置，以及資料所在位置使用的驗證規則。
title: 目的地傳送
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 1%

---


# 目的地傳送

若要進一步控制匯出至目的地的資料所在位置，Destination SDK可讓您指定目的地傳送設定。

目的地傳送區段會指出匯出的資料所在位置，以及資料著陸位置中使用的驗證規則。

<!-- When configuring a destination, you must specify an authentication rule and one or more `destinationServerId` parameters, corresponding to the destination servers that define where the data will be delivered to. In most cases, the authentication rule that you should use is `CUSTOMER_AUTHENTICATION`.  -->

若要了解此元件在透過Destination SDK建立的整合中的插入位置，請參閱 [配置選項](../configuration-options.md) 檔案或請參閱下列目的地組態概觀頁面：

* [使用Destination SDK來設定串流目的地](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [使用Destination SDK配置基於檔案的目標](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

您可以透過 `/authoring/destinations` 端點。 如需詳細API呼叫範例，請參閱下列API參考頁面，您可在其中設定本頁面所示的元件。

* [建立目標配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目標配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文說明可用於目的地的所有支援目的地傳送選項。

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

設定目的地傳送設定時，您可以使用下表所述的參數來定義匯出資料的傳送位置。

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `authenticationRule` | 字串 | 指示方式 [!DNL Platform] 應該連線到您的目的地。 支援的值：<ul><li>`CUSTOMER_AUTHENTICATION`:如果Platform客戶透過上述任何驗證方法登入您的系統，請使用此選項 [此處](customer-authentication.md).</li><li>`PLATFORM_AUTHENTICATION`:如果Adobe與目的地之間有全域驗證系統，且 [!DNL Platform] 客戶不需要提供任何驗證憑證來連線至您的目的地。 在此情況下，您必須使用 [認證API](../../credentials-api/create-credential-configuration.md) 設定。 </li><li>`NONE`:如果不需要驗證即可將資料傳送至目的地平台，請使用此選項。 </li></ul> |
| `destinationServerId` | 字串 | 此 `instanceId` 的 [目的地伺服器](../../authoring-api/destination-server/create-destination-server.md) 將資料匯出至的區段。 |
| `deliveryMatchers.type` | 字串 | <ul><li>為檔案型目的地設定目的地傳送時，請一律將此設為 `SOURCE`.</li><li>為串流目的地設定目的地傳送時， `deliveryMatchers` 區段並非必要項目。</li></ul> |
| `deliveryMatchers.value` | 字串 | <ul><li>為檔案型目的地設定目的地傳送時，請一律將此設為 `batch`.</li><li>為串流目的地設定目的地傳送時， `deliveryMatchers` 區段並非必要項目。</li></ul> |

{style="table-layout:auto"}

## 串流目的地的目的地傳送設定 {#destination-delivery-streaming}

下列範例說明應如何為串流目的地設定目的地傳送設定。 請注意， `deliveryMatchers` 串流目的地不需要區段。

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

## 檔案型目的地的目的地傳送設定 {#destination-delivery-file-based}

下列範例說明應如何為檔案型目的地設定目的地傳送設定。 請注意， `deliveryMatchers` 檔案型目的地需要區段。

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

閱讀本文後，您應該更清楚了解如何針對串流和檔案型目的地，設定目的地應匯出資料的位置。

若要進一步了解其他目的地元件，請參閱下列文章：

* [客戶驗證](customer-authentication.md)
* [OAuth2驗證](oauth2-authentication.md)
* [UI屬性](ui-attributes.md)
* [客戶資料欄位](customer-data-fields.md)
* [結構配置](schema-configuration.md)
* [身分命名空間設定](identity-namespace-configuration.md)
* [支援的對應配置](supported-mapping-configurations.md)
* [對象中繼資料設定](audience-metadata-configuration.md)
* [聚合策略](aggregation-policy.md)
* [批次設定](batch-configuration.md)
* [歷史設定檔資格](historical-profile-qualifications.md)