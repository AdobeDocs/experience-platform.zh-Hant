---
title: 公司端點
description: 了解如何在Reactor API中呼叫/companys端點。
exl-id: ee435358-ed34-4e0c-93af-796133fb11fc
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 3%

---

# 公司端點

公司代表客戶組織，通常是企業。 在Reactor API中，這些公司會比對1:1與組織ID。 API使用者只能查看其有權存取的公司。 公司可能包含許多 [屬性](./properties.md). 屬性只屬於一個公司。

此 `/companies` reactor API中的端點可讓您以程式設計方式擷取您在experience應用程式中可存取的公司。

## 快速入門

本指南中使用的端點屬於 [Reactor API](https://www.adobe.io/experience-platform-apis/references/reactor/). 繼續之前，請檢閱 [快速入門手冊](../getting-started.md) 以取得如何驗證API的重要資訊。

## 擷取公司清單 {#list}

您可以向 `/companies` 端點。 在大多數情況下，只有一個。

**API格式**

```http
GET /companies
```

>[!NOTE]
>
>您可以使用查詢參數，根據下列屬性來篩選上市公司：<ul><li>`created_at`</li><li>`name`</li><li>`org_id`</li><li>`token`</li><li>`updated_at`</li></ul>請參閱 [篩選回應](../guides/filtering.md) 以取得更多資訊。

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/companies \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回您有權存取的公司清單。

```json
{
  "data": [
    {
      "id": "COdb0cd64ad4524440be94b8496416ec7d",
      "type": "companies",
      "attributes": {
        "created_at": "2020-08-13T17:13:30.667Z",
        "name": "Example Company",
        "org_id": "{ORG_ID}",
        "updated_at": "2020-08-13T17:13:30.667Z",
        "token": "d5a4f682bbae",
        "cjm_enabled": false,
        "edge_enabled": false,
        "edge_events_allotment": null,
        "edge_fanout_ratio": null
      },
      "relationships": {
        "properties": {
          "links": {
            "related": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
          }
        }
      },
      "links": {
        "self": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d",
        "properties": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
      },
      "meta": {
        "rights": [
          "develop_extensions",
          "manage_properties"
        ],
        "platform_rights": {
          "web": [
            "develop_extensions",
            "manage_properties"
          ],
          "mobile": [
            "develop_extensions",
            "manage_properties"
          ]
        }
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

## 查找公司 {#lookup}

您可以在請求的路徑中加入特定公司ID，借此查詢其GET。

**API格式**

```http
GET /companies/{COMPANY_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{COMPANY_ID}` | 此 `id` 貴公司的價值。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的回應會傳回公司的詳細資訊。

```json
{
  "data": {
    "id": "COdb0cd64ad4524440be94b8496416ec7d",
    "type": "companies",
    "attributes": {
      "created_at": "2020-08-13T17:13:30.667Z",
      "name": "Example Company",
      "org_id": "{ORG_ID}",
      "updated_at": "2020-08-13T17:13:30.667Z",
      "token": "d5a4f682bbae",
      "cjm_enabled": false,
      "edge_enabled": false,
      "edge_events_allotment": null,
      "edge_fanout_ratio": null
    },
    "relationships": {
      "properties": {
        "links": {
          "related": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
        }
      }
    },
    "links": {
      "self": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d",
      "properties": "https://reactor.adobe.io/companies/COdb0cd64ad4524440be94b8496416ec7d/properties"
    },
    "meta": {
      "rights": [
        "develop_extensions",
        "manage_properties"
      ],
      "platform_rights": {
        "web": [
          "develop_extensions",
          "manage_properties"
        ],
        "mobile": [
          "develop_extensions",
          "manage_properties"
        ]
      }
    }
  }
}
```
