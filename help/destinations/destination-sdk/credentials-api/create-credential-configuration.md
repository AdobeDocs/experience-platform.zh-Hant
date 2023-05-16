---
description: 此頁面是建立憑證設定Adobe Experience Platform Destination SDK所使用的API呼叫的範例。
title: 建立憑據配置
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 7%

---


# 建立憑據配置

>[!IMPORTANT]
>
>**API端點**: `platform.adobe.io/data/core/activation/authoring/credentials`

此頁面是API要求和裝載的範例，您可以用來建立憑證設定，使用 `/authoring/credentials` API端點。

## 何時使用 `/credentials` API端點 {#when-to-use}

>[!IMPORTANT]
>
>在大多數情況下，您 ***不*** 需要使用 `/credentials` API端點。 反之，您可以透過 `customerAuthenticationConfigurations` 參數 `/destinations` 端點。
> 
>閱讀 [客戶驗證配置](../functionality/destination-configuration/customer-authentication.md) 以取得支援驗證類型的詳細資訊。

只有在Adobe與目的地平台之間有全域驗證系統，且 [!DNL Platform] 客戶不需要提供任何驗證憑證來連線至您的目的地。 在這種情況下，您必須使用 `/credentials` API端點。

使用全局身份驗證系統時，必須設定 `"authenticationRule":"PLATFORM_AUTHENTICATION"` 在 [目的地傳送](../functionality/destination-configuration/destination-delivery.md) 配置時 [建立新目標配置](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名稱和值均為 **區分大小寫**. 為避免區分大小寫錯誤，請使用參數名稱和值，如說明檔案所示。

## 憑證API操作快速入門 {#get-started}

繼續之前，請檢閱 [快速入門手冊](../getting-started.md) 若要成功呼叫API，需知的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 建立憑據配置 {#create}

您可以建立新憑證配置，方法是 `POST` 請求 `/authoring/credentials` 端點。

**API格式**

```http
POST /authoring/credentials
```

下列請求會建立新的憑證設定，由裝載中提供的參數定義。

選取下方的每個標籤，以檢視對應的裝載。

>[!BEGINTABS]

>[!TAB 基本]

**建立基本憑據配置**

+++請求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "basicAuthentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

| 參數 | 類型 | 說明 |
| -------- | ----------- | ----------- |
| `url` | 字串 | 授權提供程式的URL |
| `username` | 字串 | 憑據配置登錄用戶名 |
| `password` | 字串 | 憑據配置登錄密碼 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200，並包含新建立憑據組態的詳細資訊。

+++

>[!TAB Amazon S3]

**建立 [!DNL Amazon S3] 憑據配置**

+++**要求**

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   }
}
```

| 參數 | 類型 | 說明 |
| -------- | ----------- | ----------- |
| `accessId` | 字串 | [!DNL Amazon S3] 存取ID |
| `secretKey` | 字串 | [!DNL Amazon S3] 密鑰 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200，並包含新建立憑據組態的詳細資訊。

+++

>[!TAB SSH]

**建立SSH憑據配置**

+++請求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "sshAuthentication":{
      "username":"string",
      "sshKey":"string"
   }
}
```

| 參數 | 類型 | 說明 |
| -------- | ----------- | ----------- |
| `username` | 字串 | 憑據配置登錄用戶名 |
| `sshKey` | 字串 | SSH驗證的SFTP SSH金鑰 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200，並包含新建立憑據組態的詳細資訊。

+++

>[!TAB Azure資料湖儲存]

**建立 [!DNL Azure Data Lake Storage] 憑據配置**

+++請求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "azureAuthentication":{
      "url":"string",
      "tenant":"string",
      "servicePrincipalId":"string",
      "servicePrincipalKey":"string"
   }
}
```

| 參數 | 類型 | 說明 |
| -------- | ----------- | ----------- |
| `url` | 字串 | 授權提供程式的URL |
| `tenant` | 字串 | Azure資料湖儲存租戶 |
| `servicePrincipalId` | 字串 | Azure資料湖儲存的Azure服務主體ID |
| `servicePrincipalKey` | 字串 | Azure資料湖儲存的Azure服務主密鑰 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200，並包含新建立憑據組態的詳細資訊。

+++

>[!TAB Azure Blob 儲存體]

**建立 [!DNL Azure Blob Storage] 憑據配置**

+++請求

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
    "azureConnectionStringAuthentication":{
      "connectionString":"string"
   }
}
```

| 參數 | 類型 | 說明 |
| -------- | ----------- | ----------- |
| `connectionString` | 字串 | [!DNL Azure Blob Storage] 連接字串 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200，並包含新建立憑據組態的詳細資訊。

+++

>[!ENDTABS]

## API錯誤處理 {#error-handling}

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../../landing/troubleshooting.md#api-status-codes) 和 [請求標題錯誤](../../../landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中）。

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在知道何時應使用憑證端點，以及如何使用 `/authoring/credentials` API端點讀取 [如何使用Destination SDK來設定您的目的地](../guides/configure-destination-instructions.md) 了解此步驟在設定目的地程式中的適用位置。
