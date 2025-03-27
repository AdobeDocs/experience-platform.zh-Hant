---
keywords: Experience Platform；首頁；熱門主題；來源；聯結器；來源聯結器；來源sdk；sdk；SDK
title: 設定自助來源驗證規格(批次SDK)
description: 本檔案提供使用自助來源(批次SDK)所需準備的設定概述。
exl-id: 68ed22fe-1f22-46d2-9d58-72ad8a9e6b98
source-git-commit: 8517532f991413a239e0da890bf53b1bf5b621f0
workflow-type: tm+mt
source-wordcount: '770'
ht-degree: 3%

---

# 設定自助來源驗證規格(批次SDK)

驗證規格會定義Adobe Experience Platform使用者如何連線至您的來源。

`authSpec`陣列包含將來源連線到Platform所需的驗證引數資訊。 任何特定來源都可以支援多種不同型別的驗證。

## 驗證規格

自助來源(批次SDK)支援OAuth 2重新整理程式碼和基本驗證。 如需使用OAuth 2重新整理程式碼和基本驗證的指引，請參閱下表

### OAuth 2重新整理代碼

OAuth 2重新整理程式碼可產生暫時存取權杖和重新整理權杖，以安全地存取應用程式。 存取權杖可讓您安全存取您的資源，而無需提供其他認證，而重新整理權杖可讓您在存取權杖過期後產生新的存取權杖。

+++檢視OAuth 2重新整理程式碼的範例

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
| `authSpec.name` | 顯示支援的驗證型別名稱。 | `oAuth2-refresh-code` |
| `authSpec.type` | 定義來源支援的驗證型別。 | `oAuth2-refresh-code` |
| `authSpec.spec` | 包含驗證結構、資料型別和屬性的相關資訊。 |
| `authSpec.spec.$schema` | 定義用於驗證的結構描述。 | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | 定義結構描述的資料型別。 | `object` |
| `authSpec.spec.properties` | 包含用於驗證的認證的相關資訊。 |
| `authSpec.spec.properties.description` | 顯示認證的簡短說明。 |
| `authSpec.spec.properties.type` | 定義認證的資料型別。 | `string` |
| `authSpec.spec.properties.clientId` | 與您的應用程式相關聯的使用者端ID。 使用者端ID會與您的使用者端密碼搭配使用，以擷取您的存取權杖。 |
| `authSpec.spec.properties.clientSecret` | 與您的應用程式關聯的使用者端密碼。 使用者端密碼會與使用者端ID搭配使用，以擷取您的存取權杖。 |
| `authSpec.spec.properties.accessToken` | 存取權杖會授權您安全存取應用程式。 |
| `authSpec.spec.properties.refreshToken` | 當存取權杖過期時，重新整理權杖會用來產生新的存取權杖。 |
| `authSpec.spec.properties.expirationDate` | 定義存取Token的到期日。 |
| `authSpec.spec.properties.refreshTokenUrl` | 用來擷取重新整理權杖的URL。 |
| `authSpec.spec.properties.accessTokenUrl` | 用來擷取重新整理權杖的URL。 |
| `authSpec.spec.properties.requestParameterOverride` | 可讓您指定認證引數以在驗證時覆寫。 |
| `authSpec.spec.required` | 顯示驗證所需的認證。 | `accessToken` |

{style="table-layout:auto"}

+++

### 基本驗證

基本驗證是一種驗證型別，可讓您使用帳戶使用者名稱和帳戶密碼的組合來存取應用程式。

+++ 檢視基本驗證的範例

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
| `authSpec.name` | 顯示支援的驗證型別名稱。 | `Basic Authentication` |
| `authSpec.type` | 定義來源支援的驗證型別。 | `BasicAuthentication` |
| `authSpec.spec` | 包含驗證結構、資料型別和屬性的相關資訊。 |
| `authSpec.spec.$schema` | 定義用於驗證的結構描述。 | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | 定義結構描述的資料型別。 | `object` |
| `authSpec.spec.description` | 顯示您驗證型別的特定進一步資訊。 |
| `authSpec.spec.properties` | 包含用於驗證的認證的相關資訊。 |
| `authSpec.spec.properties.username` | 與您的應用程式相關聯的帳戶使用者名稱。 |
| `authSpec.spec.properties.password` | 與您的應用程式關聯的帳戶密碼。 |
| `authSpec.spec.required` | 指定在Experience Platform中輸入必填欄位。 | `username` |

{style="table-layout:auto"}

+++

### API金鑰驗證 {#api-key-authentication}

API金鑰驗證是在要求中提供API金鑰和其他相關驗證引數，用來存取API的安全方法。 根據您的特定API資訊，您可以傳送API金鑰做為請求標頭、查詢引數或本文的一部分。

使用API金鑰驗證時，通常需要下列引數：

| 參數 | 類型 | 必要 | 說明 |
| --- | --- | --- | --- |
| `host` | 字串 | 無 | 資源URL |
| `authKey1` | 字串 | 是 | API存取所需的第一個驗證金鑰。 它通常會在請求標頭或查詢引數中傳送。 |
| `authKey2` | 字串 | 選填 | 第二個驗證金鑰。 如有需要，此金鑰常用來進一步驗證請求。 |
| `authKeyN` | 字串 | 選填 | 這是可視需要使用的其他驗證變數，但API除外。 |

{style="table-layout:auto"}

+++檢視API金鑰驗證

```json
{
  "name": "API Key Authentication",
  "type": "KeyBased",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "Define authentication parameters required for API access",
    "properties": {
      "host": {
        "type": "string",
        "description": "Enter resource URL host path"
      },
      "authKey1": {
        "type": "string",
        "format": "password",
        "title": "Authentication Key 1",
        "description": "Primary authentication key for accessing the API",
        "restAttributes": {
          "headerParamName": "X-Auth-Key1"
        }
      },
      "authKey2": {
        "type": "string",
        "format": "password",
        "title": "Authentication Key 2",
        "description": "Secondary authentication key, if required",
        "restAttributes": {
          "headerParamName": "X-Auth-Key2"
        }
      },
      ..
      ..
      "authKeyN": {
        "type": "string",
        "format": "password",
        "title": "Additional Authentication Key",
        "description": "Additional authentication keys as needed by the API",
        "restAttributes": {
          "headerParamName": "X-Auth-KeyN"
        }
      }
    },
    "required": [
      "authKey1"
    ]
  }
}
```

+++

### 驗證行為

您可以使用`restAttributes`引數來定義API金鑰應如何包含在要求中。 例如，在以下範例中，`headerParamName`屬性指出`X-Auth-Key1`應作為標頭傳送。

```json
  "restAttributes": {
      "headerParamName": "X-Auth-Key1"
  }
```

每個驗證金鑰（例如`authKey1`、`authKey2`等）都可以與`restAttributes`相關聯，以指定它們作為要求傳送的方式。

如果`authKey1`有`"headerParamName": "X-Auth-Key1"`。 這表示要求標頭應包含`X-Auth-Key:{YOUR_AUTH_KEY1}`。 此外，金鑰名稱和`headerParamName`不一定必須相同。 例如：

* `authKey1`可以有`headerParamName: X-Custom-Auth-Key`。 這表示要求標頭將使用`X-Custom-Auth-Key`而非`authKey1`。
* 相反地，`authKey1`可以有`headerParamName: authKey1`。 這表示要求標頭名稱保持不變。

**範例API格式**

```http
GET /data?X-Auth-Key1={YOUR_AUTH_KEY1}&X-Auth-Key2={YOUR_AUTH_KEY2}
```

## 驗證規格範例

以下是使用[[!DNL MailChimp Members]](../../tutorials/api/create/marketing-automation/mailchimp-members.md)來源的已完成驗證規格的範例。

+++檢視驗證規格範例

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

+++

## 後續步驟

填入您的驗證規格後，您可以繼續設定您要整合至平台的來源的來源規格。 如需詳細資訊，請參閱[設定來源規格](./sourcespec.md)上的檔案。
