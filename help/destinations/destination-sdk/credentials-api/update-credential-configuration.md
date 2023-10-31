---
description: 此頁面是用來透過Adobe Experience Platform Destination SDK更新現有認證設定的API呼叫的範例。
title: 更新認證設定
exl-id: ebff370c-9189-48df-871f-ed0e1cd535c8
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 8%

---

# 更新認證設定

>[!IMPORTANT]
>
>**API端點**： `platform.adobe.io/data/core/activation/authoring/credentials`

此頁面以範例說明可用於更新現有認證設定的API請求和裝載，使用 `/authoring/credentials` api端點。

## 何時使用 `/credentials` API端點 {#when-to-use}

>[!IMPORTANT]
>
>在大多數情況下，您 ***不要*** 需要使用 `/credentials` api端點。 您可以改為透過以下方式設定目的地的驗證資訊： `customerAuthenticationConfigurations` 的引數 `/destinations` 端點。
> 
>讀取 [客戶驗證設定](../functionality/destination-configuration/customer-authentication.md) 以取得支援驗證型別的詳細資訊。

只有在Adobe和您的目的地平台之間存在全域驗證系統，而且 [!DNL Platform] 客戶不需要提供任何驗證認證即可連線至您的目的地。 在此情況下，您必須使用 `/credentials` api端點。

使用全域驗證系統時，您必須設定 `"authenticationRule":"PLATFORM_AUTHENTICATION"` 在 [目的地傳遞](../functionality/destination-configuration/destination-delivery.md) 設定，當 [建立新的目的地組態](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值如下 **區分大小寫**. 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 認證API操作快速入門 {#get-started}

在繼續之前，請檢閱 [快速入門手冊](../getting-started.md) 如需您成功呼叫API所需的重要資訊，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 更新認證設定 {#update}

您可以更新 [現有](create-credential-configuration.md) 認證設定，透過發出 `PUT` 要求給 `/authoring/credentials` 具有已更新裝載的端點。

若要取得現有的認證設定及其對應的認證設定 `{INSTANCE_ID}`，請參閱「 」一文，瞭解 [擷取認證設定](retrieve-credential-configuration.md).

**API格式**

```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 您要更新的認證設定ID。 若要取得現有的認證設定及其對應的認證設定 `{INSTANCE_ID}`，請參閱 [擷取認證設定](retrieve-credential-configuration.md). |

以下請求會更新由承載中提供的引數定義的現有認證設定。

選取下方的每個索引標籤以檢視對應的裝載。

>[!BEGINTABS]

>[!TAB 基本]

**更新基本認證設定**

+++請求

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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
| `url` | 字串 | 授權提供者的URL |
| `username` | 字串 | 認證組態登入使用者名稱 |
| `password` | 字串 | 認證組態登入密碼 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200以及您更新的認證設定的詳細資料。

+++

>[!TAB Amazon S3]

**更新 [!DNL Amazon S3] 認證設定**

+++請求

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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
| `accessId` | 字串 | [!DNL Amazon S3] 存取識別碼 |
| `secretKey` | 字串 | [!DNL Amazon S3] 秘密金鑰 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200以及您更新的認證設定的詳細資料。

+++

>[!TAB SSH]

**更新 [!DNL SSH] 認證設定**

+++請求

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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
| `username` | 字串 | 認證組態登入使用者名稱 |
| `sshKey` | 字串 | [!DNL SSH] 索引鍵： [!DNL SFTP] 替換為 [!DNL SSH] authentication |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200以及您更新的認證設定的詳細資料。

+++

>[!TAB Azure Data Lake儲存]

**更新 [!DNL Azure Data Lake Storage] 認證設定**

+++請求

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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
| `url` | 字串 | 授權提供者的URL |
| `tenant` | 字串 | Azure Data Lake Storage租使用者 |
| `servicePrincipalId` | 字串 | [!DNL Azure Service Principal] 的ID [!DNL Azure Data Lake Storage] |
| `servicePrincipalKey` | 字串 | [!DNL Azure Service Principal Key] for [!DNL Azure Data Lake Storage] |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200以及您更新的認證設定的詳細資料。

+++

>[!TAB Azure Blob 儲存體]

**更新 [!DNL Azure Blob] 認證設定**

+++請求

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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
| `connectionString` | 字串 | [!DNL Azure Blob Storage] 連線字串 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200以及您更新的認證設定的詳細資料。

+++

>[!ENDTABS]

## API錯誤處理 {#error-handling}

Destination SDK API端點遵循一般Experience Platform API錯誤訊息原則。 請參閱 [API狀態代碼](../../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../../landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中）。

## 後續步驟 {#next-steps}

閱讀本檔案後，您現在知道如何使用 `/authoring/credentials` api端點。 讀取 [如何使用Destination SDK來設定您的目的地](../guides/configure-destination-instructions.md) 以瞭解此步驟在設定目的地的程式中的適用位置。
