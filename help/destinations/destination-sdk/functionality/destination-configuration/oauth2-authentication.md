---
description: 本頁介紹了Destination SDK支援的各種OAuth 2身份驗證流，並提供了為目標設定OAuth 2身份驗證的說明。
title: OAuth 2身份驗證
exl-id: 280ecb63-5739-491c-b539-3c62bd74e433
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '2155'
ht-degree: 4%

---

# OAuth 2身份驗證

Destination SDK支援多種到目標的身份驗證方法。 其中包括使用 [OAuth 2驗證框架](https://tools.ietf.org/html/rfc6749)。

本頁介紹了Destination SDK支援的各種OAuth 2身份驗證流，並提供了為目標設定OAuth 2身份驗證的說明。

>[!IMPORTANT]
>
>Destination SDK支援的所有參數名和值均 **區分大小寫**。 為避免區分大小寫錯誤，請完全按文檔所示使用參數名稱和值。

## 支援的整合類型 {#supported-integration-types}

有關哪些類型的整合支援本頁所述功能的詳細資訊，請參閱下表。

| 整合類型 | 支援功能 |
|---|---|
| 即時（流）整合 | 是 |
| 基於檔案（批處理）的整合 | 無 |

## 如何將OAuth 2身份驗證詳細資訊添加到目標配置 {#how-to-setup}

### 系統中的先決條件 {#prerequisites}

作為第一步，您必須在系統中為Adobe Experience Platform建立應用，或在系統中註冊Experience Platform。 目標是生成客戶端ID和客戶端密碼，這是驗證到目標的Experience Platform所需的。 作為系統中此配置的一部分，您需要Adobe Experience PlatformOAuth 2重定向/回叫URL，您可以從下面的清單中獲取該URL。

* `https://platform-va7.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-nld2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-aus5.adobe.io/data/core/activation/oauth/api/v1/callback`

>[!IMPORTANT]
>
>在系統中註冊Adobe Experience Platform的重定向/回叫URL的步驟僅對於 [OAuth 2，帶授權碼](oauth2-authentication.md#authorization-code) 授予類型。 對於其他兩種支援的授權類型（密碼和客戶端憑據），可跳過此步驟。

在此步驟的結束時，您應：
* 客戶端ID;
* 客戶機密；
* Adobe的回調URL（用於授權代碼授予）。

### 你在Destination SDK {#to-do-in-destination-sdk}

要在Experience Platform中設定目標的OAuth 2身份驗證，必須將OAuth 2詳細資訊添加到 [目標配置](../../authoring-api/destination-configuration/create-destination-configuration.md)，也請參見Wiki頁。 `customerAuthenticationConfigurations` 的下界。 請參閱 [客戶驗證](../../functionality/destination-configuration/customer-authentication.md) 的上界。 本頁的下面進一步介紹了您需要將哪些欄位添加到配置模板（具體取決於您的OAuth 2身份驗證授權類型）。

## 支援的OAuth 2授權類型 {#oauth2-grant-types}

Experience Platform支援下表中的三種OAuth 2授權類型。 如果您有自定義OAuth 2安裝程式，Adobe可以借助整合中的自定義欄位來支援它。 有關詳細資訊，請參閱每個授權類型的部分。

>[!IMPORTANT]
>
>* 按照以下各節的說明提供輸入參數。 Adobe — 內部系統連接到平台的驗證系統並獲取輸出參數，這些參數用於驗證用戶並維護到目標的驗證。
>* 在表中以粗體突出顯示的輸入參數是OAuth 2驗證流中所需的參數。 其他參數是可選的。 此處未顯示其他自定義輸入參數，但這些參數在各節中長度描述 [自定義OAuth 2配置](#customize-configuration) 和 [訪問令牌刷新](#access-token-refresh)。


| OAuth 2授予 | 輸入 | 輸出 |
|---------|----------|---------|
| 授權代碼 | <ul><li><b>客戶端ID</b></li><li><b>客戶機密鑰</b></li><li>範圍</li><li><b>授權URL</b></li><li><b>accessTokenUrl</b></li><li>刷新令牌URL</li></ul> | <ul><li><b>訪問令牌</b></li><li>過期時間</li><li>刷新令牌</li><li>tokenType</li></ul> |
| 密碼 | <ul><li><b>客戶端ID</b></li><li><b>客戶機密鑰</b></li><li>範圍</li><li><b>accessTokenUrl</b></li><li><b>用戶名</b></li><li><b>密碼</b></li></ul> | <ul><li><b>訪問令牌</b></li><li>過期時間</li><li>刷新令牌</li><li>tokenType</li></ul> |
| 客戶端憑據 | <ul><li><b>客戶端ID</b></li><li><b>客戶機密鑰</b></li><li>範圍</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>訪問令牌</b></li><li>過期時間</li><li>刷新令牌</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

上表列出了標準OAuth 2流中使用的欄位。 除了這些標準欄位外，各種合作夥伴整合可能需要額外的輸入和輸出。 Adobe為Destination SDK設計了一個靈活的OAuth 2驗證/授權框架，該框架可處理對上述標準欄位模式的變化，同時支援自動重新生成無效輸出的機制，如過期的訪問令牌。

所有情況下的輸出都包括訪問令牌，該令牌由Experience Platform用來驗證和維護對目標的驗證。

Adobe為OAuth 2身份驗證設計的系統：
* 支援所有三個OAuth 2授權，同時考慮其中的任何變化，如附加資料欄位、非標準API調用等。
* 支援具有不同生存期值（無論是90天、30分鐘還是您指定的任何其他生存期值）的訪問令牌。
* 支援帶刷新令牌或不帶刷新令牌的OAuth 2授權流。

## OAuth 2，帶授權碼 {#authorization-code}

如果目標支援標準OAuth 2.0授權碼流(請閱讀 [RFC標準規範](https://tools.ietf.org/html/rfc6749#section-4.1))或其變體，請參閱以下必需欄位和可選欄位：

| OAuth 2授予 | 輸入 | 輸出 |
|---------|----------|---------|
| 授權代碼 | <ul><li><b>客戶端ID</b></li><li><b>客戶機密鑰</b></li><li>範圍</li><li><b>授權URL</b></li><li><b>accessTokenUrl</b></li><li>刷新令牌URL</li></ul> | <ul><li><b>訪問令牌</b></li><li>過期時間</li><li>刷新令牌</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

要為目標設定此身份驗證方法，請在配置中添加以下行 [建立目標配置](../../authoring-api/destination-configuration/create-destination-configuration.md):

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_AUTHORIZATION_CODE",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "authorizationUrl": "https://www.moviestar.com/dialog/OAuth",
      "refreshTokenUrl": "https://api.moviestar.com/OAuth/refresh_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
//...
}
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `authType` | 字串 | 使用「OAUTH2」。 |
| `grant` | 字串 | 使用&quot;OAUTH2_AUTHORIZATION_CODE&quot;。 |
| `accessTokenUrl` | 字串 | 您一方的URL，它發出訪問令牌，並（可選）刷新令牌。 |
| `authorizationUrl` | 字串 | 授權伺服器的URL，在該URL中，您將用戶重定向到您的應用程式。 |
| `refreshTokenUrl` | 字串 | *選填.* 發出刷新令牌的URL。 通常， `refreshTokenUrl` 與 `accessTokenUrl`。 |
| `clientId` | 字串 | 您的系統分配給Adobe Experience Platform的客戶端ID。 |
| `clientSecret` | 字串 | 你的系統給Adobe Experience Platform分配的客戶機機密。 |
| `scope` | 字串清單 | *可選*. 設定訪問令牌允許Experience Platform對資源執行的作用域。 示例：「讀，寫」。 |

{style="table-layout:auto"}

## OAuth 2，帶密碼授權

對於OAuth 2密碼授予(請閱讀 [RFC標準規範](https://tools.ietf.org/html/rfc6749#section-4.3)),Experience Platform需要用戶的用戶名和密碼。 在驗證流中，Experience Platform將這些憑據交換為訪問令牌和可選地刷新令牌。
Adobe利用以下標準輸入簡化目標配置，並能夠覆蓋值：

| OAuth 2授予 | 輸入 | 輸出 |
|---------|----------|---------|
| 密碼 | <ul><li><b>客戶端ID</b></li><li><b>客戶機密鑰</b></li><li>範圍</li><li><b>accessTokenUrl</b></li><li><b>用戶名</b></li><li><b>密碼</b></li></ul> | <ul><li><b>訪問令牌</b></li><li>過期時間</li><li>刷新令牌</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

>[!NOTE]
>
> 您不需要為 `username` 和 `password` 的下界。 添加時 `"grant": "OAUTH2_PASSWORD"` 在目標配置中，當用戶對目標進行身份驗證時，系統將請求用戶在Experience PlatformUI中提供用戶名和密碼。

要為目標設定此身份驗證方法，請在配置中添加以下行 [建立目標配置](../../authoring-api/destination-configuration/create-destination-configuration.md):

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_PASSWORD",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `authType` | 字串 | 使用「OAUTH2」。 |
| `grant` | 字串 | 使用「OAUTH2_PASSWORD」。 |
| `accessTokenUrl` | 字串 | 您一方的URL，它發出訪問令牌，並（可選）刷新令牌。 |
| `clientId` | 字串 | 您的系統分配給Adobe Experience Platform的客戶端ID。 |
| `clientSecret` | 字串 | 你的系統給Adobe Experience Platform分配的客戶機機密。 |
| `scope` | 字串清單 | *可選*. 設定訪問令牌允許Experience Platform對資源執行的作用域。 示例：「讀，寫」。 |

{style="table-layout:auto"}

## 具有客戶端憑據授予的OAuth 2

您可以配置OAuth 2客戶端憑據(請閱讀 [RFC標準規範](https://tools.ietf.org/html/rfc6749#section-4.4))目的地，支援下面列出的標準輸入和輸出。 您可以自定義值。 請參閱 [自定義OAuth 2配置](#customize-configuration) 的雙曲餘切值。

| OAuth 2授予 | 輸入 | 輸出 |
|---------|----------|---------|
| 客戶端憑據 | <ul><li><b>客戶端ID</b></li><li><b>客戶機密鑰</b></li><li>範圍</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>訪問令牌</b></li><li>過期時間</li><li>刷新令牌</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

要為目標設定此身份驗證方法，請在配置中添加以下行 [建立目標配置](../../authoring-api/destination-configuration/create-destination-configuration.md):

```json
{
//...
  "customerAuthenticationConfigurations": [
    {
      "authType": "OAUTH2",
      "grant": "OAUTH2_CLIENT_CREDENTIALS",
      "accessTokenUrl": "https://api.moviestar.com/OAuth/access_token",
      "refreshTokenUrl": "https://api.moviestar.com/OAuth/refresh_token",
      "clientId": "Experience-Platform-client-id",
      "clientSecret": "Experience-Platform-client-secret",
      "scope": ["read", "write"]
    }
  ]
//...
}
```

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `authType` | 字串 | 使用「OAUTH2」。 |
| `grant` | 字串 | 使用「OAUTH2_CLIENT_CREDENTIALS」。 |
| `accessTokenUrl` | 字串 | 授權伺服器的URL，它發出訪問令牌和可選刷新令牌。 |
| `refreshTokenUrl` | 字串 | *選填.* 發出刷新令牌的URL。 通常， `refreshTokenUrl` 與 `accessTokenUrl`。 |
| `clientId` | 字串 | 您的系統分配給Adobe Experience Platform的客戶端ID。 |
| `clientSecret` | 字串 | 你的系統給Adobe Experience Platform分配的客戶機機密。 |
| `scope` | 字串清單 | *可選*. 設定訪問令牌允許Experience Platform對資源執行的作用域。 示例：「讀，寫」。 |

{style="table-layout:auto"}

## 自定義OAuth 2配置 {#customize-configuration}

以上各節中描述的配置描述了標準OAuth 2授權。 但是，通過Adobe設計的系統提供了靈活性，因此您可以對OAuth 2授權中的任何變體使用自定義參數。 要自定義標準OAuth 2設定，請使用 `authenticationDataFields` 參數，如下例所示。

### 示例1:使用 `authenticationDataFields` 捕獲來自身份驗證響應的資訊 {#example-1}

在本示例中，目標平台具有在一定時間後過期的刷新令牌。 在這種情況下，合作夥伴將 `refreshTokenExpiration` 自定義欄位，從 `refresh_token_expires_in` 欄位。

```json
{
   "customerAuthenticationConfigurations":[
      {
         "authType":"OAUTH2",
         "options":{
            
         },
         "grant":"OAUTH2_AUTHORIZATION_CODE",
         "accessTokenUrl":"https://api.moviestar.com/OAuth/access_token",
         "authorizationUrl":"https://api.moviestar.com/OAuth/authorization",
         "scope":[
            "read",
            "write",
            "delete"
         ],
         "refreshTokenUrl":"https://api.moviestar.com/OAuth/accessToken",
         "clientSecret":"client-secret-here",
         "authenticationDataFields":[
            {
               "name":"refreshTokenExpiration",
               "title":"Refresh Token Expires In",
               "description":"Time in seconds when the refresh token will expire",
               "type":"string",
               "isRequired":false,
               "source":"CUSTOMER",
               "authenticationResponsePath":"refresh_token_expires_in"
            }
         ]
      }
   ]
}  
```

### 示例2:使用 `authenticationDataFields` 提供特殊刷新令牌 {#example-2}

在本示例中，合作夥伴設定其目標以提供特殊刷新令牌。 此外，訪問令牌的到期日期在API響應中不返回，因此它們可以硬編碼預設值，在這種情況下為3600秒。

```json
      "authenticationDataFields": [
        {
            "name": "refreshToken",
            "value": "special_refresh_token"
        },
        {
            "name": "expiresIn",
            "value": 3600
        } 
      ]
```

### 示例3:用戶在配置目標時輸入客戶端ID和客戶端機密 {#example-3}

在本示例中，不是建立全局客戶端ID和客戶端機密，如一節所示 [系統中的先決條件](#prerequisites)，客戶需要輸入客戶端ID、客戶機密碼和帳戶ID（客戶用於登錄到目標的ID）

```json
{
    //...
    "customerAuthenticationConfigurations": [
        {
            "authType": "OAUTH2",
            "grant": "OAUTH2_CLIENT_CREDENTIALS",
            "authenticationDataFields": [
                {
                    "name": "clientId",
                    "title": "Client ID",
                    "description": "Client ID",
                    "type": "string",
                    "isRequired": true,
                    "source": "CUSTOMER"
                },
                {
                    "name": "clientSecret",
                    "title": "Client Secret",
                    "description": "Client Secret",
                    "type": "string",
                    "isRequired": true,
                    "format": "password",
                    "source": "CUSTOMER"
                },
                {
                    "name": "moviestarId",
                    "title": "Moviestar ID",
                    "description": "Moviestar ID",
                    "type": "string",
                    "isRequired": true,
                    "source": "CUSTOMER"
                }
            ],
            "accessTokenRequest": {
                "destinationServerType": "URL_BASED",
                "urlBasedDestination": {
                    "url": {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "https://{{ authData.moviestarId }}.yourdestination.com/identity/oauth/token"
                    }
                },
                "httpTemplate": {
                    "requestBody": {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ formUrlEncode('grant_type', 'client_credentials', 'client_id', authData.clientId, 'client_secret', authData.clientSecret) | raw }}"
                    },
                    "httpMethod": "POST",
                    "contentType": "application/x-www-form-urlencoded"
                },
                "responseFields": [
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.access_token }}",
                        "name": "accessToken"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.scope }}",
                        "name": "scope"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.token_type }}",
                        "name": "tokenType"
                    },
                    {
                        "templatingStrategy": "PEBBLE_V1",
                        "value": "{{ response.body.expires_in }}",
                        "name": "expiresIn"
                    }
                ]
            }
        }
    ]
//...
}
```



可在 `authenticationDataFields` 自定義OAuth 2配置：

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `authenticationDataFields.name` | 字串 | 自定義欄位的名稱。 |
| `authenticationDataFields.title` | 字串 | 可為自定義欄位提供的標題。 |
| `authenticationDataFields.description` | 字串 | 您設定的自定義資料欄位的說明。 |
| `authenticationDataFields.type` | 字串 | 定義自定義資料欄位的類型。 <br> 接受的值： `string`。 `boolean`。 `integer` |
| `authenticationDataFields.isRequired` | 布林值 | 指定驗證流中是否需要自定義資料欄位。 |
| `authenticationDataFields.format` | 字串 | 選擇時 `"format":"password"`,Adobe加密驗證資料欄位的值。 當與 `"fieldType": "CUSTOMER"`，當用戶在欄位中鍵入內容時，還會隱藏UI中的輸入。 |
| `authenticationDataFields.fieldType` | 字串 | 指示輸入是來自合作夥伴（您）還是來自用戶，當他們以Experience Platform設定目標時。 |
| `authenticationDataFields.value` | 字串. 布林值. 整數 | 自定義資料欄位的值。 值與所選類型匹配 `authenticationDataFields.type`。 |
| `authenticationDataFields.authenticationResponsePath` | 字串 | 指示您正在引用的API響應路徑中的欄位。 |

{style="table-layout:auto"}

## 訪問令牌刷新 {#access-token-refresh}

Adobe設計了一種系統，該系統可刷新過期的訪問令牌，而不要求用戶重新登錄到您的平台。 系統能夠生成新令牌，以便客戶可以無縫地繼續激活到目標。

要設定訪問令牌刷新，您可能需要配置模板化HTTP請求，該請求允許Adobe使用刷新令牌獲取新的訪問令牌。 如果訪問令牌已過期，Adobe將獲取您提供的模板化請求，並添加您提供的參數。 使用 `accessTokenRequest` 參數以配置訪問令牌刷新機制。


```json
{
   "customerAuthenticationConfigurations":[
      {
         "authType":"OAUTH2",
         "grant":"OAUTH2_CLIENT_CREDENTIALS",
         "accessTokenRequest":{
            "destinationServerType":"URL_BASED",
            "urlBasedDestination":{
               "url":{
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"https://{{authData.customerId}}.yourdestination.com/identity/oauth/token"
               }
            },
            "httpTemplate":{
               "requestBody":{
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ formUrlEncode('grant_type', 'client_credentials', 'client_id', authData.clientId, 'client_secret', authData.clientSecret) | raw }}"
               },
               "httpMethod":"POST",
               "contentType":"application/x-www-form-urlencoded",
               "headers":[
                  
               ]
            },
            "responseFields":[
               {
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ response.body.expires_in }}",
                  "name":"expiresIn"
               },
               {
                  "templatingStrategy":"PEBBLE_V1",
                  "value":"{{ response.body.access_token }}",
                  "name":"accessToken"
               }
            ],
            "validations":[
               {
                  "name":"access_token validation",
                  "actualValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"{{response.body.access_token is empty }}"
                  },
                  "expectedValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"false"
                  }
               },
               {
                  "name":"response status",
                  "actualValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"{{ response.status }}"
                  },
                  "expectedValue":{
                     "templatingStrategy":"PEBBLE_V1",
                     "value":"200"
                  }
               }
            ]
         }
      }
   ]
}
```

可在 `accessTokenRequest` 要自定義令牌刷新過程，請執行以下操作：

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `accessTokenRequest.destinationServerType` | 字串 | 使用 `URL_BASED`. |
| `accessTokenRequest.urlBasedDestination.url.templatingStrategy` | 字串 | <ul><li>使用 `PEBBLE_V1` 如果在中使用模板 `accessTokenRequest.urlBasedDestination.url.value`。</li><li> 使用 `NONE` 欄位中的值 `accessTokenRequest.urlBasedDestination.url.value` 是常數。 </li></li> |
| `accessTokenRequest.urlBasedDestination.url.value` | 字串 | Experience Platform請求訪問令牌的URL。 |
| `accessTokenRequest.httpTemplate.requestBody.templatingStrategy` | 字串 | <ul><li>使用 `PEBBLE_V1` 如果在 `accessTokenRequest.httpTemplate.requestBody.value`。</li><li> 使用 `NONE` 欄位中的值 `accessTokenRequest.httpTemplate.requestBody.value` 是常數。 </li></li> |
| `accessTokenRequest.httpTemplate.requestBody.value` | 字串 | 使用模板語言對訪問令牌端點的HTTP請求中的欄位進行自定義。 有關如何使用模板自定義欄位的資訊，請參閱 [模板公約](#templating-conventions) 的子菜單。 |
| `accessTokenRequest.httpTemplate.httpMethod` | 字串 | 指定用於調用訪問令牌終結點的HTTP方法。 在大多數情況下，此值 `POST`。 |
| `accessTokenRequest.httpTemplate.contentType` | 字串 | 指定訪問令牌終結點的HTTP調用的內容類型。 <br> 例如： `application/x-www-form-urlencoded` 或 `application/json`。 |
| `accessTokenRequest.httpTemplate.headers` | 字串 | 指定是否應將任何標頭添加到訪問令牌終結點的HTTP調用中。 |
| `accessTokenRequest.responseFields.templatingStrategy` | 字串 | <ul><li>使用 `PEBBLE_V1` 如果在 `accessTokenRequest.responseFields.value`。</li><li> 使用 `NONE` 欄位中的值 `accessTokenRequest.responseFields.value` 是常數。 </li></li> |
| `accessTokenRequest.responseFields.value` | 字串 | 使用模板語言從訪問令牌端點訪問HTTP響應中的欄位。 有關如何使用模板自定義欄位的資訊，請參閱 [模板公約](#templating-conventions) 的子菜單。 |
| `accessTokenRequest.validations.name` | 字串 | 指示為此驗證提供的名稱。 |
| `accessTokenRequest.validations.actualValue.templatingStrategy` | 字串 | <ul><li>使用 `PEBBLE_V1` 如果在 `accessTokenRequest.validations.actualValue.value`。</li><li> 使用 `NONE` 欄位中的值 `accessTokenRequest.validations.actualValue.value` 是常數。 </li></li> |
| `accessTokenRequest.validations.actualValue.value` | 字串 | 使用模板語言訪問HTTP響應中的欄位。 有關如何使用模板自定義欄位的資訊，請參閱 [模板公約](#templating-conventions) 的子菜單。 |
| `accessTokenRequest.validations.expectedValue.templatingStrategy` | 字串 | <ul><li>使用 `PEBBLE_V1` 如果在 `accessTokenRequest.validations.expectedValue.value`。</li><li> 使用 `NONE` 欄位中的值 `accessTokenRequest.validations.expectedValue.value` 是常數。 </li></li> |
| `accessTokenRequest.validations.expectedValue.value` | 字串 | 使用模板語言訪問HTTP響應中的欄位。 有關如何使用模板自定義欄位的資訊，請參閱 [模板公約](#templating-conventions) 的子菜單。 |

{style="table-layout:auto"}

## 模板約定 {#templating-conventions}

根據身份驗證自定義，您可能需要訪問身份驗證響應中的資料欄位，如上一節所示。 為此，請熟悉 [卵石模板語言](https://pebbletemplates.io/) 用於Adobe，並參考以下模板約定來自定義OAuth 2實施。


| 前置詞 | 說明 | 範例 |
|---------|----------|---------|
| 驗證資料 | 訪問任何合作夥伴或客戶資料欄位的值。 | ``{{ authData.accessToken }}`` |
| response.body | HTTP響應體 | ``{{ response.body.access_token }}`` |
| response.status | HTTP響應狀態 | ``{{ response.status }}`` |
| response.headers | HTTP響應標頭 | ``{{ response.headers.server[0] }}`` |
| 用戶上下文 | 訪問有關當前身份驗證嘗試的資訊 | <ul><li>`{{ userContext.sandboxName }} `</li><li>`{{ userContext.sandboxId }} `</li><li>`{{ userContext.imsOrgId }} `</li><li>`{{ userContext.client }} // the client executing the authentication attempt `</li></ul> |

{style="table-layout:auto"}

## 後續步驟 {#next-steps}

通過閱讀本文，您現在瞭解了Adobe Experience Platform支援的OAuth 2身份驗證模式，並知道如何使用OAuth 2身份驗證支援配置目標。 接下來，您可以使用Destination SDK設定OAuth 2支援的目標。 閱讀 [使用Destination SDK配置目標](../../guides/configure-destination-instructions.md) 的子菜單。
