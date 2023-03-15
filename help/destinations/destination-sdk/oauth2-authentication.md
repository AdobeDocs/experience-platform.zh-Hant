---
description: 本頁說明Destination SDK支援的各種OAuth 2驗證流程，並提供針對您目的地設定OAuth 2驗證的指示。
title: OAuth 2驗證
exl-id: 280ecb63-5739-491c-b539-3c62bd74e433
source-git-commit: 87fb3ffa65449b61e05d94d2b56daf727ecebdea
workflow-type: tm+mt
source-wordcount: '2080'
ht-degree: 4%

---

# OAuth 2驗證

## 總覽 {#overview}

使用Destination SDK來允許Adobe Experience Platform使用 [OAuth 2驗證架構](https://tools.ietf.org/html/rfc6749).

本頁說明Destination SDK支援的各種OAuth 2驗證流程，並提供針對您目的地設定OAuth 2驗證的指示。

## 如何將OAuth 2驗證詳細資料新增至您的目的地設定 {#how-to-setup}

### 系統的必要條件 {#prerequisites}

首先，您必須在系統中建立Adobe Experience Platform的應用程式，或在系統中註冊Experience Platform。 目標是產生用戶端ID和用戶端密碼，這是驗證Experience Platform至您目的地所需的工具。 在您的系統中執行此設定時，您需要Adobe Experience Platform OAuth 2重新導向/回呼URL，可從下列清單取得。

* `https://platform-va7.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-nld2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-aus5.adobe.io/data/core/activation/oauth/api/v1/callback`

>[!IMPORTANT]
>
>在您的系統中註冊Adobe Experience Platform的重新導向/回呼URL的步驟，僅是 [OAuth 2，含授權碼](./oauth2-authentication.md#authorization-code) 授權類型。 對於其他兩種支援的授權類型（密碼和客戶端憑據），您可以跳過此步驟。

在此步驟結束時，您應：
* 用戶端ID;
* 客戶機密；
* Adobe的回呼URL（用於授權程式碼授權）。

### 您需要在Destination SDK {#to-do-in-destination-sdk}

若要以Experience Platform設定目的地的OAuth 2驗證，您必須將OAuth 2詳細資料新增至 [目的地配置](./destination-configuration.md)，在 `customerAuthenticationConfigurations` 參數，使用 `platform.adobe.io/data/core/activation/authoring/destinations` [API端點](./destination-configuration-api.md). 請參閱 [範例設定](./destination-configuration.md#example-configuration). 本頁下方會根據您的OAuth 2驗證授權類型，說明您需要新增哪些欄位至設定範本的具體指示。

## 支援的OAuth 2授權類型 {#oauth2-grant-types}

Experience Platform支援下表中的三種OAuth 2授權類型。 如果您有自訂OAuth 2設定，Adobe便能在整合的自訂欄位協助下支援。 如需詳細資訊，請參閱每個授權類型的區段。

>[!IMPORTANT]
>
>* 您提供輸入參數，如以下各節所述。 Adobe內部系統會連線至您平台的驗證系統，並抓取輸出參數，這些參數用來驗證使用者並維護對您目的地的驗證。
>* 表格中以粗體強調顯示的輸入參數是OAuth 2驗證流程中的必要參數。 其他參數為選用。 此處未顯示其他自訂輸入參數，但各節中會詳細說明這些參數的長度 [自訂您的OAuth 2設定](./oauth2-authentication.md#customize-configuration) 和 [存取權杖重新整理](./oauth2-authentication.md#access-token-refresh).


| OAuth 2授予 | 輸入 | 輸出 |
|---------|----------|---------|
| 授權碼 | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>範圍</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>過期時間</li><li>refreshToken</li><li>tokenType</li></ul> |
| 密碼 | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>範圍</li><li><b>accessTokenUrl</b></li><li><b>用戶名</b></li><li><b>密碼</b></li></ul> | <ul><li><b>accessToken</b></li><li>過期時間</li><li>refreshToken</li><li>tokenType</li></ul> |
| 客戶端憑據 | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>範圍</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>過期時間</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

上表列出標準OAuth 2流量中使用的欄位。 除了這些標準欄位外，各種合作夥伴整合可能需要額外的輸入和輸出。 Adobe為Destination SDK設計了彈性的OAuth 2驗證/授權架構，可處理上述標準欄位模式的變化，同時支援自動重新產生無效輸出的機制，例如過期的存取權杖。

在所有情況下，輸出都包含存取權杖，供Experience Platform用來驗證和維護對您目的地的驗證。

Adobe為OAuth 2驗證而設計的系統：
* 支援所有三個OAuth 2授予，同時考慮其中的任何變數，例如其他資料欄位、非標準API呼叫等。
* 支援使用不同期限值的存取權杖，無論是90天、30分鐘，或您指定的任何其他期限值皆可。
* 支援使用或不使用重新整理Token的OAuth 2授權流程。

## OAuth 2，含授權碼 {#authorization-code}

如果您的目的地支援標準OAuth 2.0授權碼流程(請閱讀 [RFC標準規格](https://tools.ietf.org/html/rfc6749#section-4.1))或變數，請參閱下列必填和選填欄位：

| OAuth 2授予 | 輸入 | 輸出 |
|---------|----------|---------|
| 授權碼 | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>範圍</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>過期時間</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

若要為您的目的地設定此驗證方法，請在 `/destinations` [端點](./destination-configuration.md):

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
| `authType` | 字串 | 使用&quot;OAUTH2&quot;。 |
| `grant` | 字串 | 使用&quot;OAUTH2_AUTHORIZATION_CODE&quot;。 |
| `accessTokenUrl` | 字串 | 您這邊的URL會發出存取權杖，並選擇性地重新整理權杖。 |
| `authorizationUrl` | 字串 | 授權伺服器的URL，您會將使用者重新導向以登入您的應用程式。 |
| `refreshTokenUrl` | 字串 | *選填.* 您這邊的URL會發生重新整理Token的問題。 通常， `refreshTokenUrl` 與 `accessTokenUrl`. |
| `clientId` | 字串 | 您的系統指派給Adobe Experience Platform的用戶端ID。 |
| `clientSecret` | 字串 | 您的系統指派給Adobe Experience Platform的用戶端密碼。 |
| `scope` | 字串清單 | *可選*. 設定存取權杖可讓Experience Platform對您的資源執行之作業的範圍。 範例：「讀，寫」。 |

{style="table-layout:auto"}

## OAuth 2（含密碼授予）

OAuth 2密碼授予(請閱讀 [RFC標準規格](https://tools.ietf.org/html/rfc6749#section-4.3))，則Experience Platform需要使用者的使用者名稱和密碼。 在驗證流程中，Experience Platform會交換這些憑證以取得存取權杖，並選擇性地交換重新整理權杖。
Adobe利用以下標準輸入來簡化目標配置，並能覆寫值：

| OAuth 2授予 | 輸入 | 輸出 |
|---------|----------|---------|
| 密碼 | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>範圍</li><li><b>accessTokenUrl</b></li><li><b>用戶名</b></li><li><b>密碼</b></li></ul> | <ul><li><b>accessToken</b></li><li>過期時間</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

>[!NOTE]
>
> 您不需要為 `username` 和 `password` 在下列設定中。 新增 `"grant": "OAUTH2_PASSWORD"` 在目標配置中，當使用者驗證您的目標時，系統會要求使用者在Experience PlatformUI中提供使用者名稱和密碼。

若要為您的目的地設定此驗證方法，請在 `/destinations` [端點](./destination-configuration.md):

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
| `authType` | 字串 | 使用&quot;OAUTH2&quot;。 |
| `grant` | 字串 | 使用&quot;OAUTH2_PASSWORD&quot;。 |
| `accessTokenUrl` | 字串 | 您這邊的URL會發出存取權杖，並選擇性地重新整理權杖。 |
| `clientId` | 字串 | 您的系統指派給Adobe Experience Platform的用戶端ID。 |
| `clientSecret` | 字串 | 您的系統指派給Adobe Experience Platform的用戶端密碼。 |
| `scope` | 字串清單 | *可選*. 設定存取權杖可讓Experience Platform對您的資源執行之作業的範圍。 範例：「讀，寫」。 |

{style="table-layout:auto"}

## 具有客戶端憑據的OAuth 2授予

您可以設定OAuth 2用戶端認證(請參閱 [RFC標準規格](https://tools.ietf.org/html/rfc6749#section-4.4))目的地，支援下列標準輸入和輸出。 您可以自訂值。 請參閱 [自訂您的OAuth 2設定](./oauth2-authentication.md#customize-configuration) 以取得詳細資訊。

| OAuth 2授予 | 輸入 | 輸出 |
|---------|----------|---------|
| 客戶端憑據 | <ul><li><b>clientId</b></li><li><b>clientSecret</b></li><li>範圍</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>過期時間</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

若要為您的目的地設定此驗證方法，請在 `/destinations` [端點](./destination-configuration.md):

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
| `authType` | 字串 | 使用&quot;OAUTH2&quot;。 |
| `grant` | 字串 | 使用&quot;OAUTH2_CLIENT_CREDENTIALS&quot;。 |
| `accessTokenUrl` | 字串 | 授權伺服器的URL，會發出存取權杖和選用的重新整理權杖。 |
| `refreshTokenUrl` | 字串 | *選填.* 您這邊的URL會發生重新整理Token的問題。 通常， `refreshTokenUrl` 與 `accessTokenUrl`. |
| `clientId` | 字串 | 您的系統指派給Adobe Experience Platform的用戶端ID。 |
| `clientSecret` | 字串 | 您的系統指派給Adobe Experience Platform的用戶端密碼。 |
| `scope` | 字串清單 | *可選*. 設定存取權杖可讓Experience Platform對您的資源執行之作業的範圍。 範例：「讀，寫」。 |

{style="table-layout:auto"}

## 自訂您的OAuth 2設定 {#customize-configuration}

上節所述的設定說明標準OAuth 2授予。 不過，由Adobe設計的系統具有彈性，因此您可以針對OAuth 2授權中的任何變數使用自訂參數。 若要自訂標準OAuth 2設定，請使用 `authenticationDataFields` 參數，如下列範例所示。

### 範例1:使用 `authenticationDataFields` 捕獲來自身份驗證響應的資訊 {#example-1}

在此範例中，目的地平台會重新整理Token，這些Token會在一段時間後過期。 在此情況下，合作夥伴會設定 `refreshTokenExpiration` 自訂欄位，從 `refresh_token_expires_in` 欄位。

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

### 範例2:使用 `authenticationDataFields` 提供特殊的重新整理代號 {#example-2}

在此範例中，合作夥伴會設定其目的地，以提供特殊的重新整理Token。 此外，存取權杖的到期日不會在API回應中傳回，因此它們可以以硬式編碼撰寫預設值，在此例中為3600秒。

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

### 範例3:使用者在設定目的地時輸入用戶端ID和用戶端密碼 {#example-3}

在此範例中，請避免建立全域用戶端ID和用戶端密碼，如區段所示 [系統的必要條件](./oauth2-authentication.md#prerequisites)，則客戶必須輸入用戶端ID、用戶端密碼和帳戶ID（客戶用來登入目的地的ID）

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



您可以在 `authenticationDataFields` 若要自訂OAuth 2設定：

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `authenticationDataFields.name` | 字串 | 自訂欄位的名稱。 |
| `authenticationDataFields.title` | 字串 | 可為自訂欄位提供的標題。 |
| `authenticationDataFields.description` | 字串 | 您設定的自訂資料欄位說明。 |
| `authenticationDataFields.type` | 字串 | 定義自訂資料欄位的類型。 <br> 接受的值： `string`, `boolean`, `integer` |
| `authenticationDataFields.isRequired` | 布林值 | 指定驗證流程中是否需要自訂資料欄位。 |
| `authenticationDataFields.format` | 字串 | 選取 `"format":"password"`,Adobe會加密驗證資料欄位的值。 搭配使用時 `"fieldType": "CUSTOMER"`，這也會在使用者輸入欄位時隱藏UI中的輸入。 |
| `authenticationDataFields.fieldType` | 字串 | 指出輸入內容是來自合作夥伴（您）還是來自使用者，當他們以Experience Platform設定您的目的地時。 |
| `authenticationDataFields.value` | 字串. 布林值. 整數 | 自訂資料欄位的值。 值與所選取的類型相符 `authenticationDataFields.type`. |
| `authenticationDataFields.authenticationResponsePath` | 字串 | 指出您參考的API回應路徑中的哪個欄位。 |

{style="table-layout:auto"}

## 存取權杖重新整理 {#access-token-refresh}

Adobe已設計系統，可重新整理過期的存取權杖，而不要求使用者重新登入您的平台。 系統能產生新代號，讓客戶能夠順暢地繼續啟動至目的地。

若要設定存取權杖重新整理，您可能需要設定範本化HTTP請求，讓Adobe使用重新整理權杖來取得新的存取權杖。 如果存取權杖已過期，Adobe會取用您提供的範本請求，並新增您提供的參數。 使用 `accessTokenRequest` 設定存取權杖重新整理機制的參數。


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

您可以在 `accessTokenRequest` 若要自訂代號重新整理程式：

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `accessTokenRequest.destinationServerType` | 字串 | 使用 `URL_BASED`. |
| `accessTokenRequest.urlBasedDestination.url.templatingStrategy` | 字串 | <ul><li>使用 `PEBBLE_V1` 如果您對 `accessTokenRequest.urlBasedDestination.url.value`.</li><li> 使用 `NONE` 如果欄位中的值 `accessTokenRequest.urlBasedDestination.url.value` 是常數。 </li></li> |
| `accessTokenRequest.urlBasedDestination.url.value` | 字串 | Experience Platform要求存取權杖的URL。 |
| `accessTokenRequest.httpTemplate.requestBody.templatingStrategy` | 字串 | <ul><li>使用 `PEBBLE_V1` 若您對 `accessTokenRequest.httpTemplate.requestBody.value`.</li><li> 使用 `NONE` 如果欄位中的值 `accessTokenRequest.httpTemplate.requestBody.value` 是常數。 </li></li> |
| `accessTokenRequest.httpTemplate.requestBody.value` | 字串 | 使用範本語言來自訂HTTP要求中的欄位至存取權杖端點。 有關如何使用模板自定義欄位的資訊，請參閱 [模板約定](./oauth2-authentication.md#templating-conventions) 區段。 |
| `accessTokenRequest.httpTemplate.httpMethod` | 字串 | 指定用來呼叫存取權杖端點的HTTP方法。 在大多數情況下，此值是 `POST`. |
| `accessTokenRequest.httpTemplate.contentType` | 字串 | 指定對您的存取權杖端點進行HTTP呼叫的內容類型。 <br> 例如： `application/x-www-form-urlencoded` 或 `application/json`. |
| `accessTokenRequest.httpTemplate.headers` | 字串 | 指定是否應將任何標題新增至存取權杖端點的HTTP呼叫。 |
| `accessTokenRequest.responseFields.templatingStrategy` | 字串 | <ul><li>使用 `PEBBLE_V1` 若您對 `accessTokenRequest.responseFields.value`.</li><li> 使用 `NONE` 如果欄位中的值 `accessTokenRequest.responseFields.value` 是常數。 </li></li> |
| `accessTokenRequest.responseFields.value` | 字串 | 使用範本語言從存取權杖端點存取HTTP回應中的欄位。 有關如何使用模板自定義欄位的資訊，請參閱 [模板約定](./oauth2-authentication.md#templating-conventions) 區段。 |
| `accessTokenRequest.validations.name` | 字串 | 指示為此驗證提供的名稱。 |
| `accessTokenRequest.validations.actualValue.templatingStrategy` | 字串 | <ul><li>使用 `PEBBLE_V1` 若您對 `accessTokenRequest.validations.actualValue.value`.</li><li> 使用 `NONE` 如果欄位中的值 `accessTokenRequest.validations.actualValue.value` 是常數。 </li></li> |
| `accessTokenRequest.validations.actualValue.value` | 字串 | 使用範本語言存取HTTP回應中的欄位。 有關如何使用模板自定義欄位的資訊，請參閱 [模板約定](./oauth2-authentication.md#templating-conventions) 區段。 |
| `accessTokenRequest.validations.expectedValue.templatingStrategy` | 字串 | <ul><li>使用 `PEBBLE_V1` 若您對 `accessTokenRequest.validations.expectedValue.value`.</li><li> 使用 `NONE` 如果欄位中的值 `accessTokenRequest.validations.expectedValue.value` 是常數。 </li></li> |
| `accessTokenRequest.validations.expectedValue.value` | 字串 | 使用範本語言存取HTTP回應中的欄位。 有關如何使用模板自定義欄位的資訊，請參閱 [模板約定](./oauth2-authentication.md#templating-conventions) 區段。 |

{style="table-layout:auto"}

## 範本慣例 {#templating-conventions}

視您的驗證自訂而定，您可能需要存取驗證回應中的資料欄位，如前一節所示。 若要這麼做，請熟悉 [卵石模板語言](https://pebbletemplates.io/) 供Adobe使用，並參考下列範本慣例以自訂您的OAuth 2實作。


| 前置詞 | 說明 | 範例 |
|---------|----------|---------|
| authData | 存取任何合作夥伴或客戶資料欄位的值。 | ``{{ authData.accessToken }}`` |
| response.body | HTTP回應內文 | ``{{ response.body.access_token }}`` |
| response.status | HTTP回應狀態 | ``{{ response.status }}`` |
| response.headers | HTTP回應標題 | ``{{ response.headers.server[0] }}`` |
| userContext | 訪問有關當前身份驗證嘗試的資訊 | <ul><li>`{{ userContext.sandboxName }} `</li><li>`{{ userContext.sandboxId }} `</li><li>`{{ userContext.imsOrgId }} `</li><li>`{{ userContext.client }} // the client executing the authentication attempt `</li></ul> |

{style="table-layout:auto"}

## 後續步驟 {#next-steps}

閱讀本文，您現在已了解Adobe Experience Platform支援的OAuth 2驗證模式，並了解如何使用OAuth 2驗證支援來設定您的目的地。 接下來，您可以使用Destination SDK來設定OAuth 2支援的目的地。 閱讀 [使用Destination SDK來設定您的目的地](./configure-destination-instructions.md) 以了解後續步驟。
