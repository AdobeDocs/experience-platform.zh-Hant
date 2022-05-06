---
description: 本頁介紹了可以使用「/authoring/credentials」 API終結點執行的所有API操作。
title: 憑據終結點API操作
exl-id: 89957f38-e7f4-452d-abc0-0940472103fe
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '797'
ht-degree: 4%

---

# 憑據終結點API操作 {#credentials}

>[!IMPORTANT]
>
>**API終結點**: `platform.adobe.io/data/core/activation/authoring/credentials`

此頁列出並說明了可以使用 `/authoring/credentials` API終結點。

有關此終結點支援的功能的說明，請閱讀：

* [流目標配置](destination-configuration.md) 為流目標配置的功能。
* [基於檔案的目標配置](file-based-destination-configuration.md) 為基於檔案的目標配置的功能。

## 何時使用 `/credentials` API終結點 {#when-to-use}

>[!IMPORTANT]
>
>在大多數情況下，你 *不* 需要使用 `/credentials` API終結點。 相反，您可以通過 `customerAuthenticationConfigurations` 參數 `/destinations` 端點。 閱讀 [驗證配置](./authentication-configuration.md#when-to-use) 的子菜單。

使用此API終結點並選擇 `PLATFORM_AUTHENTICATION` 的 [目標配置](./destination-configuration.md#destination-delivery) 如果Adobe與目標之間有全局身份驗證系統， [!DNL Platform] 客戶不需要提供任何身份驗證憑據來連接到目標。 在這種情況下，必須使用 `/credentials` API終結點。

## 憑據配置API操作入門 {#get-started}

在繼續之前，請查看 [入門指南](./getting-started.md) 瞭解成功調用API所需的重要資訊，包括如何獲得所需的目標創作權限和所需的標題。

## 建立憑據配置 {#create}

通過向POST請求建立新的憑據配置 `/authoring/credentials` 端點。

**API格式**

```http
POST /authoring/credentials
```

**要求**

以下請求將建立由負載中提供的參數配置的新憑據配置。 下面的負載包括接受的所有參數 `/authoring/credentials` 端點。 請注意，您不必在調用中添加所有參數，並且模板可根據API要求進行自定義。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "oauth2UserAuthentication":{
      "url":"string",
      "clientId":"string",
      "clientSecret":"string",
      "username":"string",
      "password":"string",
      "header":"string"
   },
   "oauth2ClientAuthentication":{
      "url":"string",
      "clientId":"string",
      "clientSecret":"string",
      "header":"string",
      "developerToken":"string"
   },
   "oauth2AccessTokenAuthentication":{
      "accessToken":"string",
      "expiration":"string",
      "username":"string",
      "userId":"string",
      "url":"string",
      "header":"string"
   },
   "oauth2RefreshTokenAuthentication":{
      "refreshToken":"string",
      "expiration":"string",
      "clientId":"string",
      "clientSecret":"string",
      "url":"string",
      "header":"string"
   },
   "s3Authentication":{
      "accessId":"string",
      "secretKey":"string"
   },
   "sshAuthentication":{
      "username":"string",
      "sshKey":"string"
   },
   "azureAuthentication":{
      "url":"string",
      "tenant":"string",
      "servicePrincipalId":"string",
      "servicePrincipalKey":"string"
   },
   "azureConnectionStringAuthentication":{
      "connectionString":"string"
   },
   "basicAuthentication":{
      "url":"string",
      "username":"string",
      "password":"string"
   }
}
```

| 參數 | 類型 | 說明 |
| -------- | ----------- | ----------- |
| `username` | 字串 | 憑據配置登錄用戶名 |
| `password` | 字串 | 憑據配置登錄密碼 |
| `url` | 字串 | 授權提供程式的URL |
| `clientId` | 字串 | 客戶端/應用程式憑據的客戶端ID |
| `clientSecret` | 字串 | 客戶端/應用程式憑據的客戶端密鑰 |
| `accessToken` | 字串 | 授權提供程式提供的訪問令牌 |
| `expiration` | 字串 | 訪問令牌的生存時間 |
| `refreshToken` | 字串 | 由授權提供程式提供的刷新令牌 |
| `header` | 字串 | 授權所需的任何標頭 |
| `accessId` | 字串 | AmazonS3訪問ID |
| `secretKey` | 字串 | AmazonS3密鑰 |
| `sshKey` | 字串 | SSH認證的SFTP的SSH密鑰 |
| `tenant` | 字串 | Azure資料湖儲存租戶 |
| `servicePrincipalId` | 字串 | Azure資料湖儲存的Azure服務主體ID |
| `servicePrincipalKey` | 字串 | Azure資料湖儲存的Azure服務主體密鑰 |
| `connectionString` | 字串 | Azure Blob儲存連接字串 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的響應返回HTTP狀態200，其中包含新建立的憑據配置的詳細資訊。

## 列出憑據配置 {#retrieve-list}

通過向IMS組織發出GET請求，您可以檢索IMS組織的所有憑據配置清單 `/authoring/credentials` 端點。

**API格式**


```http
GET /authoring/credentials
```

**要求**

以下請求將根據IMS組織和沙盒配置檢索您有權訪問的憑據配置清單。

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

以下響應會根據您使用的IMS組織ID和沙盒名稱返回HTTP狀態200，其中包含您有權訪問的憑據配置清單。 一 `instanceId` 對應於一個憑據配置的模板。 響應被截斷以便簡化。

```json
{
   "items":[
      {
         "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
         "createdDate":"2021-06-07T06:41:48.641943Z",
         "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
         "type":"OAUTH2_USER_CREDENTIAL",
         "name":"yourdestination",
         "oauth2UserAuthentication":{
            "url":"ABCD",
            "clientId":"ABCDEFGHIJKL",
            "clientSecret":"clientsecret",
            "username":"username",
            "password":"password",
            "header":"header"
         }
      }
   ]
}
    
```

## 更新現有憑據配置 {#update}

通過向發出PUT請求，可以更新現有的憑據配置 `/authoring/credentials` 終結點並提供要更新的憑據配置的實例ID。 在呼叫正文中，提供更新的憑據配置。

**API格式**


```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 要更新的憑據配置的ID。 |

**要求**

以下請求更新現有憑據配置，配置由負載中提供的參數進行。

```shell
curl -X PUT https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"OAUTH2_USER_CREDENTIAL",
   "name":"yourdestination",
   "oauth2UserAuthentication":{
      "url":"ABCD",
      "clientId":"ABCDEFGHIJKL",
      "clientSecret":"clientsecret",
      "username":"username",
      "password":"password",
      "header":"header"
   }
}
```

## 檢索特定憑據配置 {#get}

您可以通過向Oracle Server發出GET請求來檢索有關特定憑據配置的詳細資訊 `/authoring/credentials` 終結點並提供要更新的憑據配置的實例ID。

**API格式**

```http
GET /authoring/credentials/{INSTANCE_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 要檢索的憑據配置的ID。 |

**要求**

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回HTTP狀態200，其中包含有關指定憑據配置的詳細資訊。

```json
{
   "instanceId":"n55affa0-3747-4030-895d-1d1236bb3680",
   "createdDate":"2021-06-07T06:41:48.641943Z",
   "lastModifiedDate":"2021-06-07T06:41:48.641943Z",
   "type":"OAUTH2_USER_CREDENTIAL",
   "name":"yourdestination",
   "oauth2UserAuthentication":{
      "url":"ABCD",
      "clientId":"ABCDEFGHIJKL",
      "clientSecret":"clientsecret",
      "username":"username",
      "password":"password",
      "header":"header"
   }
}
```

## 刪除特定憑據配置 {#delete}

您可以通過向DELETE請求刪除指定的憑據配置 `/authoring/credentials` 終結點，並提供在請求路徑中要刪除的憑據配置的ID。

**API格式**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 的 `id` 刪除的憑據配置。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的響應返回HTTP狀態200以及空的HTTP響應。

## API錯誤處理

Destination SDKAPI端點遵循常規Experience PlatformAPI錯誤消息原則。 請參閱 [API狀態代碼](../../landing/troubleshooting.md#api-status-codes) 和 [請求標頭錯誤](../../landing/troubleshooting.md#request-header-errors) 中。

## 後續步驟

閱讀此文檔後，您現在知道何時使用憑據終結點以及如何使用 `/authoring/credentials` API終結點或 `/authoring/destinations` 端點。 閱讀 [如何使用Destination SDK配置目標](./configure-destination-instructions.md) 瞭解此步驟在配置目標過程中的適用範圍。
