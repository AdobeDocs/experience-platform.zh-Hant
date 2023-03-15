---
description: 本頁面說明您可以使用「/authoring/credentials」 API端點執行的所有API操作。
title: 憑證端點API操作
exl-id: 89957f38-e7f4-452d-abc0-0940472103fe
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '794'
ht-degree: 4%

---

# 憑證端點API操作 {#credentials}

>[!IMPORTANT]
>
>**API端點**: `platform.adobe.io/data/core/activation/authoring/credentials`

此頁面列出並說明您可使用 `/authoring/credentials` API端點。

有關此端點支援的功能的說明，請參閱：

* [串流目的地設定](destination-configuration.md) 針對您可為串流目的地設定的功能。
* [基於檔案的目標配置](file-based-destination-configuration.md) 針對您可為檔案式目的地設定的功能。

## 何時使用 `/credentials` API端點 {#when-to-use}

>[!IMPORTANT]
>
>在大多數情況下，您 *不* 需要使用 `/credentials` API端點。 反之，您可以透過 `customerAuthenticationConfigurations` 參數 `/destinations` 端點。 閱讀 [驗證配置](./authentication-configuration.md#when-to-use) 以取得更多資訊。

使用此API端點並選取 `PLATFORM_AUTHENTICATION` 在 [目的地配置](./destination-configuration.md#destination-delivery) 如果Adobe與目的地之間有全域驗證系統，則 [!DNL Platform] 客戶不需要提供任何驗證憑證來連線至您的目的地。 在此情況下，您必須使用 `/credentials` API端點。

## 憑證設定API操作快速入門 {#get-started}

繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 若要成功呼叫API，需知的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 建立憑據配置 {#create}

您可以向發出POST要求，以建立新憑證設定 `/authoring/credentials` 端點。

**API格式**

```http
POST /authoring/credentials
```

**要求**

下列請求會建立新的憑證設定，由裝載中提供的參數所設定。 以下裝載包含接受的所有參數 `/authoring/credentials` 端點。 請注意，您不必在呼叫上新增所有參數，且可根據您的API需求自訂範本。

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
| `clientSecret` | 字串 | 客戶端/應用程式憑據的客戶端密碼 |
| `accessToken` | 字串 | 授權提供者提供的存取權杖 |
| `expiration` | 字串 | 存取權杖的存留時間 |
| `refreshToken` | 字串 | 授權提供者提供的重新整理Token |
| `header` | 字串 | 授權所需的任何標頭 |
| `accessId` | 字串 | Amazon S3存取ID |
| `secretKey` | 字串 | Amazon S3密鑰 |
| `sshKey` | 字串 | SSH驗證的SFTP SSH金鑰 |
| `tenant` | 字串 | Azure資料湖儲存租戶 |
| `servicePrincipalId` | 字串 | Azure資料湖儲存的Azure服務主體ID |
| `servicePrincipalKey` | 字串 | Azure資料湖儲存的Azure服務主密鑰 |
| `connectionString` | 字串 | Azure Blob儲存連接字串 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回HTTP狀態200，並包含新建立憑據組態的詳細資訊。

## 列出憑據配置 {#retrieve-list}

您可以向提出GET要求，以擷取IMS組織的所有認證設定清單 `/authoring/credentials` 端點。

**API格式**


```http
GET /authoring/credentials
```

**要求**

下列要求會根據IMS組織和沙箱設定，擷取您有權存取的認證設定清單。

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

下列回應會根據您使用的IMS組織ID和沙箱名稱，傳回HTTP狀態200，並列出您有權存取的憑證設定。 一 `instanceId` 與一個憑據配置的模板相對應。 回應會為簡潔而截斷。

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

您可以向發出PUT要求，以更新現有的憑證設定 `/authoring/credentials` 端點，並提供您要更新之憑證設定的執行個體ID。 在呼叫內文中，提供更新的憑證設定。

**API格式**


```http
PUT /authoring/credentials/{INSTANCE_ID}
```

| 參數 | 說明 |
| -------- | ----------- |
| `{INSTANCE_ID}` | 要更新的憑據配置的ID。 |

**要求**

下列要求會更新現有憑證設定，由裝載中提供的參數所設定。

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

您可以向提出GET要求，以擷取特定憑證設定的詳細資訊 `/authoring/credentials` 端點，並提供您要更新之憑證設定的執行個體ID。

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

成功的回應會傳回HTTP狀態200，其中包含指定憑證設定的詳細資訊。

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

您可以向發出DELETE要求，以刪除指定的憑證設定 `/authoring/credentials` 端點，並提供您要在請求路徑中刪除之憑證設定的ID。

**API格式**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 此 `id` 刪除的憑據配置。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的回應會傳回HTTP狀態200，並傳回空的HTTP回應。

## API錯誤處理

Destination SDKAPI端點遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱 [API狀態代碼](../../landing/troubleshooting.md#api-status-codes) 和 [請求標題錯誤](../../landing/troubleshooting.md#request-header-errors) （位於平台疑難排解指南中）。

## 後續步驟

閱讀本檔案後，您現在知道何時應使用憑證端點，以及如何使用 `/authoring/credentials` API端點或 `/authoring/destinations` 端點。 閱讀 [如何使用Destination SDK來設定您的目的地](./configure-destination-instructions.md) 了解此步驟在設定目的地程式中的適用位置。
