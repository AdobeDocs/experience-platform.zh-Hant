---
description: 本頁面說明您可以使用「/authoring/credentials」 API端點執行的所有API操作。
title: 憑證端點API操作
source-git-commit: 19307fba8f722babe5b6d57e80735ffde00fc851
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 4%

---

# 憑證端點API操作 {#credentials}

>[!IMPORTANT]
>
>**API端點**:  `platform.adobe.io/data/core/activation/authoring/credentials`

本頁列出並說明了所有可使用`/authoring/credentials` API端點執行的API操作。

## 何時使用`/credentials` API端點 {#when-to-use}

>[!IMPORTANT]
>
>在大多數情況下，您&#x200B;*不*&#x200B;需要使用`/credentials` API端點。 反之，您可以透過`/destinations`端點的`customerAuthenticationConfigurations`參數來設定目的地的驗證資訊。 如需詳細資訊，請參閱[憑據配置](./credentials-configuration.md)。

如果Adobe與目的地之間有全域驗證系統，且[!DNL Platform]客戶不需要提供任何驗證憑證來連線至您的目的地，請使用此API端點，並在[目的地設定](./destination-configuration.md#destination-delivery)中選取`PLATFORM_AUTHENTICATION`。 在此情況下，您必須使用`/credentials` API端點建立憑證物件。

<!--

Commenting out the example configurations

## Example configurations

**Example configuration for a Basic authentication credential configuration with username and password**

```json
{
  "type": "BASIC",
  "name": "YOUR_DESTINATION_NAME",
  "basicAuthentication": {
    "username": "YOUR_DESTINATION_SERVER_USERNAME",
    "password": "YOUR_DESTINATION_SERVER_PASSWORD"
  }
}

```

**Example configuration for an OAuth2 credential configuration**

```json

{
  "oauth2AccessTokenAuthentication": {
    "accessToken": "YOUR_DESTINATION_SERVER_ACCESS_TOKEN",
    "expiration": "YOUR_TOKEN_TIME_TO_LIVE",
    "username": "YOUR_DESTINATION_SERVER_USERNAME",
    "userId": "YOUR_DESTINATION_USER_ID",
    "url": "AUTHORIZATION_PROVIDER_URL",
    "header": "YOUR_AUTHORIZATION_HEADER"
  }
}

```

The sections below list out the necessary parameters for each authentication type. Let us know which authentication type your server uses and provide us with the relevant information for your server type.

## Basic authentication

|Parameter | Type | Description|
|---------|----------|------|
|`username` | String | credentials configuration login username |
|`password` | String | credentials configuration login password |



// commenting out this part as these types of authentication methods are not supported in phase one

### S3 authentication

|Parameter | Type | Description|
|---------|----------|------|
|accessId | String | credentials configuration S3 credential Access key ID |
|secretKey | String | credentials configuration S3 credential Secret key |

### SSH 

|Parameter | Type | Description|
|---------|----------|------|
|username | String | credentials configuration SSH username |
|SSHKey | String | credentials configuration SSH key |



## OAuth1

|Parameter | Type | Description|
|---------|----------|------|
|`apiKey` | String | A value used by the Destinations Service to identify itself to the Service Provider. |
|`apiSecret` | String | Secret used by the Destinations Service to establish ownership of the API key to the Service Provider. |
|`acccessToken` | String | A value used by the Destinations Service to gain access to the Protected Resources on behalf of the User |
|`tokenSecret` | String | A secret used by the Destinations Service to establish ownership of an access token. |

## OAuth2 user credentials

|Parameter | Type | Description|
|---------|----------|------|
|`clientId` | String | Client ID of Client/Application credential |
|`clientSecret` | String | Client secret of Client/Application credential |
|`username` | String | The user's username to log on to your platform. |
|`password` | String | The user's password to log on to your platform. |
|`url` | String | URL of authorization provider |
|`header` | String | Any header required for authorization |

## OAuth2 client credentials

|Parameter | Type | Description|
|---------|----------|------|
|`clientId` | String | Client ID of Client/Application credential |
|`clientSecret` | String | Client secret of Client/Application credential |
|`username`| String | URL of authorization provider |
|`password` | String | Any header required for authorization |

## OAuth2 access token

|Parameter | Type | Description|
|---------|----------|------|
|`accessToken` | String | Access token provided by the authorization provider |
|`expiration` | String | The time-to-live for the access token |
|`username` | String | The user's username to log on to your platform. |
|`userId` | String | The user's ID with your platform. |
|`url` | String | URL of authorization provider |
|`header` | String | Any header required for authorization |

## OAuth2 refresh token

|Parameter | Type | Description|
|---------|----------|------|
|`clientId` | String | Client ID of Client/Application credential |
|`clientSecret` | String | Client secret of Client/Application credential |
|`refreshToken` | String | Refresh token provided by the authorization provider |
|`url` | String | URL of authorization provider |
|`expiration` | String | The time-to-live for the refresh token |
|`header` | String | Any header required for authorization |

-->

## 憑證設定API操作快速入門 {#get-started}

繼續之前，請檢閱[快速入門手冊](./getting-started.md)，以取得成功呼叫API所需的重要資訊，包括如何取得必要的目的地編寫權限和必要的標題。

## 建立憑據配置 {#create}

您可以向`/authoring/credentials`端點發出POST請求，以建立新的憑據配置。

**API格式**


```http
POST /authoring/credentials
```

**要求**

下列請求會建立新的憑證設定，由裝載中提供的參數所設定。 以下裝載包含`/authoring/credentials`端點接受的所有參數。 請注意，您不必在呼叫上新增所有參數，且可根據您的API需求自訂範本。

```shell
curl -X POST https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

{style=&quot;table-layout:auto&quot;}

**回應**

成功的回應會傳回HTTP狀態200，並包含新建立憑據組態的詳細資訊。

## 列出憑據配置 {#retrieve-list}

您可以向`/authoring/credentials`端點提出GET要求，以擷取IMS組織的所有憑證設定清單。

**API格式**


```http
GET /authoring/credentials
```

**要求**

下列要求會根據IMS組織和沙箱設定，擷取您有權存取的認證設定清單。

```shell
curl -X GET https://platform.adobe.io/data/core/activation/authoring/credentials \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

下列回應會根據您使用的IMS組織ID和沙箱名稱，傳回HTTP狀態200，並列出您有權存取的憑證設定。 一個`instanceId`對應於一個憑據配置的模板。 回應會為簡潔而截斷。

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

通過向`/authoring/credentials`端點發出PUT請求並提供要更新的憑據配置的實例ID，可以更新現有憑據配置。 在呼叫內文中，提供更新的憑證設定。

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
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

通過向`/authoring/credentials`端點發出GET請求並提供要更新的憑據配置的實例ID，可以檢索有關特定憑據配置的詳細資訊。

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
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
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

通過向`/authoring/credentials`端點發出DELETE請求並在請求路徑中提供要刪除的憑據配置的ID，可以刪除指定的憑據配置。

**API格式**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| 參數 | 說明 |
| --------- | ----------- |
| `{INSTANCE_ID}` | 要刪除的憑據配置的`id`。 |

**要求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/n55affa0-3747-4030-895d-1d1236bb3680 \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的回應會傳回HTTP狀態200，並傳回空的HTTP回應。

## API錯誤處理

目標SDK API端點會遵循一般Experience PlatformAPI錯誤訊息原則。 請參閱平台疑難排解指南中的[API狀態代碼](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#api-status-codes)和[要求標題錯誤](https://experienceleague.adobe.com/docs/experience-platform/landing/troubleshooting.html?lang=en#request-header-errors)。

## 後續步驟

閱讀本檔案後，您現在知道何時使用憑證端點，以及如何使用`/authoring/credentials` API端點或`/authoring/destinations`端點設定憑證設定。 請參閱[如何使用目標SDK來設定目標](./configure-destination-instructions.md) ，了解此步驟在設定目標程式中的適用位置。
