---
description: 此頁面說明Destination SDK支援的各種OAuth 2授權流程，並提供為目的地設定OAuth 2授權的指示。
title: OAuth 2授權
exl-id: 280ecb63-5739-491c-b539-3c62bd74e433
source-git-commit: 8f430fa3949c19c22732ff941e8c9b07adb37e1f
workflow-type: tm+mt
source-wordcount: '2154'
ht-degree: 4%

---


# OAuth 2授權

Destination SDK支援多種前往目的地的授權方法。 其中一種選項是使用 [OAuth 2授權架構](https://tools.ietf.org/html/rfc6749).

此頁面說明Destination SDK支援的各種OAuth 2授權流程，並提供為目的地設定OAuth 2授權的指示。

>[!IMPORTANT]
>
>Destination SDK支援的所有引數名稱和值如下 **區分大小寫**. 為避免區分大小寫錯誤，請完全依照檔案中所示使用引數名稱和值。

## 支援的整合型別 {#supported-integration-types}

如需瞭解哪些型別的整合支援本頁面所述功能的詳細資訊，請參閱下表。

| 整合型別 | 支援功能 |
|---|---|
| 即時（串流）整合 | 是 |
| 檔案式（批次）整合 | 無 |

## 如何將OAuth 2授權詳細資料新增至您的目的地設定 {#how-to-setup}

### 您系統中的必要條件 {#prerequisites}

首先，您必須在系統中建立適用於Adobe Experience Platform的應用程式，或在系統中註冊Experience Platform。 目標是產生使用者端ID和使用者端密碼，這是驗證Experience Platform至您的目的地所需的密碼。 在您的系統中，此設定會包含您所需的Adobe Experience Platform OAuth 2重新導向/回呼URL，您可於下列清單中取得該URL。

* `https://platform-va7.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-nld2.adobe.io/data/core/activation/oauth/api/v1/callback`
* `https://platform-aus5.adobe.io/data/core/activation/oauth/api/v1/callback`

>[!IMPORTANT]
>
>只有在下列情況下，才需要在您的系統中為Adobe Experience Platform註冊重新導向/回呼URL的步驟 [含授權碼的OAuth 2](#authorization-code) 授予型別。 對於其他兩種支援的授權型別（密碼和使用者端認證），您可以略過此步驟。

在此步驟結束時，您應該會：
* 使用者端ID；
* 使用者端密碼；
* Adobe的回呼URL （用於授權代碼授權）。

### 您在Destination SDK中需要做什麼 {#to-do-in-destination-sdk}

若要在Experience Platform中為目的地設定OAuth 2授權，您必須將OAuth 2詳細資料新增至 [目的地設定](../../authoring-api/destination-configuration/create-destination-configuration.md)，位於 `customerAuthenticationConfigurations` 引數。 另請參閱 [客戶驗證](../../functionality/destination-configuration/customer-authentication.md) 以取得詳細範例。 本頁面進一步說明會根據您的OAuth 2授權授予型別，說明您需要將哪些欄位新增至設定範本。

## 支援的OAuth 2授權型別 {#oauth2-grant-types}

Experience Platform支援下表中的三個OAuth 2授權型別。 如果您有自訂OAuth 2設定，Adobe可以透過整合中的自訂欄位提供支援。 如需詳細資訊，請參閱各授權型別的章節。

>[!IMPORTANT]
>
>* 您可以依照下節的指示提供輸入引數。 Adobe內部系統連線至您平台的授權系統並抓取輸出引數，這些引數用於驗證使用者及維護對您目的地的授權。
>* 在OAuth 2授權流程中，表格中以粗體強調顯示的輸入引數為必要引數。 其他引數為選用引數。 還有其他未顯示於此處但於各節中詳細說明的自訂輸入引數 [自訂您的OAuth 2設定](#customize-configuration) 和 [存取權杖重新整理](#access-token-refresh).

| OAuth 2授予 | 輸入 | 輸出 |
|---------|----------|---------|
| 授權代碼 | <ul><li><b>clientId</b></li><li><b>使用者端密碼</b></li><li>範圍</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| 密碼 | <ul><li><b>clientId</b></li><li><b>使用者端密碼</b></li><li>範圍</li><li><b>accessTokenUrl</b></li><li><b>使用者名稱</b></li><li><b>密碼</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |
| 使用者端認證 | <ul><li><b>clientId</b></li><li><b>使用者端密碼</b></li><li>範圍</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

上表列出標準OAuth 2流程中使用的欄位。 除了這些標準欄位之外，不同的合作夥伴整合可能需要額外的輸入和輸出。 Adobe已為Destination SDK設計了彈性的OAuth 2授權架構，可以處理上述標準欄位模式的變異，同時支援自動重新產生無效輸出的機制，例如過期的存取權杖。

在任何情況下，輸出都包含存取權杖，Experience Platform會使用該權杖來驗證和維護對您目的地的授權。

Adobe為OAuth 2授權設計的系統：
* 支援所有三個OAuth 2授權，並解決其中的任何變數，例如其他資料欄位、非標準API呼叫等。
* 支援具有不同期限值（90天、30分鐘或您指定的任何其他期限值）的存取權杖。
* 支援具有或不具有重新整理權杖的OAuth 2授權流程。

## 含授權碼的OAuth 2 {#authorization-code}

如果您的目的地支援標準OAuth 2.0授權代碼流程(閱讀 [RFC標準規格](https://tools.ietf.org/html/rfc6749#section-4.1))或它的變體，請參閱下列必要和選用欄位：

| OAuth 2授予 | 輸入 | 輸出 |
|---------|----------|---------|
| 授權代碼 | <ul><li><b>clientId</b></li><li><b>使用者端密碼</b></li><li>範圍</li><li><b>authorizationUrl</b></li><li><b>accessTokenUrl</b></li><li>refreshTokenUrl</li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

若要針對您的目的地設定此授權方法，請在設定中新增下列行，當 [建立目的地設定](../../authoring-api/destination-configuration/create-destination-configuration.md)：

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
| `grant` | 字串 | 使用「OAUTH2_AUTHORIZATION_CODE」。 |
| `accessTokenUrl` | 字串 | 您這邊的URL會核發存取權杖，並可選擇重新整理權杖。 |
| `authorizationUrl` | 字串 | 授權伺服器的URL，您可在此處重新導向使用者以登入您的應用程式。 |
| `refreshTokenUrl` | 字串 | *選填.* 您這邊的URL會發出重新整理Token。 通常 `refreshTokenUrl` 與 `accessTokenUrl`. |
| `clientId` | 字串 | 系統指派給Adobe Experience Platform的使用者端ID。 |
| `clientSecret` | 字串 | 您的系統指派給Adobe Experience Platform的使用者端密碼。 |
| `scope` | 字串清單 | *可選*. 設定存取Token允許Experience Platform對您的資源執行的範圍。 範例： &quot;read， write&quot;。 |

{style="table-layout:auto"}

## 具有密碼授予的OAuth 2

針對OAuth 2密碼授予(請參閱 [RFC標準規格](https://tools.ietf.org/html/rfc6749#section-4.3))，Experience Platform需要使用者的使用者名稱和密碼。 在授權流程中，Experience Platform會將這些認證交換為存取權杖，以及選擇性地交換重新整理權杖。
Adobe會使用以下標準輸入來簡化目的地設定，並具備覆寫值的功能：

| OAuth 2授予 | 輸入 | 輸出 |
|---------|----------|---------|
| 密碼 | <ul><li><b>clientId</b></li><li><b>使用者端密碼</b></li><li>範圍</li><li><b>accessTokenUrl</b></li><li><b>使用者名稱</b></li><li><b>密碼</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

>[!NOTE]
>
> 您不需要為新增任何引數 `username` 和 `password` 在以下的設定中。 當您新增時 `"grant": "OAUTH2_PASSWORD"` 在目標設定中，當使用者對您的目標進行驗證時，系統將要求使用者在Experience PlatformUI中提供使用者名稱和密碼。

若要針對您的目的地設定此授權方法，請在設定中新增下列行，當 [建立目的地設定](../../authoring-api/destination-configuration/create-destination-configuration.md)：

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
| `accessTokenUrl` | 字串 | 您這邊的URL會核發存取權杖，並可選擇重新整理權杖。 |
| `clientId` | 字串 | 系統指派給Adobe Experience Platform的使用者端ID。 |
| `clientSecret` | 字串 | 您的系統指派給Adobe Experience Platform的使用者端密碼。 |
| `scope` | 字串清單 | *可選*. 設定存取Token允許Experience Platform對您的資源執行的範圍。 範例： &quot;read， write&quot;。 |

{style="table-layout:auto"}

## 具有使用者端憑證授權的OAuth 2

您可以設定OAuth 2使用者端認證(請參閱 [RFC標準規格](https://tools.ietf.org/html/rfc6749#section-4.4))目的地，支援下列標準輸入和輸出。 您可以自訂值。 另請參閱 [自訂您的OAuth 2設定](#customize-configuration) 以取得詳細資訊。

| OAuth 2授予 | 輸入 | 輸出 |
|---------|----------|---------|
| 使用者端認證 | <ul><li><b>clientId</b></li><li><b>使用者端密碼</b></li><li>範圍</li><li><b>accessTokenUrl</b></li></ul> | <ul><li><b>accessToken</b></li><li>expiresIn</li><li>refreshToken</li><li>tokenType</li></ul> |

{style="table-layout:auto"}

若要針對您的目的地設定此授權方法，請在設定中新增下列行，當 [建立目的地設定](../../authoring-api/destination-configuration/create-destination-configuration.md)：

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
| `accessTokenUrl` | 字串 | 授權伺服器的URL，它會發出存取權杖和選用的重新整理權杖。 |
| `refreshTokenUrl` | 字串 | *選填.* 您這邊的URL會發出重新整理Token。 通常 `refreshTokenUrl` 與 `accessTokenUrl`. |
| `clientId` | 字串 | 系統指派給Adobe Experience Platform的使用者端ID。 |
| `clientSecret` | 字串 | 您的系統指派給Adobe Experience Platform的使用者端密碼。 |
| `scope` | 字串清單 | *可選*. 設定存取Token允許Experience Platform對您的資源執行的範圍。 範例： &quot;read， write&quot;。 |

{style="table-layout:auto"}

## 自訂您的OAuth 2設定 {#customize-configuration}

上節所述的設定描述了標準OAuth 2授權。 不過，由Adobe設計的系統提供彈性，讓您可以將自訂引數用於OAuth 2授權中的任何變數。 若要自訂標準OAuth 2設定，請使用 `authenticationDataFields` 引數，如下列範例所示。

### 範例1：使用 `authenticationDataFields` 擷取來自授權回應的資訊 {#example-1}

在此範例中，目的地平台的重新整理權杖會在特定時間後到期。 在這種情況下，合作夥伴會設定 `refreshTokenExpiration` 自訂欄位以取得來自的重新整理權杖有效期 `refresh_token_expires_in` API回應中的欄位。

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

### 範例2：使用 `authenticationDataFields` 提供特殊的重新整理權杖 {#example-2}

在此範例中，合作夥伴會設定其目的地，以提供特殊的重新整理權杖。 此外，存取權杖的到期日不會在API回應中傳回，因此他們可以硬式編碼預設值，在此例中為3600秒。

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

### 範例3：使用者在設定目的地時輸入使用者端ID和使用者端密碼 {#example-3}

在此範例中，不會建立全域使用者端ID和使用者端密碼，如區段所示 [您系統中的必要條件](#prerequisites)，客戶必須輸入使用者端ID、使用者端密碼和帳戶ID （客戶用來登入目的地的ID）

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



您可在中使用下列引數 `authenticationDataFields` 若要自訂您的OAuth 2設定：

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `authenticationDataFields.name` | 字串 | 自訂欄位的名稱。 |
| `authenticationDataFields.title` | 字串 | 您可以為自訂欄位提供的標題。 |
| `authenticationDataFields.description` | 字串 | 您設定的自訂資料欄位說明。 |
| `authenticationDataFields.type` | 字串 | 定義自訂資料欄位的型別。 <br> 接受的值： `string`， `boolean`， `integer` |
| `authenticationDataFields.isRequired` | 布林值 | 指定在授權流程中是否需要自訂資料欄位。 |
| `authenticationDataFields.format` | 字串 | 當您選取 `"format":"password"`，Adobe會加密授權資料欄位的值。 搭配使用時 `"fieldType": "CUSTOMER"`，這也會在使用者鍵入欄位時隱藏UI中的輸入。 |
| `authenticationDataFields.fieldType` | 字串 | 指出當合作夥伴（您）或使用者在Experience Platform中設定您的目的地時，輸入是否來自他們。 |
| `authenticationDataFields.value` | 字串. 布林值. 整數 | 自訂資料欄位的值。 值與從中選擇的型別相符 `authenticationDataFields.type`. |
| `authenticationDataFields.authenticationResponsePath` | 字串 | 指出您正在參照的API回應路徑欄位。 |

{style="table-layout:auto"}

## 存取權杖重新整理 {#access-token-refresh}

Adobe設計的系統可重新整理過期的存取權杖，而不需要使用者重新登入您的平台。 系統能夠產生新的Token，這樣客戶就能順暢地繼續啟用您的目的地。

若要設定存取權杖重新整理，您可能需要設定範本化HTTP請求，以允許Adobe使用重新整理權杖取得新的存取權杖。 如果存取權杖已過期，Adobe會採用您提供的樣板化請求，並新增您提供的引數。 使用 `accessTokenRequest` 引數以設定存取權杖重新整理機制。


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

您可在中使用下列引數 `accessTokenRequest` 若要自訂您的Token重新整理程式：

| 參數 | 類型 | 說明 |
|---------|----------|------|
| `accessTokenRequest.destinationServerType` | 字串 | 使用 `URL_BASED`. |
| `accessTokenRequest.urlBasedDestination.url.templatingStrategy` | 字串 | <ul><li>使用 `PEBBLE_V1` 如果您將範本用於 `accessTokenRequest.urlBasedDestination.url.value`.</li><li> 使用 `NONE` 如果欄位中的值 `accessTokenRequest.urlBasedDestination.url.value` 為常數。 </li></li> |
| `accessTokenRequest.urlBasedDestination.url.value` | 字串 | Experience Platform要求存取權杖的URL。 |
| `accessTokenRequest.httpTemplate.requestBody.templatingStrategy` | 字串 | <ul><li>使用 `PEBBLE_V1` 如果您將範本用於 `accessTokenRequest.httpTemplate.requestBody.value`.</li><li> 使用 `NONE` 如果欄位中的值 `accessTokenRequest.httpTemplate.requestBody.value` 為常數。 </li></li> |
| `accessTokenRequest.httpTemplate.requestBody.value` | 字串 | 使用範本化語言來自訂HTTP請求中的欄位以存取權杖端點。 有關如何使用範本化來自訂欄位的資訊，請參閱 [範本化慣例](#templating-conventions) 區段。 |
| `accessTokenRequest.httpTemplate.httpMethod` | 字串 | 指定用來呼叫存取權杖端點的HTTP方法。 在大多數情況下，這個值為 `POST`. |
| `accessTokenRequest.httpTemplate.contentType` | 字串 | 指定存取權杖端點之HTTP呼叫的內容型別。 <br> 例如： `application/x-www-form-urlencoded` 或 `application/json`. |
| `accessTokenRequest.httpTemplate.headers` | 字串 | 指定是否應將任何標頭新增至存取權杖端點的HTTP呼叫。 |
| `accessTokenRequest.responseFields.templatingStrategy` | 字串 | <ul><li>使用 `PEBBLE_V1` 如果您將範本用於 `accessTokenRequest.responseFields.value`.</li><li> 使用 `NONE` 如果欄位中的值 `accessTokenRequest.responseFields.value` 為常數。 </li></li> |
| `accessTokenRequest.responseFields.value` | 字串 | 使用範本化語言從存取權杖端點存取HTTP回應中的欄位。 有關如何使用範本化來自訂欄位的資訊，請參閱 [範本化慣例](#templating-conventions) 區段。 |
| `accessTokenRequest.validations.name` | 字串 | 表示您為此驗證提供的名稱。 |
| `accessTokenRequest.validations.actualValue.templatingStrategy` | 字串 | <ul><li>使用 `PEBBLE_V1` 如果您將範本用於 `accessTokenRequest.validations.actualValue.value`.</li><li> 使用 `NONE` 如果欄位中的值 `accessTokenRequest.validations.actualValue.value` 為常數。 </li></li> |
| `accessTokenRequest.validations.actualValue.value` | 字串 | 使用範本化語言來存取HTTP回應中的欄位。 有關如何使用範本化來自訂欄位的資訊，請參閱 [範本化慣例](#templating-conventions) 區段。 |
| `accessTokenRequest.validations.expectedValue.templatingStrategy` | 字串 | <ul><li>使用 `PEBBLE_V1` 如果您將範本用於 `accessTokenRequest.validations.expectedValue.value`.</li><li> 使用 `NONE` 如果欄位中的值 `accessTokenRequest.validations.expectedValue.value` 為常數。 </li></li> |
| `accessTokenRequest.validations.expectedValue.value` | 字串 | 使用範本化語言來存取HTTP回應中的欄位。 有關如何使用範本化來自訂欄位的資訊，請參閱 [範本化慣例](#templating-conventions) 區段。 |

{style="table-layout:auto"}

## 範本化慣例 {#templating-conventions}

根據您的授權自訂，您可能需要存取授權回應中的資料欄位，如上一節所示。 若要這麼做，請熟悉 [Pebble範本語言](https://pebbletemplates.io/) 供Adobe使用，並參閱以下範本慣例以自訂您的OAuth 2實作。


| 前置詞 | 說明 | 範例 |
|---------|----------|---------|
| authData | 存取任何合作夥伴或客戶資料欄位的值。 | ``{{ authData.accessToken }}`` |
| response.body | HTTP回應內文 | ``{{ response.body.access_token }}`` |
| response.status | HTTP回應狀態 | ``{{ response.status }}`` |
| response.headers | HTTP回應標題 | ``{{ response.headers.server[0] }}`` |
| userContext | 存取有關目前授權嘗試的資訊 | <ul><li>`{{ userContext.sandboxName }} `</li><li>`{{ userContext.sandboxId }} `</li><li>`{{ userContext.imsOrgId }} `</li><li>`{{ userContext.client }} // the client executing the authorization attempt `</li></ul> |

{style="table-layout:auto"}

## 後續步驟 {#next-steps}

閱讀本文章，您現在已瞭解Adobe Experience Platform支援的OAuth 2授權模式，知道如何使用OAuth 2授權支援設定您的目的地。 接下來，您可以使用Destination SDK設定您的OAuth 2支援目的地。 讀取 [使用Destination SDK設定您的目的地](../../guides/configure-destination-instructions.md) 以瞭解後續步驟。
