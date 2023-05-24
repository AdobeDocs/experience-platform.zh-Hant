---
title: 應用程式配置終結點
description: 瞭解如何調用Reactor API中的/app_configurations終結點。
exl-id: 88a1ec36-b4d2-4fb6-92cb-1da04268492a
source-git-commit: 36320addc790e844a1102314890e8692841dc5d0
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 4%

---

# 應用程式配置終結點

>[!WARNING]
>
>執行 `/app_configurations` 端點在添加、刪除和重新處理特徵時處於流量狀態。

應用程式配置允許儲存和檢索憑據以供以後使用。 的 `/app_configurations` Reactor API中的終結點允許您以寫程式方式管理體驗應用程式中的應用程式配置。

## 快速入門

本指南中使用的端點是 [反應堆API](https://www.adobe.io/experience-platform-apis/references/reactor/)。 在繼續之前，請查看 [入門指南](../getting-started.md) 有關如何驗證到API的重要資訊。

## 檢索應用配置清單 {#list}

**API格式**

```http
GET /companies/{COMPANY_ID}/app_configurations
```

| 參數 | 說明 |
| --- | --- |
| `COMPANY_ID` | 的 `id` 的 [公司](./companies.md) 擁有應用配置的用戶。 |

{style="table-layout:auto"}

>[!NOTE]
>
>使用查詢參數，可以根據以下屬性篩選列出的應用程式配置：<ul><li>`app_id`</li><li>`created_at`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`updated_at`</li></ul>請參閱上的指南 [過濾響應](../guides/filtering.md) 的子菜單。

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

成功的響應返回應用配置清單。

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

## 查找應用配置 {#lookup}

通過在GET請求路徑中提供其ID，可以查找應用配置。

**API格式**

```http
GET /app_configurations/{APP_CONFIGURATION_ID}
```

| 參數 | 說明 |
| --- | --- |
| `APP_CONFIGURATION_ID` | 的 `id` 查找的應用配置。 |

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

成功的響應返回應用配置的詳細資訊。

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

## 建立應用配置 {#create}

通過發出POST請求，可以建立新的應用配置。

**API格式**

```http
POST /companies/{COMPANY_ID}/app_configurations
```

| 參數 | 說明 |
| --- | --- |
| `COMPANY_ID` | 的 `id` 的 [公司](./companies.md) 定義應用程式配置。 |

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
| `platform` | 應用程式在（Web或移動）上運行的平台。 這將確定哪些消息服務可用。 |
| `messaging_service` | 與應用關聯的消息服務，如 [Apple推送通知服務(APN)](https://developer.apple.com/library/archive/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html) 和 [Firebase雲消息(FCM)](https://firebase.google.com/docs/cloud-messaging)。 這確定可以使用哪些鍵類型。 |
| `key_type` | 表示推送服務供應商支援的協定並確定 `push_credential` 的雙曲餘切值。 隨著消息服務協定的發展， `key_type` 建立值以支援更新的協定。 |
| `push_credential` | 實際憑據值，在靜態時加密。 此欄位通常不被解密或包含在API響應中。 只有某些Adobe服務才能獲取包含解密的推送憑據的響應。 |

{style="table-layout:auto"}

**回應**

成功的響應將返回新建立的應用程式配置的詳細資訊。

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

## 更新應用配置

通過在PATCH請求路徑中包含應用配置ID，可以更新應用配置。

**API格式**

```http
PATCH /app_configurations/{APP_CONFIGURATION_ID}
```

| 參數 | 說明 |
| --- | --- |
| `APP_CONFIGURATION_ID` | 的 `id` 要更新的應用配置。 |

{style="table-layout:auto"}

**要求**

以下請求更新 `app_id` 為現有應用配置。

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
| `attributes` | 其屬性表示要為應用程式配置更新的屬性的對象。 每個鍵都表示要更新的特定應用程式配置屬性以及應更新到的相應值。<br><br>可以為應用配置更新以下屬性：<ul><li>`app_id`</li><li>`key_type`</li><li>`messaging_service`</li><li>`name`</li><li>`platform`</li><li>`push_credential`</li></ul> |
| `id` | 的 `id` 要更新的應用配置。 這應與 `{APP_CONFIGURATION_ID}` 請求路徑中提供的值。 |
| `type` | 要更新的資源類型。 對於此終結點，值必須為 `app_configurations`。 |

{style="table-layout:auto"}

**回應**

成功的響應將返回更新的應用配置的詳細資訊。

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

## 刪除應用配置

通過在DELETE請求的路徑中包含應用配置的ID，可以刪除它。

**API格式**

```http
DELETE /app_configurations/{APP_CONFIGURATION_ID}
```

| 參數 | 說明 |
| --- | --- |
| `APP_CONFIGURATION_ID` | 的 `id` 刪除的應用配置。 |

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

成功的響應返回沒有響應正文的HTTP狀態204（無內容），表示應用配置已被刪除。
