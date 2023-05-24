---
title: 審核事件終結點
description: 瞭解如何調用Reactor API中的/audit_events終結點。
exl-id: 59cd58dc-4085-47b7-846f-d3937740dd9b
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 3%

---

# 審核事件終結點

>[!WARNING]
>
>執行 `/audit_events` 端點在添加、刪除和重新處理特徵時處於流量狀態。

審計事件是在進行更改時生成的對反應器API中的另一個資源的特定更改的記錄。 這些是可通過使用 [回調](./callbacks.md)。 的 `/audit_events` Reactor API中的端點允許您以寫程式方式管理體驗應用程式中的審計事件。

審核事件以審核 `{RESOURCE_TYPE}.{EVENT}`，例如 `build.created` 或 `rule.updated`。

資源類型可以是下列任一類型：

* `property`
* `extension`
* `data_element`
* `rule`
* `rule_component`
* `library`
* `build`
* `environment`
* `host`

每種資源類型都支援以下事件：

* `created`
* `updated`
* `deleted`

## 快速入門

本指南中使用的端點是 [反應堆API](https://www.adobe.io/experience-platform-apis/references/reactor/)。 在繼續之前，請查看 [入門指南](../getting-started.md) 有關如何驗證到API的重要資訊。

## 檢索審計事件清單 {#list}

通過向以下對象發出GET請求，您可以檢索組織擁有的所有屬性的審計事件清單 `/audit_events` 端點。

**API格式**

```http
GET /audit_events
```

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/audit_events \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的響應返回審計事件清單。 下面的示例響應已被截斷為空間。

```json
{
  "data": [
    {
      "id": "AEa98742de8ef044d8b86767aa6a15a674",
      "type": "audit_events",
      "attributes": {
        "attributed_to_display_name": "John Smith",
        "attributed_to_email": "jsmith@example.com",
        "created_at": "2020-12-14T17:31:21.836Z",
        "display_name": "Kessel Apns App",
        "type_of": "app_configuration.updated",
        "updated_at": "2020-12-14T17:31:21.836Z",
        "entity": "{\"data\":{\"id\":\"AC40c339ab80d24c958b90d67b698602eb\",\"type\":\"app_configurations\",\"links\":{\"self\":\"https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb\",\"company\":\"https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1\"},\"attributes\":{\"name\":\"Kessel Apns App\",\"app_id\":\"com.adobe.test_app_2\",\"key_type\":\"p8_file\",\"platform\":\"mobile\",\"created_at\":\"2020-12-14T17:31:10.626Z\",\"updated_at\":\"2020-12-14T17:31:21.787Z\",\"messaging_service\":\"apns\"},\"relationships\":{\"company\":{\"data\":{\"id\":\"CO2bf094214ffd4785bb4bcf88c952a7c1\",\"type\":\"companies\"},\"links\":{\"related\":\"https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company\"}}}}}"
      },
      "relationships": {
        "property": {
          "links": {
            "related": null
          },
          "data": null
        },
        "entity": {
          "links": {
            "related": null
          },
          "data": {
            "type": "app_configurations",
            "id": "AC40c339ab80d24c958b90d67b698602eb"
          }
        }
      },
      "links": {
        "entity": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb",
        "property": null,
        "self": "https://reactor.adobe.io/audit_events/AEa98742de8ef044d8b86767aa6a15a674"
      }
    },
    {
      "id": "AE7320b6c1c3f84bb69405fcfe9cb58189",
      "type": "audit_events",
      "attributes": {
        "attributed_to_display_name": "John Smith",
        "attributed_to_email": "jsmith@example.com",
        "created_at": "2020-12-14T17:31:10.672Z",
        "display_name": "Kessel Apns App",
        "type_of": "app_configuration.created",
        "updated_at": "2020-12-14T17:31:10.672Z",
        "entity": "{\"data\":{\"id\":\"AC40c339ab80d24c958b90d67b698602eb\",\"type\":\"app_configurations\",\"links\":{\"self\":\"https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb\",\"company\":\"https://reactor.adobe.io/companies/CO2bf094214ffd4785bb4bcf88c952a7c1\"},\"attributes\":{\"name\":\"Kessel Apns App\",\"app_id\":\"com.adobe.test_app\",\"key_type\":\"p8_file\",\"platform\":\"mobile\",\"created_at\":\"2020-12-14T17:31:10.626Z\",\"updated_at\":\"2020-12-14T17:31:10.626Z\",\"messaging_service\":\"apns\"},\"relationships\":{\"company\":{\"data\":{\"id\":\"CO2bf094214ffd4785bb4bcf88c952a7c1\",\"type\":\"companies\"},\"links\":{\"related\":\"https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb/company\"}}}}}"
      },
      "relationships": {
        "property": {
          "links": {
            "related": null
          },
          "data": null
        },
        "entity": {
          "links": {
            "related": null
          },
          "data": {
            "type": "app_configurations",
            "id": "AC40c339ab80d24c958b90d67b698602eb"
          }
        }
      },
      "links": {
        "entity": "https://reactor.adobe.io/app_configurations/AC40c339ab80d24c958b90d67b698602eb",
        "property": null,
        "self": "https://reactor.adobe.io/audit_events/AE7320b6c1c3f84bb69405fcfe9cb58189"
      }
    }
  ],
  "links": {
    "self": "https://reactor.adobe.io/audit_events?page%5Bnumber%5D=1&page%5Bsize%5D=25",
    "next": "https://reactor.adobe.io/audit_events?page%5Bnumber%5D=2&page%5Bsize%5D=25",
    "last": "https://reactor.adobe.io/audit_events?page%5Bnumber%5D=129&page%5Bsize%5D=25"
  },
  "meta": {
    "pagination": {
      "current_page": 1,
      "next_page": null,
      "prev_page": null,
      "total_pages": 1,
      "total_count": 2
    }
  }
}
```

## 查找審核事件 {#lookup}

您可以通過在GET請求的路徑中提供其ID來查找審計事件。

**API格式**

```http
GET /audit_events/{AUDIT_EVENT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `AUDIT_EVENT_ID` | 的 `id` 查找的審核事件。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/audit_events/AEa98742de8ef044d8b86767aa6a15a674 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的響應將返回審計事件的詳細資訊。

```json
{
  "data": {
    "id": "AEd6a3b381fb8241818d7520001f8bd459",
    "type": "audit_events",
    "attributes": {
      "attributed_to_display_name": "John Smith",
      "attributed_to_email": "jsmith@example.com",
      "created_at": "2020-12-14T17:31:46.956Z",
      "display_name": "Example Rule",
      "type_of": "rule.created",
      "updated_at": "2020-12-14T17:31:46.956Z",
      "entity": "{\"data\":{\"id\":\"RL52d156a9074844b89ca20c987dbafd3b\",\"meta\":{\"latest_revision_number\":0},\"type\":\"rules\",\"links\":{\"self\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b\",\"origin\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b\",\"property\":\"https://reactor.adobe.io/properties/PR03cc61073ef74fd2af21e4cfb6ed97a7\",\"rule_components\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/rule_components\"},\"attributes\":{\"name\":\"Example Rule\",\"dirty\":true,\"enabled\":true,\"published\":false,\"created_at\":\"2020-12-14T17:31:46.883Z\",\"deleted_at\":null,\"updated_at\":\"2020-12-14T17:31:46.883Z\",\"published_at\":null,\"review_status\":\"unsubmitted\",\"revision_number\":0},\"relationships\":{\"notes\":{\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/notes\"}},\"origin\":{\"data\":{\"id\":\"RL52d156a9074844b89ca20c987dbafd3b\",\"type\":\"rules\"},\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/origin\"}},\"property\":{\"data\":{\"id\":\"PR03cc61073ef74fd2af21e4cfb6ed97a7\",\"type\":\"properties\"},\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/property\"}},\"libraries\":{\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/libraries\"}},\"revisions\":{\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/revisions\"}},\"rule_components\":{\"links\":{\"related\":\"https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b/rule_components\"}}}}}"
    },
    "relationships": {
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/audit_events/AEd6a3b381fb8241818d7520001f8bd459/property"
        },
        "data": {
          "id": "PR03cc61073ef74fd2af21e4cfb6ed97a7",
          "type": "properties"
        }
      },
      "entity": {
        "links": {
          "related": "https://reactor.adobe.io/audit_events/AEd6a3b381fb8241818d7520001f8bd459/rule"
        },
        "data": {
          "type": "rules",
          "id": "RL52d156a9074844b89ca20c987dbafd3b"
        }
      }
    },
    "links": {
      "entity": "https://reactor.adobe.io/rules/RL52d156a9074844b89ca20c987dbafd3b",
      "property": "https://reactor.adobe.io/properties/PR03cc61073ef74fd2af21e4cfb6ed97a7",
      "self": "https://reactor.adobe.io/audit_events/AEd6a3b381fb8241818d7520001f8bd459"
    },
    "meta": {
      "property_name": "Kessel Example Property"
    }
  }
}
```
