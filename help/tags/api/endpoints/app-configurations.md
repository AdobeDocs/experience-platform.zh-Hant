---
title: 應用配置端點
description: 了解如何在Reactor API中呼叫/app_configurations端點。
exl-id: 88a1ec36-b4d2-4fb6-92cb-1da04268492a
source-git-commit: 36320addc790e844a1102314890e8692841dc5d0
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 4%

---

# 應用配置端點

>[!WARNING]
>
>實施 `/app_configurations` 隨著功能的添加、刪除和重作，端點處於通量中。

應用程式設定可儲存及擷取憑證以供日後使用。 此 `/app_configurations` reactor API中的端點可讓您以程式設計方式管理experience應用程式中的應用程式設定。

## 快速入門

本指南中使用的端點屬於 [Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/). 繼續之前，請檢閱 [快速入門手冊](../getting-started.md) 以取得如何驗證API的重要資訊。

## 擷取應用程式設定清單 {#list}

**API格式**

```http
GET /companies/{COMPANY_ID}/app_configurations
```

| 參數 | 說明 |
| --- | --- |
| `COMPANY_ID` | 此 `id` 的 [公司](./companies.md) 擁有應用程式設定。 |

{style="table-layout:auto"}

>[!NOTE]
>
>您可以使用查詢參數，根據下列屬性來篩選列出的應用程式設定：<ul><li>`app_id`</li><li>`created_at`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`updated_at`</li></ul>請參閱 [篩選回應](../guides/filtering.md) 以取得更多資訊。

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/app_configurations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回應用程式設定清單。

```json
{
  "data": [
    {
      "id": "AC40c339ab80d24c958b90d67b698602eb",
      "type": "app_configurations",
      "attributes": {
        "created_at": "2020-12-14T17:31:10.626Z",
        "updated_at": "2020-12-14T17:31:10.626Z",
        "app_id": "com.adobe.test_app",
        "name": "Kessel Apns App",
        "platform": "mobile",
        "messaging_service": "apns",
        "key_type": "p8_file"
      },
      "relationships": {
        "company": {
          "links": {
            "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
          },
          "data": {
            "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
            "type": "companies"
          }
        }
      },
      "links": {
        "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
        "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
      }
    }
  ],
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 1
    }
  }
}
```

## 查詢應用程式設定 {#lookup}

您可以在應用程式請求的路徑中提供其ID，以查詢應用程式設定。

**API格式**

```http
GET /app_configurations/{APP_CONFIGURATION_ID}
```

| 參數 | 說明 |
| --- | --- |
| `APP_CONFIGURATION_ID` | 此 `id` 的應用程式設定。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回應用程式設定的詳細資訊。

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:10.626Z",
      "app_id": "com.adobe.test_app",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## 建立應用程式設定 {#create}

您可以提出POST要求，以建立新的應用程式設定。

**API格式**

```http
POST /companies/{COMPANY_ID}/app_configurations
```

| 參數 | 說明 |
| --- | --- |
| `COMPANY_ID` | 此 `id` 的 [公司](./companies.md) 定義應用程式設定時所使用之區段。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X POST \
  https://reactor.adobe.io/companies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "attributes": {
            "name": "Kessel Apns App",
            "app_id": "com.adobe.test_app",
            "platform": "mobile",
            "messaging_service": "apns",
            "key_type": "p8_file",
            "push_credential": {
              "bundleId": "com.adobe.test_app",
              "keyId": "{KEY_ID}",
              "p8": "{SECRET}",
              "teamId": "{TEAM_ID}"
            }
          },
          "type": "app_configurations"
        }
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `platform` | 應用程式在（網頁或行動裝置）上執行的平台。 這決定了哪些報文傳送服務可用。 |
| `messaging_service` | 與應用程式相關聯的傳訊服務，例如 [Apple推播通知服務(APN)](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html) 和 [Firebase雲端傳訊(FCM)](https://firebase.google.com/docs/cloud-messaging). 這會決定可使用的索引鍵類型。 |
| `key_type` | 代表推送服務供應商支援的通訊協定，並決定 `push_credential` 物件。 隨著報文傳送服務協定的發展，新 `key_type` 會建立值以支援更新的通訊協定。 |
| `push_credential` | 實際憑據值，在靜止時加密。 此欄位通常不會解密或包含在API回應中。 只有特定Adobe服務能取得包含已解密推送憑證的回應。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回新建立之應用程式設定的詳細資訊。

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:10.626Z",
      "app_id": "com.adobe.test_app",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## 更新應用程式設定

您可以在PATCH請求的路徑中加入應用程式設定ID，以更新應用程式設定。

**API格式**

```http
PATCH /app_configurations/{APP_CONFIGURATION_ID}
```

| 參數 | 說明 |
| --- | --- |
| `APP_CONFIGURATION_ID` | 此 `id` 的應用程式設定。 |

{style="table-layout:auto"}

**要求**

下列請求會更新 `app_id` （適用於現有應用程式設定）。

```shell
curl -X PATCH \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -H 'Accept: application/vnd.api+json;revision=1' \
  -d '{
        "data": {
          "attributes": {
            "app_id": "com.adobe.test_app_2"
          },
          "id": "AC40c339ab80d24c958b90d67b698602eb",
          "type": "app_configurations"
        }
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `attributes` | 一個物件，其屬性代表要針對應用程式設定更新的屬性。 每個索引鍵代表要更新的特定應用程式設定屬性，以及應更新的對應值。<br><br>可針對應用程式設定更新下列屬性：<ul><li>`app_id`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`push_credential`</li></ul> |
| `id` | 此 `id` 的應用程式設定。 這應符合 `{APP_CONFIGURATION_ID}` 值。 |
| `type` | 要更新的資源類型。 對於此端點，值必須是 `app_configurations`. |

{style="table-layout:auto"}

**回應**

成功的回應會傳回更新應用程式設定的詳細資訊。

```json
{
  "data": {
    "id": "AC40c339ab80d24c958b90d67b698602eb",
    "type": "app_configurations",
    "attributes": {
      "created_at": "2020-12-14T17:31:10.626Z",
      "updated_at": "2020-12-14T17:31:21.787Z",
      "app_id": "com.adobe.test_app_2",
      "name": "Kessel Apns App",
      "platform": "mobile",
      "messaging_service": "apns",
      "key_type": "p8_file"
    },
    "relationships": {
      "company": {
        "links": {
          "related": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company"
        },
        "data": {
          "id": "CO2bf094214ffd4785bb4bcf88c952a7c1",
          "type": "companies"
        }
      }
    },
    "links": {
      "company": "https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1",
      "self": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb"
    }
  }
}
```

## 刪除應用程式設定

您可以在DELETE請求的路徑中加入應用程式設定ID，以刪除該設定。

**API格式**

```http
DELETE /app_configurations/{APP_CONFIGURATION_ID}
```

| 參數 | 說明 |
| --- | --- |
| `APP_CONFIGURATION_ID` | 此 `id` 刪除的應用程式設定。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X DELETE \
  https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回HTTP狀態204（無內容），但沒有回應內文，表示應用程式設定已刪除。
