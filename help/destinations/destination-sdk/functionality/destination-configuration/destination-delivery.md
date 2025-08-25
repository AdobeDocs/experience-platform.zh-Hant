---
description: 瞭解如何為使用Destination SDK建立的目的地設定目的地傳送設定，以指出匯出的資料前往何處，以及在資料著陸位置使用什麼驗證規則。
title: 目的地傳遞
exl-id: ade77b6b-4b62-4b17-a155-ef90a723a4ad
source-git-commit: 560200a6553a1aae66c608eef7901b3248c886b4
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 2%

---

# 目的地傳遞

為了更能掌控資料匯出至目的地著陸的位置，Destination SDK可讓您指定目的地傳送設定。

目的地傳送區段會指出匯出的資料前往何處，以及資料著陸位置所使用的驗證規則。

<!-- When configuring a destination, you must specify an authentication rule and one or more `destinationServerId` parameters, corresponding to the destination servers that define where the data will be delivered to. In most cases, the authentication rule that you should use is `CUSTOMER_AUTHENTICATION`.  -->

若要瞭解此元件在何處適合使用Destination SDK建立的整合，請參閱[設定選項](../configuration-options.md)檔案中的圖表，或檢視以下目的地設定概觀頁面：

* [使用Destination SDK設定串流目的地](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [使用Destination SDK設定以檔案為基礎的目的地](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

您可以透過`/authoring/destinations`端點設定目的地傳遞設定。 請參閱下列API參考頁面，以取得詳細的API呼叫範例，您可在此範例設定本頁面中顯示的元件。

* [建立目的地設定](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目的地設定](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文會說明您可用於目的地的所有支援目的地傳送選項。

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值都會區分大小寫&#x200B;****。 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 支援的整合型別 {#supported-integration-types}

如需瞭解哪些型別的整合支援本頁面所述功能的詳細資訊，請參閱下表。

| 整合型別 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 是 |

## 支援的引數 {#supported-parameters}

設定目的地傳送設定時，您可以使用下表所述的引數來定義應傳送已匯出資料的位置。

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `authenticationRule` | 字串 | 指示[!DNL Experience Platform]應該如何連線到您的目的地。 支援的值：<ul><li>`CUSTOMER_AUTHENTICATION`：如果Experience Platform客戶透過[此處](customer-authentication.md)說明的任何驗證方法登入您的系統，請使用此選項。</li><li>`PLATFORM_AUTHENTICATION`：如果Adobe與您的目的地之間有全域驗證系統，且[!DNL Experience Platform]客戶不需要提供任何驗證認證即可連線至您的目的地，請使用此選項。 在此情況下，您必須使用[認證API](../../credentials-api/create-credential-configuration.md)設定來建立認證物件，並將`authenticationId`引數設定為認證物件識別碼值。</li><li>`NONE`：如果不需要驗證即可將資料傳送至您的目的地平台，請使用此選項。 </li></ul> |
| `authenticationId` | 字串 | 用於驗證的認證物件組態識別碼的`instanceId`。 只有在您需要指定特定認證組態時，才需要使用此引數。 |
| `destinationServerId` | 字串 | 您要匯出資料的`instanceId`目的地伺服器[的](../../authoring-api/destination-server/create-destination-server.md)。 |
| `deliveryMatchers.type` | 字串 | <ul><li>設定檔案型目的地的目的地傳遞時，請一律將此項設為`SOURCE`。</li><li>設定串流目的地的目的地傳遞時，`deliveryMatchers`區段不是必要的。</li></ul> |
| `deliveryMatchers.value` | 字串 | <ul><li>設定檔案型目的地的目的地傳遞時，請一律將此項設為`batch`。</li><li>設定串流目的地的目的地傳遞時，`deliveryMatchers`區段不是必要的。</li></ul> |

{style="table-layout:auto"}

## 串流目的地的目的地傳送設定 {#destination-delivery-streaming}

以下範例說明應如何為串流目的地設定目的地傳送設定。 請注意，串流目的地不需要`deliveryMatchers`區段。

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

以下範例說明應如何針對以檔案為基礎的目的地設定目的地傳送設定。 請注意，以檔案為基礎的目的地需要`deliveryMatchers`區段。

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

## 平台驗證設定 {#platform-authentication}

使用`PLATFORM_AUTHENTICATION`時，您必須指定`authenticationId`引數，將目的地組態連結至認證組態。

1. 在您的目的地組態中將`destinationDelivery.authenticationRule`設定為`"PLATFORM_AUTHENTICATION"`
2. [建立認證物件](/help/destinations/destination-sdk/credentials-api/create-credential-configuration.md)。
3. 將`authenticationId`引數設定為認證物件的`instanceId`值。

**具有PLATFORM_AUTHENTICATION的設定範例：**

>[!BEGINSHADEBOX]

```json
{
   "destinationDelivery":[
      {
         "authenticationRule":"PLATFORM_AUTHENTICATION",
         "authenticationId":"<string-here>",
         "destinationServerId":"<string-here>"
      }
   ]
}
```

>[!ENDSHADEBOX]

## 後續步驟 {#next-steps}

閱讀本文後，您應該更加瞭解如何針對串流和檔案型目的地，設定目的地應匯出資料的位置。

若要深入瞭解其他目的地元件，請參閱下列文章：

* [客戶驗證](customer-authentication.md)
* [OAuth2授權](oauth2-authorization.md)
* [UI屬性](ui-attributes.md)
* [客戶資料欄位](customer-data-fields.md)
* [結構描述設定](schema-configuration.md)
* [身分名稱空間設定](identity-namespace-configuration.md)
* [支援的對應設定](supported-mapping-configurations.md)
* [對象中繼資料設定](audience-metadata-configuration.md)
* [彙總原則](aggregation-policy.md)
* [批次設定](batch-configuration.md)
* [歷史設定檔資格](historical-profile-qualifications.md)
