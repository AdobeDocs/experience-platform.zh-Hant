---
keywords: Experience Platform；首頁；熱門主題；源；連接器；源連接器；源sdk;sdk;SDK
title: 配置自助源的驗證規範（批處理SDK）
topic-legacy: overview
description: 本文檔概述了使用自助源（批處理SDK）所需準備的配置。
exl-id: 68ed22fe-1f22-46d2-9d58-72ad8a9e6b98
source-git-commit: 4d7799b01c34f4b9e4a33c130583eadcfdc3af69
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 2%

---

# 配置自助源的驗證規範（批處理SDK）

身份驗證規範定義了Adobe Experience Platform用戶如何連接到源。

的 `authSpec` array包含有關將源連接到平台所需的身份驗證參數的資訊。 任何給定源都可支援多種不同類型的身份驗證。

## 驗證規範

自助源（批處理SDK）支援OAuth 2刷新代碼和基本身份驗證。 有關使用OAuth 2刷新代碼和基本身份驗證的指導，請參閱下表

### OAuth 2刷新代碼

OAuth 2刷新代碼允許通過生成臨時訪問令牌和刷新令牌來安全訪問應用程式。 訪問令牌允許您安全地訪問您的資源而無需提供其他憑據，而刷新令牌允許您在訪問令牌過期後生成新的訪問令牌。

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
      "host",
      "accessToken"
    ]
  }
}
```

| 屬性 | 說明 | 範例 |
| --- | --- | --- |
| `authSpec.name` | 顯示支援的身份驗證類型的名稱。 | `oAuth2-refresh-code` |
| `authSpec.type` | 定義源支援的驗證類型。 | `oAuth2-refresh-code` |
| `authSpec.spec` | 包含有關驗證的架構、資料類型和屬性的資訊。 |
| `authSpec.spec.$schema` | 定義用於驗證的架構。 | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | 定義架構的資料類型。 | `object` |
| `authSpec.spec.properties` | 包含有關用於身份驗證的憑據的資訊。 |
| `authSpec.spec.properties.description` | 顯示有關憑據的簡短說明。 |
| `authSpec.spec.properties.type` | 定義憑據的資料類型。 | `string` |
| `authSpec.spec.properties.clientId` | 與應用程式關聯的客戶端ID。 客戶端ID與您的客戶端密碼一起使用以檢索您的訪問令牌。 |
| `authSpec.spec.properties.clientSecret` | 與應用程式關聯的客戶端密碼。 客戶機密鑰與您的客戶機ID一起使用以檢索您的訪問令牌。 |
| `authSpec.spec.properties.accessToken` | 訪問令牌授權您對應用程式的安全訪問。 |
| `authSpec.spec.properties.refreshToken` | 當訪問令牌過期時，刷新令牌用於生成新的訪問令牌。 |
| `authSpec.spec.properties.expirationDate` | 定義訪問令牌的到期日期。 |
| `authSpec.spec.properties.refreshTokenUrl` | 用於檢索刷新標籤的URL。 |
| `authSpec.spec.properties.accessTokenUrl` | 用於檢索刷新標籤的URL。 |
| `authSpec.spec.properties.requestParameterOverride` | 允許您指定驗證時要覆蓋的憑據參數。 |
| `authSpec.spec.required` | 顯示驗證所需的憑據。 | `accessToken` |

{style=&quot;table-layout:auto&quot;}


### 基本身份驗證

基本身份驗證是一種身份驗證類型，允許您使用應用程式的主機URL、帳戶用戶名和帳戶密碼的組合來訪問應用程式。

```json
{
  "name": "Basic Authentication",
  "type": "BasicAuthentication",
  "spec": {
    "$schema": "http://json-schema.org/draft-07/schema#",
    "type": "object",
    "description": "defines auth params required for connecting to rest service.",
    "properties": {
      "host": {
        "type": "string",
        "description": "Enter resource url host path"
      },
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
      "host",
      "username",
      "password"
    ]
  }
}
```

| 屬性 | 說明 | 範例 |
| --- | --- | --- |
| `authSpec.name` | 顯示支援的身份驗證類型的名稱。 | `Basic Authentication` |
| `authSpec.type` | 定義源支援的驗證類型。 | `BasicAuthentication` |
| `authSpec.spec` | 包含有關驗證的架構、資料類型和屬性的資訊。 |
| `authSpec.spec.$schema` | 定義用於驗證的架構。 | `http://json-schema.org/draft-07/schema#` |
| `authSpec.spec.type` | 定義架構的資料類型。 | `object` |
| `authSpec.spec.description` | 顯示特定於身份驗證類型的詳細資訊。 |
| `authSpec.spec.properties` | 包含有關用於身份驗證的憑據的資訊。 |
| `authSpec.spec.properties.host` | 應用程式的主機URL。 |
| `authSpec.spec.properties.username` | 與應用程式關聯的帳戶用戶名。 |
| `authSpec.spec.properties.password` | 與應用程式關聯的帳戶密碼。 |
| `authSpec.spec.required` | 指定在平台中輸入的必需值所需的欄位。 | `host` |

{style=&quot;table-layout:auto&quot;&quot;

## 驗證規範示例

以下是使用 [[!DNL MailChimp Members]](../../tutorials/api/create/marketing-automation/mailchimp-members.md) 源。

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
          "host": {
            "type": "string",
            "description": "Enter resource url host path"
          },
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
          "host",
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
          "host": {
            "type": "string",
            "description": "Enter resource url host path."
          },
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
          "host",
          "username",
          "password"
        ]
      }
    }
  ],
```

## 後續步驟

在填充了驗證規範後，您可以繼續為要整合到平台的源配置源規範。 查看上的文檔 [配置源規範](./sourcespec.md) 的子菜單。
