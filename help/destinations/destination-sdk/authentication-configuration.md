---
description: 使用Adobe Experience Platform Destination SDK中支援的身份驗證配置來驗證用戶並將資料激活到目標終結點。
title: 驗證配置
exl-id: 33eaab24-f867-4744-b424-4ba71727373c
source-git-commit: 92bca3600d854540fd2badd925e453fba41601a7
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 0%

---

# 驗證配置 {#credentials}

## 支援的身份驗證類型 {#supported-authentication-types}

您選擇的Experience Platform配置決定了平台UI中的身份驗證到目標的方式。

Adobe Experience Platform Destination SDK支援多種身份驗證類型：

* 承載驗證
* (Beta)AmazonS3驗證
* (Beta)Azure連接字串
* （測試版）Azure服務主體
* (Beta)SFTP，帶SSH密鑰
* (Beta)帶密碼的SFTP
* 具有授權代碼的OAuth 2
* 具有密碼授予的第2個非統組織
* 具有客戶端憑據授予的OAuth 2

您可以通過 `customerAuthenticationConfigurations` 參數 `/destinations` 端點。

有關每種類型目標的驗證配置詳細資訊，請參閱以下各節：

* [流目標的驗證配置](destination-configuration.md#customer-authentication-configurations)
* [基於檔案的目標的驗證配置](file-based-destination-configuration.md#customer-authentication-configurations)

## 承載驗證 {#bearer}

支援對Experience Platform中的流目標進行承載身份驗證。

要為目標設定承載類型驗證，請配置 `customerAuthenticationConfigurations` 參數 `/destinations` 如下所示：

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"BEARER"
      }
   ]
```

## (Beta) [!DNL Amazon S3] 認證 {#s3}

[!DNL Amazon S3] 支援對Experience Platform中基於檔案的目標進行身份驗證。

>[!IMPORTANT]
>
>Adobe Experience Platform Destination SDK中基於檔案的目標支援當前處於測試版中。 文檔和功能可能會更改。

要設定目標的AmazonS3身份驗證，請配置 `customerAuthenticationConfigurations` 參數 `/destinations` 如下所示：

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"S3"
      }
   ]
```

## (Beta) [!DNL Azure Blob Storage] {#blob}

[!DNL Azure Blob Storage] 支援對Experience Platform中基於檔案的目標進行身份驗證。

>[!IMPORTANT]
>
>Adobe Experience Platform Destination SDK中基於檔案的目標支援當前處於測試版中。 文檔和功能可能會更改。

設定 [!DNL Azure Blob] 為目標進行身份驗證，配置 `customerAuthenticationConfigurations` 參數 `/destinations` 如下所示：

```json
   "customerAuthenticationConfigurations":[
     {
        "authType":"AZURE_CONNECTION_STRING"
     }
  ]
```

## (Beta) [!DNL Azure Data Lake Storage] {#adls}

[!DNL Azure Data Lake Storage] 支援對Experience Platform中基於檔案的目標進行身份驗證。

>[!IMPORTANT]
>
>Adobe Experience Platform Destination SDK中基於檔案的目標支援當前處於測試版中。 文檔和功能可能會更改。

設定 [!DNL Azure Data Lake Storage] (ADLS)目標的身份驗證，配置 `customerAuthenticationConfigurations` 參數 `/destinations` 如下所示：

```json
   "customerAuthenticationConfigurations":[
     {
        "authType":"AZURE_SERVICE_PRINCIPAL"
     }
  ]
```

## (Beta) [!DNL SFTP] 驗證 [!DNL SSH] 鍵 {#sftp-ssh}

[!DNL SFTP] 驗證 [!DNL SSH] 在Experience Platform中，基於檔案的目標支援鍵。

>[!IMPORTANT]
>
>Adobe Experience Platform Destination SDK中基於檔案的目標支援當前處於測試版中。 文檔和功能可能會更改。

要為目標設定SFTP驗證，請配置 `customerAuthenticationConfigurations` 參數 `/destinations` 如下所示：

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"SFTP_WITH_SSH_KEY"
      }
   ]
```

## (Beta) [!DNL SFTP] 密碼驗證 {#sftp-password}

[!DNL SFTP] 對於Experience Platform中基於檔案的目標，支援使用口令進行身份驗證。

>[!IMPORTANT]
>
>Adobe Experience Platform Destination SDK中基於檔案的目標支援當前處於測試版中。 文檔和功能可能會更改。

要設定目標的SFTP驗證，請配置 `customerAuthenticationConfigurations` 參數 `/destinations` 如下所示：

```json
   "customerAuthenticationConfigurations":[
      {
         "authType":"SFTP_WITH_PASSWORD"
      }
   ]
```

## [!DNL OAuth 2] 認證 {#oauth2}

[!DNL OAuth 2] 支援對Experience Platform中的流目標進行身份驗證。

有關如何設定各種受支援的OAuth 2流以及自定義OAuth 2支援的資訊，請閱讀有關的Destination SDK文檔 [OAuth 2身份驗證](./oauth2-authentication.md)。


## 何時使用 `/credentials` API終結點 {#when-to-use}

>[!IMPORTANT]
>
>在大多數情況下，你 *不* 需要使用 `/credentials` API終結點。 相反，您可以通過 `customerAuthenticationConfigurations` 參數 `/destinations` 端點。

的 `/credentials` 當Adobe與目標之間存在全局身份驗證系統時，將向目標開發人員提供API終結點 [!DNL Platform] 客戶不需要提供任何身份驗證憑據來連接到目標。

在這種情況下，必須使用 `/credentials` API終結點。 您還必須選擇 `PLATFORM_AUTHENTICATION` 的 [目標配置](./destination-configuration.md#destination-delivery)。 閱讀 [憑據API終結點操作](./credentials-configuration-api.md) 可以在 `/credentials` 端點。
