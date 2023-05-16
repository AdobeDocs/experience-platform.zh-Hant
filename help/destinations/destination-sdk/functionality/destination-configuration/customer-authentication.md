---
description: 了解如何為您的目的地設定驗證機制，並根據您選取的驗證方法，深入了解使用者在UI中會看到的內容。
title: 客戶驗證配置
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1094'
ht-degree: 0%

---


# 客戶驗證配置

Experience Platform在合作夥伴和客戶可用的驗證通訊協定中提供極大的彈性。 您可以設定目的地以支援任何業界標準驗證方法，例如 [!DNL OAuth2]、承載權杖驗證、密碼驗證等。

本頁面說明如何使用您偏好的驗證方法來設定您的目的地。 根據您在建立目的地時使用的驗證設定，客戶在Experience PlatformUI中連線至目的地時，會看到不同類型的驗證頁面。

若要了解此元件在透過Destination SDK建立的整合中的插入位置，請參閱 [配置選項](../configuration-options.md) 檔案或請參閱下列目的地組態概觀頁面：

* [使用Destination SDK來設定串流目的地](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [使用Destination SDK配置基於檔案的目標](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

客戶必須先依照 [目的地連線](../../../ui/connect-destination.md) 教學課程。

當 [建立目的地](../../authoring-api/destination-configuration/create-destination-configuration.md) 透過Destination SDK, `customerAuthenticationConfigurations` 一節定義客戶在 [驗證螢幕](../../../ui/connect-destination.md#authenticate). 根據目標驗證類型，客戶必須提供各種驗證詳細資訊，例如：

* 針對使用 [基本驗證](#basic)，使用者必須直接在「Experience PlatformUI驗證」頁面中提供使用者名稱和密碼。
* 針對使用 [承載認證](#bearer)，則使用者必須提供不記名代號。
* 針對使用 [OAuth2驗證](#oauth2)，系統會將使用者重新導向至您目的地的登入頁面，讓使用者以其憑證登入。
* 針對 [Amazon S3](#s3) 目的地，使用者必須提供 [!DNL Amazon S3] 存取金鑰和機密金鑰。
* 針對 [Azure Blob](#blob) 目的地，使用者必須提供 [!DNL Azure Blob] 連線字串。

您可以透過 `/authoring/destinations` 端點。 如需詳細API呼叫範例，請參閱下列API參考頁面，您可在其中設定本頁面所示的元件。

* [建立目標配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目標配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文說明您可用於目的地的所有支援客戶驗證設定，並根據您為目的地設定的驗證方法，顯示Experience PlatformUI中的客戶將看到什麼。

>[!IMPORTANT]
>
>客戶驗證設定不需要您設定任何參數。 當 [建立](../../authoring-api/destination-configuration/create-destination-configuration.md) 或 [更新](../../authoring-api/destination-configuration/update-destination-configuration.md) 目的地設定，而您的使用者會在Platform UI中看到對應的驗證畫面。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名稱和值均為 **區分大小寫**. 為避免區分大小寫錯誤，請使用參數名稱和值，如說明檔案所示。

## 支援的整合類型 {#supported-integration-types}

如需詳細資訊，請參閱下表以了解哪些類型的整合支援本頁面所述的功能。

| 整合類型 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 是 |

## 驗證規則配置 {#authentication-rule}

使用本頁所述的任何客戶驗證設定時，請一律將 `authenticationRule` 參數 [目的地傳送](destination-delivery.md) to `"CUSTOMER_AUTHENTICATION"`，如下所示。

```json {line-numbers="true" highlight="4"
{
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

## 基本驗證 {#basic}

Experience Platform中的即時（串流）整合支援基本驗證。

配置基本身份驗證類型時，用戶需要輸入用戶名和密碼以連接到目標。

![UI使用基本驗證呈現](../../assets/functionality/destination-configuration/basic-authentication-ui.png)

若要設定目的地的基本驗證，請設定 `customerAuthenticationConfigurations` 區段 `/destinations` 端點，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BASIC"
   }
]
```

## 承載驗證 {#bearer}

當您配置承載身份驗證類型時，用戶需要輸入從您的目標獲取的承載令牌。

![使用承載驗證呈現UI](../../assets/functionality/destination-configuration/bearer-authentication-ui.png)

若要設定目的地的承載類型驗證，請設定 `customerAuthenticationConfigurations` 區段 `/destinations` 端點，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BEARER"
   }
]
```

## OAuth 2驗證 {#oauth2}

用戶選擇 **[!UICONTROL 連接到目標]** 觸發OAuth 2驗證流程至您的目的地，如下列Twitter自訂對象目的地範例所示。 如需設定OAuth 2驗證至目的地端點的詳細資訊，請參閱專用 [Destination SDKOAuth 2驗證頁面](oauth2-authentication.md).

![UI以OAuth 2驗證呈現](../../assets/functionality/destination-configuration/oauth2-authentication-ui.png)

設定 [!DNL OAuth2] 目的地的驗證，請設定 `customerAuthenticationConfigurations` 區段 `/destinations` 端點，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"OAUTH2"
   }
]
```

## Amazon S3驗證 {#s3}

[!DNL Amazon S3] Experience Platform中的檔案型目的地支援驗證。

設定Amazon S3驗證類型時，使用者必須輸入其S3憑證。

![UI以S3驗證呈現](../../assets/functionality/destination-configuration/s3-authentication-ui.png)

設定 [!DNL Amazon S3] 目的地的驗證，請設定 `customerAuthenticationConfigurations` 區段 `/destinations` 端點，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"S3"
   }
]
```

## Azure Blob驗證  {#blob}

[!DNL Azure Blob Storage] Experience Platform中的檔案型目的地支援驗證。

配置Azure Blob身份驗證類型時，用戶需要輸入連接字串。

![使用Blob驗證呈現UI](../../assets/functionality/destination-configuration/blob-authentication-ui.png)

設定 [!DNL Azure Blob] 目的地的驗證，請設定 `customerAuthenticationConfigurations` 參數 `/destinations` 端點，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## [!DNL Azure Data Lake Storage] 驗證 {#adls}

[!DNL Azure Data Lake Storage] Experience Platform中的檔案型目的地支援驗證。

當您設定 [!DNL Azure Data Lake Storage] 身份驗證類型，用戶需要輸入Azure服務主體憑據及其租戶資訊。

![UI呈現為 [!DNL Azure Data Lake Storage] 驗證](../../assets/functionality/destination-configuration/adls-authentication-ui.png)

設定 [!DNL Azure Data Lake Storage] (ADLS)目的地的驗證，請設定 `customerAuthenticationConfigurations` 參數 `/destinations` 端點，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_SERVICE_PRINCIPAL"
   }
]
```

## 具有密碼驗證的SFTP

[!DNL SFTP] Experience Platform中的檔案型目的地支援使用密碼驗證。

使用密碼驗證類型設定SFTP時，使用者必須輸入SFTP使用者名稱和密碼，以及SFTP網域和連接埠（預設連接埠為22）。

![使用SFTP呈現UI並進行密碼驗證](../../assets/functionality/destination-configuration/sftp-password-authentication-ui.png)

若要使用您目的地的密碼設定SFTP驗證，請設定 `customerAuthenticationConfigurations` 參數 `/destinations` 端點，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_PASSWORD"
   }
]
```

## SSH金鑰驗證的SFTP

[!DNL SFTP] 驗證 [!DNL SSH] Experience Platform中的檔案型目的地支援金鑰。

使用SSH金鑰驗證類型設定SFTP時，使用者必須輸入SFTP使用者名稱和SSH金鑰，以及SFTP網域和連接埠（預設連接埠為22）。

![UI透過SSH金鑰驗證透過SFTP轉譯](../../assets/functionality/destination-configuration/sftp-key-authentication-ui.png)

若要使用SSH金鑰設定目的地的SFTP驗證，請設定 `customerAuthenticationConfigurations` 參數 `/destinations` 端點，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## [!DNL Google Cloud Storage] 驗證 {#gcs}

[!DNL Google Cloud Storage] Experience Platform中的檔案型目的地支援驗證。

當您設定 [!DNL Google Cloud Storage] 驗證類型，需要用戶輸入 [!DNL Google Cloud Storage] [!UICONTROL 訪問密鑰ID] 和 [!UICONTROL 秘密訪問密鑰].

![UI透過Google雲端儲存驗證轉譯](../../assets/functionality/destination-configuration/google-cloud-storage-ui.png)

設定 [!DNL Google Cloud Storage] 目的地的驗證，請設定 `customerAuthenticationConfigurations` 參數 `/destinations` 端點，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"GOOGLE_CLOUD_STORAGE"
   }
]
```

## 後續步驟 {#next-steps}

閱讀本文後，您應該更了解如何設定目的地平台的使用者驗證。

若要進一步了解其他目的地元件，請參閱下列文章：

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
* [歷史設定檔資格](historical-profile-qualifications.md)