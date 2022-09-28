---
description: 使用中支援的驗證設定來驗證使用者，並將資料啟用至您的目的地端點。
title: 驗證配置
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: 9b4c7da5aa02ae27608c2841b1d825445ac3015e
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# 驗證配置 {#credentials}

## 支援的驗證類型 {#supported-authentication-types}

您選取的驗證設定會決定Experience Platform在Platform UI中對您目的地進行驗證的方式。

Adobe Experience Platform Destination SDK支援數種驗證類型：

* [承載驗證](#bearer)
* [[!DNL Amazon S3] 驗證](#s3)
* [[!DNL Azure Blob] 儲存空間](#blob)
* [[!DNL Azure Data Lake Storage]](#adls)
* [[!DNL Google Cloud Storage]](#gcs)
* [具有SSH金鑰的SFTP](#sftp-ssh)
* [使用密碼的SFTP](#sftp-password)
* [OAuth 2，含授權碼](#oauth2)
* [具有密碼授權的第2個非統組織](#oauth2)
* [具有客戶端憑據授予的OAuth 2](#oauth2)

您可以透過 `customerAuthenticationConfigurations` 參數 `/destinations` 端點。

如需每種目的地類型的驗證設定詳細資訊，請參閱下列章節：

* [串流目的地的驗證設定](destination-configuration.md#customer-authentication-configurations)
* [檔案型目的地的驗證設定](file-based-destination-configuration.md#customer-authentication-configurations)

## 承載驗證 {#bearer}

Experience Platform中的串流目的地支援承載驗證。

若要設定目的地的承載類型驗證，請設定 `customerAuthenticationConfigurations` 參數 `/destinations` 端點，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"BEARER"
   }
]
```

## [!DNL Amazon S3] 驗證 {#s3}

[!DNL Amazon S3] Experience Platform中的檔案型目的地支援驗證。

設定 [!DNL Amazon S3] 目的地的驗證，請設定 `customerAuthenticationConfigurations` 參數 `/destinations` 端點，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"S3"
   }
]
```

## [!DNL Azure Blob Storage] {#blob}

[!DNL Azure Blob Storage] Experience Platform中的檔案型目的地支援驗證。

設定 [!DNL Azure Blob] 目的地的驗證，請設定 `customerAuthenticationConfigurations` 參數 `/destinations` 端點，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_CONNECTION_STRING"
   }
]
```

## [!DNL Azure Data Lake Storage] {#adls}

[!DNL Azure Data Lake Storage] Experience Platform中的檔案型目的地支援驗證。

設定 [!DNL Azure Data Lake Storage] (ADLS)目的地的驗證，請設定 `customerAuthenticationConfigurations` 參數 `/destinations` 端點，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"AZURE_SERVICE_PRINCIPAL"
   }
]
```

## [!DNL Google Cloud Storage] {#gcs}

[!DNL Google Cloud Storage] Experience Platform中的檔案型目的地支援驗證。

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"GOOGLE_CLOUD_STORAGE"
   }
]
```


## [!DNL SFTP] 驗證 [!DNL SSH] key {#sftp-ssh}

[!DNL SFTP] 驗證 [!DNL SSH] Experience Platform中的檔案型目的地支援金鑰。

若要使用SSH金鑰設定目的地的SFTP驗證，請設定 `customerAuthenticationConfigurations` 參數 `/destinations` 端點，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_SSH_KEY"
   }
]
```

## [!DNL SFTP] 密碼驗證 {#sftp-password}

[!DNL SFTP] Experience Platform中的檔案型目的地支援使用密碼驗證。

若要使用您目的地的密碼設定SFTP驗證，請設定 `customerAuthenticationConfigurations` 參數 `/destinations` 端點，如下所示：

```json
"customerAuthenticationConfigurations":[
   {
      "authType":"SFTP_WITH_PASSWORD"
   }
]
```

## [!DNL OAuth 2] 驗證 {#oauth2}

[!DNL OAuth 2] Experience Platform中的串流目的地支援驗證。

有關如何設定各種受支援的 [!DNL OAuth 2] 流，以及自訂 [!DNL OAuth 2] 支援，請閱讀Destination SDK檔案，位於 [[!DNL OAuth 2] 驗證](./oauth2-authentication.md).


## 何時使用 `/credentials` API端點 {#when-to-use}

>[!IMPORTANT]
>
>在大多數情況下，您 *不* 需要使用 `/credentials` API端點。 反之，您可以透過 `customerAuthenticationConfigurations` 參數 `/destinations` 端點。

此 `/credentials` 當Adobe與您的目的地和 [!DNL Platform] 客戶不需要提供任何驗證憑證來連線至您的目的地。

在此情況下，您必須使用 `/credentials` API端點。 您也必須選取 `PLATFORM_AUTHENTICATION` 在 [目的地配置](./destination-configuration.md#destination-delivery). 閱讀 [憑證API端點操作](./credentials-configuration-api.md) 以取得您可在 `/credentials` 端點。
