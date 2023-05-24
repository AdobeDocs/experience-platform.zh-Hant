---
description: 本頁說明了用於建立憑據配置Adobe Experience Platform Destination SDK的API調用。
title: 建立憑據配置
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 7%

---


# 建立憑據配置

>[!IMPORTANT]
>
>**API終結點**: `platform.adobe.io/data/core/activation/authoring/credentials`

本頁說明了API請求和負載，您可以使用 `/authoring/credentials` API終結點。

## 何時使用 `/credentials` API終結點 {#when-to-use}

>[!IMPORTANT]
>
>在大多數情況下，你 ***不*** 需要使用 `/credentials` API終結點。 相反，您可以通過 `customerAuthenticationConfigurations` 參數 `/destinations` 端點。
> 
>閱讀 [客戶身份驗證配置](../functionality/destination-configuration/customer-authentication.md) 的子菜單。

僅當Adobe與目標平台之間存在全局身份驗證系統時，才使用此API終結點建立憑據配置， [!DNL Platform] 客戶不需要提供任何身份驗證憑據來連接到目標。 在這種情況下，必須使用 `/credentials` API終結點。

使用全局身份驗證系統時，必須設定 `"authenticationRule":"PLATFORM_AUTHENTICATION"` 的 [目標傳遞](../functionality/destination-configuration/destination-delivery.md) 配置，當 [建立新目標配置](../authoring-api/destination-configuration/create-destination-configuration.md)。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名和值均 **區分大小寫**。 為避免區分大小寫錯誤，請完全按文檔所示使用參數名稱和值。

## 憑據API操作入門 {#get-started}

在繼續之前，請查看 [入門指南](../getting-started.md) 瞭解成功調用API所需的重要資訊，包括如何獲得所需的目標創作權限和所需的標題。

## 建立憑據配置 {#create}

通過建立 `POST` 請求 `/authoring/credentials` 端點。

**API格式**

```http
POST /authoring/credentials
```

以下請求建立新的憑據配置，這些配置由負載中提供的參數定義。

選擇下面的每個頁籤以查看相應的負載。

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

成功的響應返回HTTP狀態200，其中包含新建立的憑據配置的詳細資訊。

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
| `accessId` | 字串 | [!DNL Amazon S3] 訪問ID |
| `secretKey` | 字串 | [!DNL Amazon S3] 密鑰 |

{style="table-layout:auto"}

+++

+++回應

成功的響應返回HTTP狀態200，其中包含新建立的憑據配置的詳細資訊。

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
| `sshKey` | 字串 | SSH認證的SFTP的SSH密鑰 |

{style="table-layout:auto"}

+++

+++回應

成功的響應返回HTTP狀態200，其中包含新建立的憑據配置的詳細資訊。

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
| `servicePrincipalKey` | 字串 | Azure資料湖儲存的Azure服務主體密鑰 |

{style="table-layout:auto"}

+++

+++回應

成功的響應返回HTTP狀態200，其中包含新建立的憑據配置的詳細資訊。

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

成功的響應返回HTTP狀態200，其中包含新建立的憑據配置的詳細資訊。

+++

>[!ENDTABS]

## API錯誤處理 {#error-handling}

Destination SDKAPI端點遵循常規Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../landing/troubleshooting.md#request-header-errors) 中。

## 後續步驟 {#next-steps}

閱讀此文檔後，您現在知道何時使用憑據終結點以及如何使用 `/authoring/credentials` API終結點讀取 [如何使用Destination SDK配置目標](../guides/configure-destination-instructions.md) 瞭解此步驟在配置目標過程中的適用範圍。
