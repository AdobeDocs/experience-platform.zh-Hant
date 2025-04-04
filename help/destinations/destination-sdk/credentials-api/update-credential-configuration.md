---
description: 此頁面是透過Adobe Experience Platform Destination SDK更新現有認證設定的API呼叫範例。
title: 更新認證設定
exl-id: ebff370c-9189-48df-871f-ed0e1cd535c8
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 5%

---

# 更新認證設定

>[!IMPORTANT]
>
>**API端點**： `platform.adobe.io/data/core/activation/authoring/credentials`

此頁面是您可用來使用`/authoring/credentials` API端點更新現有認證設定的API要求與裝載範例。

## 何時使用`/credentials` API端點 {#when-to-use}

>[!IMPORTANT]
>
>在大多數情況下，您&#x200B;***不***&#x200B;需要使用`/credentials` API端點。 您可以改為透過`/destinations`端點的`customerAuthenticationConfigurations`引數來設定您目的地的驗證資訊。
> 
>閱讀[客戶驗證組態](../functionality/destination-configuration/customer-authentication.md)，以取得支援的驗證型別的詳細資訊。

只有在Adobe和您的目的地平台之間有全域驗證系統，且[!DNL Experience Platform]客戶不需要提供任何驗證認證即可連線至您的目的地時，才使用此API端點來建立認證設定。 在此情況下，您必須使用`/credentials` API端點建立認證組態。

使用全域驗證系統時，在[建立新的目的地組態](../authoring-api/destination-configuration/create-destination-configuration.md)時，您必須在[目的地傳遞](../functionality/destination-configuration/destination-delivery.md)組態中設定`"authenticationRule":"PLATFORM_AUTHENTICATION"`。

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值都會區分大小寫&#x200B;****。 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 認證API操作快速入門 {#get-started}

繼續之前，請檢閱[快速入門手冊](../getting-started.md)以取得重要資訊，您必須瞭解這些資訊才能成功呼叫API，包括如何取得必要的目的地撰寫許可權和必要的標頭。

## 更新認證設定 {#update}

您可以藉由使用更新的承載對`/authoring/credentials`端點發出`PUT`要求，來更新[現有](create-credential-configuration.md)認證設定。

若要取得現有的認證組態及其對應的`{INSTANCE_ID}`，請參閱有關[擷取認證組態](retrieve-credential-configuration.md)的文章。

**API格式**

```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 您要更新的認證設定ID。 若要取得現有的認證組態及其對應的`{INSTANCE_ID}`，請參閱[擷取認證組態](retrieve-credential-configuration.md)。 |

以下請求會更新由承載中提供的引數定義的現有認證設定。

選取下方的每個索引標籤以檢視對應的裝載。

>[!BEGINTABS]

>[!TAB 基本]

**更新基本認證組態**

+++要求

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

**更新[!DNL Amazon S3]認證組態**

+++要求

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
| `accessId` | 字串 | [!DNL Amazon S3]存取識別碼 |
| `secretKey` | 字串 | [!DNL Amazon S3]秘密金鑰 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200以及您更新的認證設定的詳細資料。

+++

>[!TAB SSH]

**更新[!DNL SSH]認證組態**

+++要求

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
| `sshKey` | 字串 | 具有[!DNL SSH]驗證的[!DNL SFTP]的[!DNL SSH]金鑰 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200以及您更新的認證設定的詳細資料。

+++

>[!TAB Azure Data Lake儲存體]

**更新[!DNL Azure Data Lake Storage]認證組態**

+++要求

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
| `servicePrincipalId` | 字串 | [!DNL Azure Data Lake Storage]的[!DNL Azure Service Principal] ID |
| `servicePrincipalKey` | 字串 | [!DNL Azure Data Lake Storage]的[!DNL Azure Service Principal Key] |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200以及您更新的認證設定的詳細資料。

+++

>[!TAB Azure Blob儲存體]

**更新[!DNL Azure Blob]認證組態**

+++要求

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
| `connectionString` | 字串 | [!DNL Azure Blob Storage]連線字串 |

{style="table-layout:auto"}

+++

+++回應

成功的回應會傳回HTTP狀態200以及您更新的認證設定的詳細資料。

+++

>[!ENDTABS]

## API錯誤處理 {#error-handling}

Destination SDK API端點遵循一般Experience Platform API錯誤訊息原則。 請參閱Experience Platform疑難排解指南中的[API狀態碼](../../../landing/troubleshooting.md#api-status-codes)和[請求標頭錯誤](../../../landing/troubleshooting.md#request-header-errors)。

## 後續步驟 {#next-steps}

閱讀此檔案後，您現在知道如何使用`/authoring/credentials` API端點更新認證設定。 閱讀[如何使用Destination SDK來設定您的目的地](../guides/configure-destination-instructions.md)，以瞭解此步驟在設定目的地的程式中的位置。
