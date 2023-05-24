---
description: 瞭解如何為目標設定身份驗證機制，並根據您選擇的身份驗證方法深入瞭解用戶在UI中將看到的內容。
title: 客戶身份驗證配置
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '1094'
ht-degree: 0%

---


# 客戶身份驗證配置

Experience Platform為合作夥伴和客戶提供的身份驗證協定提供了極大的靈活性。 您可以配置目標以支援任何行業標準的身份驗證方法，如 [!DNL OAuth2]、承載令牌驗證、密碼驗證等。

本頁說明如何使用首選身份驗證方法設定目標。 根據您在建立目標時使用的身份驗證配置，客戶在連接到Experience PlatformUI中的目標時將看到不同類型的身份驗證頁。

要瞭解此元件在與Destination SDK建立的整合中的位置，請參閱 [配置選項](../configuration-options.md) 文檔，或參閱以下目標配置概述頁：

* [使用Destination SDK配置流目標](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [使用Destination SDK配置基於檔案的目標](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

客戶必須先按照中介紹的步驟在Experience Platform和目標之間建立新連接，然後才能將資料從平台導出到目標 [目標連接](../../../ui/connect-destination.md) 教程。

當 [建立目標](../../authoring-api/destination-configuration/create-destination-configuration.md) 通過Destination SDK, `customerAuthenticationConfigurations` 定義客戶在 [認證螢幕](../../../ui/connect-destination.md#authenticate)。 根據目標身份驗證類型，客戶必須提供各種身份驗證詳細資訊，如：

* 對於使用 [基本認證](#basic)，用戶必須直接在Experience PlatformUI驗證頁中提供用戶名和密碼。
* 對於使用 [承載認證](#bearer)，用戶必須提供持有者令牌。
* 對於使用 [OAuth2身份驗證](#oauth2)，用戶將重定向到目標的登錄頁，在該頁上，他們可以使用其憑據登錄。
* 對於 [AmazonS3](#s3) 目標，用戶必須提供 [!DNL Amazon S3] 訪問密鑰和密鑰。
* 對於 [Azure Blob](#blob) 目標，用戶必須提供 [!DNL Azure Blob] 連接字串。

您可以通過 `/authoring/destinations` 端點。 有關詳細的API調用示例，請參閱以下API參考頁，在這些示例中可以配置此頁中顯示的元件。

* [建立目標配置](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [更新目標配置](../../authoring-api/destination-configuration/update-destination-configuration.md)

本文介紹可用於目標的所有受支援的客戶身份驗證配置，並根據您為目標設定的身份驗證方法顯示客戶在Experience PlatformUI中將看到的內容。

>[!IMPORTANT]
>
>客戶身份驗證配置不要求您配置任何參數。 當API調用中顯示的代碼段在 [建立](../../authoring-api/destination-configuration/create-destination-configuration.md) 或 [更新](../../authoring-api/destination-configuration/update-destination-configuration.md) 目標配置，您的用戶將在平台UI中看到相應的驗證螢幕。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名和值均 **區分大小寫**。 為避免區分大小寫錯誤，請完全按文檔所示使用參數名稱和值。

## 支援的整合類型 {#supported-integration-types}

有關哪些類型的整合支援本頁所述功能的詳細資訊，請參閱下表。

| 整合類型 | 支援功能 |
|---|---|
| 即時（流）整合 | 是 |
| 基於檔案（批處理）的整合 | 是 |

## 驗證規則配置 {#authentication-rule}

使用本頁中描述的任何客戶身份驗證配置時，始終設定 `authenticationRule` 參數 [目標傳遞](destination-delivery.md) 至 `"CUSTOMER_AUTHENTICATION"`，如下所示。

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

## 基本身份驗證 {#basic}

Experience Platform中的即時（流）整合支援基本身份驗證。

配置基本身份驗證類型時，用戶需要輸入用戶名和密碼以連接到目標。

![具有基本身份驗證的UI呈現](../../assets/functionality/destination-configuration/basic-authentication-ui.png)

要為目標設定基本身份驗證，請配置 `customerAuthenticationConfigurations` 的 `/destinations` 如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BASIC"
   }
]
```

## 承載驗證 {#bearer}

配置承載驗證類型時，用戶需要輸入從目標獲取的承載令牌。

![具有承載驗證的UI呈現](../../assets/functionality/destination-configuration/bearer-authentication-ui.png)

要為目標設定承載類型驗證，請配置 `customerAuthenticationConfigurations` 的 `/destinations` 如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BEARER"
   }
]
```

## OAuth 2身份驗證 {#oauth2}

用戶選擇 **[!UICONTROL 連接到目標]** 觸發到目標的OAuth 2身份驗證流，如下面的Twitter自定義訪問群體目標示例所示。 有關將OAuth 2身份驗證配置到目標終結點的詳細資訊，請閱讀專用 [Destination SDKOAuth 2身份驗證頁](oauth2-authentication.md)。

![UI呈現與OAuth 2身份驗證](../../assets/functionality/destination-configuration/oauth2-authentication-ui.png)

設定 [!DNL OAuth2] 為目標進行身份驗證，配置 `customerAuthenticationConfigurations` 的 `/destinations` 如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"OAUTH2"
   }
]
```

## AmazonS3驗證 {#s3}

[!DNL Amazon S3] 支援對Experience Platform中基於檔案的目標進行身份驗證。

配置AmazonS3身份驗證類型時，用戶需要輸入其S3憑據。

![使用S3身份驗證的UI呈現](../../assets/functionality/destination-configuration/s3-authentication-ui.png)

設定 [!DNL Amazon S3] 為目標進行身份驗證，配置 `customerAuthenticationConfigurations` 的 `/destinations` 如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"S3"
   }
]
```

## Azure Blob身份驗證  {#blob}

[!DNL Azure Blob Storage] 支援對Experience Platform中基於檔案的目標進行身份驗證。

配置Azure Blob身份驗證類型時，用戶需要輸入連接字串。

![UI呈現與Blob身份驗證](../../assets/functionality/destination-configuration/blob-authentication-ui.png)

設定 [!DNL Azure Blob] 為目標進行身份驗證，配置 `customerAuthenticationConfigurations` 參數 `/destinations` 如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## [!DNL Azure Data Lake Storage] 認證 {#adls}

[!DNL Azure Data Lake Storage] 支援對Experience Platform中基於檔案的目標進行身份驗證。

配置 [!DNL Azure Data Lake Storage] 身份驗證類型，用戶需要輸入Azure服務主體憑據及其租戶資訊。

![UI呈現 [!DNL Azure Data Lake Storage] 認證](../../assets/functionality/destination-configuration/adls-authentication-ui.png)

設定 [!DNL Azure Data Lake Storage] (ADLS)目標的身份驗證，配置 `customerAuthenticationConfigurations` 參數 `/destinations` 如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_SERVICE_PRINCIPAL"
   }
]
```

## 具有密碼驗證的SFTP

[!DNL SFTP] 對於Experience Platform中基於檔案的目標，支援使用口令進行身份驗證。

使用密碼驗證類型配置SFTP時，用戶需要輸入SFTP用戶名和密碼以及SFTP域和埠（預設埠為22）。

![UI呈現，SFTP帶密碼驗證](../../assets/functionality/destination-configuration/sftp-password-authentication-ui.png)

要設定目標的SFTP驗證，請配置 `customerAuthenticationConfigurations` 參數 `/destinations` 如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_PASSWORD"
   }
]
```

## SFTP與SSH密鑰驗證

[!DNL SFTP] 驗證 [!DNL SSH] 在Experience Platform中，基於檔案的目標支援鍵。

使用SSH密鑰驗證類型配置SFTP時，用戶需要輸入SFTP用戶名和SSH密鑰，以及SFTP域和埠（預設埠為22）。

![UI呈現，SFTP帶SSH密鑰驗證](../../assets/functionality/destination-configuration/sftp-key-authentication-ui.png)

要為目標設定SFTP驗證，請配置 `customerAuthenticationConfigurations` 參數 `/destinations` 如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## [!DNL Google Cloud Storage] 認證 {#gcs}

[!DNL Google Cloud Storage] 支援對Experience Platform中基於檔案的目標進行身份驗證。

配置 [!DNL Google Cloud Storage] 驗證類型，用戶需要輸入 [!DNL Google Cloud Storage] [!UICONTROL 訪問密鑰ID] 和 [!UICONTROL 密鑰訪問密鑰]。

![UI呈現與Google雲儲存身份驗證](../../assets/functionality/destination-configuration/google-cloud-storage-ui.png)

設定 [!DNL Google Cloud Storage] 為目標進行身份驗證，配置 `customerAuthenticationConfigurations` 參數 `/destinations` 如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"GOOGLE_CLOUD_STORAGE"
   }
]
```

## 後續步驟 {#next-steps}

閱讀本文後，您應更好地瞭解如何配置目標平台的用戶身份驗證。

要瞭解有關其他目標元件的詳細資訊，請參閱以下文章：

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
* [歷史配置檔案資格](historical-profile-qualifications.md)