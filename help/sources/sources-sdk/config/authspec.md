---
keywords: Experience Platform；首頁；熱門主題；來源；連接器；來源連接器；來源sdk;sdk; SDK
title: 配置自助源的驗證規範(Batch SDK)
description: 本檔案概述使用自助來源（批次SDK）所需準備的設定。
exl-id: 68ed22fe-1f22-46d2-9d58-72ad8a9e6b98
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 1%

---

# 配置自助源的驗證規範(Batch SDK)

驗證規格會定義Adobe Experience Platform使用者如何連線至您的來源。

此 `authSpec` array包含將源連接到平台所需的身份驗證參數的資訊。 任何給定的源都可支援多種不同類型的身份驗證。

## 驗證規範

自助來源（批次SDK）支援OAuth 2重新整理程式碼和基本驗證。 請參閱下表，了解使用OAuth 2重新整理程式碼和基本驗證的指引

### OAuth 2重新整理程式碼

OAuth 2重新整理程式碼可產生暫時存取權杖和重新整理權杖，以安全存取應用程式。 存取權杖可讓您安全地存取您的資源，而不需提供其他憑證，而重新整理權杖可讓您在存取權杖過期後，產生新的存取權杖。

```json
{
  "name": "OAuth2 Refresh Code",
  "type": "OAuth2RefreshCode",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
    "properties": {
      "authorizationTestUrl": {
        "description": "Authorization test url to validate accessToken.",
        "type": "string"
      },
      "clientId": {
        "description": "Client id of user account.",
        "type": "string"
      },
      "clientSecret": {
        "description": "Client secret of user account.",
        "type": "string",
        "format": "password"
      },
      "accessToken": {
        "description": "Access Token",
        "type": "string",
        "format": "password"
      },
      "refreshToken": {
        "description": "Refresh Token",
        "type": "string",
        "format": "password"
      },
      "expirationDate": {
        "description": "Date of token expiry.",
        "type": "string",
        "format": "date",
        "uiAttributes": {
          "hidden": true
        }
      },
      "accessTokenUrl": {
        "description": "Access token url to fetch access token.",
        "type": "string"
      },
      "requestParameterOverride": {
        "type": "object",
        "description": "Specify parameter to override.",
        "properties": {
          "accessTokenField": {
            "description": "Access token field name to override.",
            "type": "string"
          },
          "refreshTokenField": {
            "description": "Refresh token field name to override.",
            "type": "string"
          },
          "expireInField": {
            "description": "ExpireIn field name to override.",
            "type": "string"
          },
          "authenticationMethod": {
            "description": "Authentication method override.",
            "type": "string",
            "enum": [
              "GET",
              "POST"
            ]
          },
          "clientId": {
            "description": "ClientId field name override.",
            "type": "string"
          },
          "clientSecret": {
            "description": "ClientSecret field name override.",
            "type": "string"
          }
        }
      }
    },
    "required": [
      "accessToken"
    ]
  }
}
```

| 屬性 | 說明 | 範例 |
| --- | --- | --- |
| `authSpec.name` | 顯示支援的驗證類型的名稱。 | `oAuth2-refresh-code` |
| `authSpec.type` | 定義源支援的驗證類型。 | `oAuth2-refresh-code` |
| `authSpec.spec` | 包含驗證結構、資料類型和屬性的相關資訊。 |
| `authSpec.spec.$schema` | 定義用於驗證的架構。 | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | 定義架構的資料類型。 | `object` |
| `authSpec.spec.properties` | 包含用於驗證的憑據的資訊。 |
| `authSpec.spec.properties.description` | 顯示憑據的簡短說明。 |
| `authSpec.spec.properties.type` | 定義憑據的資料類型。 | `string` |
| `authSpec.spec.properties.clientId` | 與您的應用程式相關聯的用戶端ID。 用戶端ID會與您的用戶端密碼搭配使用，以擷取您的存取權杖。 |
| `authSpec.spec.properties.clientSecret` | 與您的應用程式相關聯的用戶端密碼。 用戶端密碼會與您的用戶端ID搭配使用，以擷取您的存取權杖。 |
| `authSpec.spec.properties.accessToken` | 存取權杖可授權您安全存取您的應用程式。 |
| `authSpec.spec.properties.refreshToken` | 當存取權杖過期時，會使用重新整理權杖來產生新的存取權杖。 |
| `authSpec.spec.properties.expirationDate` | 定義存取權杖的到期日。 |
| `authSpec.spec.properties.refreshTokenUrl` | 用來擷取重新整理Token的URL。 |
| `authSpec.spec.properties.accessTokenUrl` | 用來擷取重新整理Token的URL。 |
| `authSpec.spec.properties.requestParameterOverride` | 允許您指定在驗證時要覆蓋的憑據參數。 |
| `authSpec.spec.required` | 顯示驗證所需的憑據。 | `accessToken` |

{style="table-layout:auto"}


### 基本驗證

基本驗證是一種驗證類型，可讓您使用帳戶使用者名稱和帳戶密碼的組合來存取應用程式。

```json
{
  "name": "Basic Authentication",
  "type": "BasicAuthentication",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "defines auth params required for connecting to rest service.",
    "properties": {
      "username": {
        "description": "Username to connect rest endpoint.",
        "type": "string"
      },
      "password": {
        "description": "Password to connect rest endpoint.",
        "type": "string",
        "format": "password"
      }
    },
    "required": [
      "username",
      "password"
    ]
  }
}
```

| 屬性 | 說明 | 範例 |
| --- | --- | --- |
| `authSpec.name` | 顯示支援的驗證類型的名稱。 | `Basic Authentication` |
| `authSpec.type` | 定義源支援的驗證類型。 | `BasicAuthentication` |
| `authSpec.spec` | 包含驗證結構、資料類型和屬性的相關資訊。 |
| `authSpec.spec.$schema` | 定義用於驗證的架構。 | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | 定義架構的資料類型。 | `object` |
| `authSpec.spec.description` | 顯示驗證類型的詳細資訊。 |
| `authSpec.spec.properties` | 包含用於驗證的憑據的資訊。 |
| `authSpec.spec.properties.username` | 與您的應用程式相關聯的帳戶使用者名稱。 |
| `authSpec.spec.properties.password` | 與您的應用程式相關聯的帳戶密碼。 |
| `authSpec.spec.required` | 指定在Platform中要輸入的必填值所需欄位。 | `username` |

{style="table-layout:auto"}

## 驗證規範示例

以下是使用 [[!DNL MailChimp Members]](../../tutorials/api/create/marketing-automation/mailchimp-members.md) 來源。

```json
  "authSpec": [
    {
      "name": "OAuth2 Refresh Code",
      "type": "OAuth2RefreshCode",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "Define auth params required for connecting to generic rest using oauth2 authorization code.",
        "properties": {
          "authorizationTestUrl": {
            "description": "Authorization test url to validate accessToken.",
            "type": "string"
          },
          "accessToken": {
            "description": "Access Token of mailChimp endpoint.",
            "type": "string",
            "format": "password"
          }
        },
        "required": [
          "accessToken"
        ]
      }
    },
    {
      "name": "Basic Authentication",
      "type": "BasicAuthentication",
      "spec": {
        "$schema": "http://json-schema.org/draft-07/schema#",
        "type": "object",
        "description": "defines auth params required for connecting to rest service.",
        "properties": {
          "username": {
            "description": "Username to connect mailChimp endpoint.",
            "type": "string"
          },
          "password": {
            "description": "Password to connect mailChimp endpoint.",
            "type": "string",
            "format": "password"
          }
        },
        "required": [
          "username",
          "password"
        ]
      }
    }
  ],
```

## 後續步驟

在填入驗證規範後，您可以繼續為要整合到Platform的源配置源規範。 請參閱 [配置源規範](./sourcespec.md) 以取得更多資訊。
