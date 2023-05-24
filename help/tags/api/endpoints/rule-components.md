---
title: 規則元件終結點
description: 瞭解如何調用Reactor API中的/rule_components端點。
exl-id: 8a878a89-7f41-45fc-88f3-17f0f743e29c
source-git-commit: e602f78470fe4eeb2a42e6333ba52096d8a9fe8a
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 3%

---

# 規則元件終結點

在資料收集標籤中， [規則](./rules.md) 控制已部署中資源的行為 [庫](./libraries.md)。 **規則元件** 是構成規則的各個部分。 如果規則是配方，則規則元件是配料之一。 的 `/rule_components` Reactor API中的端點允許您以寫程式方式管理規則元件。

>[!NOTE]
>
>本文檔介紹如何管理Reactor API中的規則元件。 有關如何與UI中的規則和規則元件交互的詳細資訊，請參閱 [UI指南](../../ui/managing-resources/rules.md)。

規則元件有三種基本類型：

| 規則元件類型 | 說明 |
| --- | --- |
| 活動 | 事件是規則的觸發器。 規則在客戶端設備上運行時發生事件時啟動。 &quot;[!UICONTROL 庫載入]&quot;, &quot;[!UICONTROL 頁首]&quot;和&quot;[!UICONTROL 按一下]&quot;是事件的示例。 |
| 條件 | 條件是評估在執行任何操作之前是否滿足某些標準。 一旦發生事件，將評估條件。 僅當滿足所有條件時才執行規則的操作。 |
| 動作 | 這些是您希望規則實際執行的操作，例如發送Adobe Analytics信標、檢索自定義訪問者ID或觸發特定框。 |

{style="table-layout:auto"}

規則元件只屬於一個規則。 規則可以（並且應該）具有許多規則元件。

規則元件僅由 [擴展](./extensions.md)。 擴展可提供許多規則元件類型。

## 快速入門

本指南中使用的端點是 [反應堆API](https://www.adobe.io/experience-platform-apis/references/reactor/)。 在繼續之前，請查看 [入門指南](../getting-started.md) 有關如何驗證到API的重要資訊。

## 檢索規則元件清單 {#list}

通過將規則的ID包括在GET請求的路徑中，可以檢索屬於規則的規則元件清單。

**API格式**

```http
GET /rules/{RULE_ID}/rule_components
```

| 參數 | 說明 |
| --- | --- |
| `RULE_ID` | 的 `id` 要列出其元件的規則。 |

{style="table-layout:auto"}

>[!NOTE]
>
>使用查詢參數，可以根據以下屬性篩選列出的規則元件：<ul><li>`created_at`</li><li>`dirty`</li><li>`enabled`</li><li>`name`</li><li>`negate`</li><li>`origin_id`</li><li>`published`</li><li>`published_at`</li><li>`revision_number`</li><li>`updated_at`</li></ul>請參閱上的指南 [過濾響應](../guides/filtering.md) 的子菜單。

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/rules/RL14dc6a8c37b14b619ddb2b3ba489a1f51/rule_components \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的響應將返回指定規則的規則元件清單。

```json
{
  "data": [
    {
      "id": "RC45944086902c4828b6e14ffbb40017f4",
      "type": "rule_components",
      "attributes": {
        "created_at": "2020-12-14T17:54:34.976Z",
        "delegate_descriptor_id": "kessel-test::events::click",
        "deleted_at": null,
        "dirty": true,
        "name": "My Example Click Event",
        "negate": false,
        "order": 0,
        "rule_order": 50.0,
        "timeout": 2000,
        "delay_next": true,
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:54:34.976Z",
        "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
      },
      "relationships": {
        "updated_with_extension_package": {
          "links": {
            "related": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/updated_with_extension_package"
          },
          "data": {
            "id": "EP75db2452065b44e2b8a38ca883ce369a",
            "type": "extension_packages"
          }
        },
        "updated_with_extension": {
          "links": {
            "related": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/updated_with_extension"
          },
          "data": {
            "id": "EX6312cea676de47ad9f70b42f7c0fbf02",
            "type": "extensions"
          }
        },
        "extension": {
          "links": {
            "related": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/extension"
          },
          "data": {
            "id": "EXbfd099788024423ebdd49cf06b52e50a",
            "type": "extensions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/notes"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/origin"
          },
          "data": {
            "id": "RC45944086902c4828b6e14ffbb40017f4",
            "type": "rule_components"
          }
        },
        "rule component": {
          "links": {
            "related": "https://reactor.adobe.io/properties/PRb1090b7443e948ac91650964b490e622"
          },
          "data": {
            "id": "PRb1090b7443e948ac91650964b490e622",
            "type": "properties"
          }
        },
        "rules": {
          "links": {
            "related": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/rules"
          }
        }
      },
      "links": {
        "extension": "https://reactor.adobe.io/extensions/EXbfd099788024423ebdd49cf06b52e50a",
        "origin": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4",
        "rules": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4/rules",
        "self": "https://reactor.adobe.io/rule_components/RC45944086902c4828b6e14ffbb40017f4"
      },
      "meta": {
        "latest_revision_number": 0
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

## 查找規則元件 {#lookup}

通過在GET請求的路徑中提供規則元件的ID，可以查找規則元件。

**API格式**

```http
GET /rule_components/{RULE_COMPONENT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `RULE_COMPONENT_ID` | 的 `id` 查找規則元件。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的響應返回規則元件的詳細資訊。

```json
{
  "data": {
    "id": "RC7be169fcfd534ffc82acc7bffdc50128",
    "type": "rule_components",
    "attributes": {
      "created_at": "2020-12-14T17:54:18.551Z",
      "delegate_descriptor_id": "kessel-test::events::click",
      "deleted_at": null,
      "dirty": true,
      "name": "My Example Click Event",
      "negate": false,
      "order": 0,
      "rule_order": 50.0,
      "timeout": 2000,
      "delay_next": true,
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:54:18.551Z",
      "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
    },
    "relationships": {
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/updated_with_extension"
        },
        "data": {
          "id": "EXa11e168f2ff2485197a493095269f964",
          "type": "extensions"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/extension"
        },
        "data": {
          "id": "EXa76eb16dd86849318b743494e75c33a1",
          "type": "extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/notes"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/origin"
        },
        "data": {
          "id": "RC7be169fcfd534ffc82acc7bffdc50128",
          "type": "rule_components"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR00a35a74381443dc994e6b30b7152106"
        },
        "data": {
          "id": "PR00a35a74381443dc994e6b30b7152106",
          "type": "properties"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/rules"
        }
      }
    },
    "links": {
      "extension": "https://reactor.adobe.io/extensions/EXa76eb16dd86849318b743494e75c33a1",
      "origin": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128",
      "rules": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128/rules",
      "self": "https://reactor.adobe.io/rule_components/RC7be169fcfd534ffc82acc7bffdc50128"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## 建立規則元件 {#create}

通過發出POST請求，可以建立新規則元件。

**API格式**

```http
POST /properties/{PROPERTY_ID}/rule_components
```

| 參數 | 說明 |
| --- | --- |
| `PROPERTY_ID` | 的 `id` 定義規則元件的屬性。 |

{style="table-layout:auto"}

**要求**

以下請求將建立新規則元件。 在有效載荷中， `relationships` 屬性將元件與特定規則和現有擴展關聯。 請參閱上的指南 [關係](../guides/relationships.md) 的子菜單。

```shell
curl -X POST \
  https://reactor.adobe.io/properties/PR97596432a82549ceb8e2a5d9df05c0e1/rule_components \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "delegate_descriptor_id": "kessel-test::events::click",
            "name": "My Example Click Event",
            "delay_next": true,
            "order": 0,
            "rule_order": 50.0,
            "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}",
            "timeout": 2000
          },
          "relationships": {
            "extension": {
              "data": {
                "id": "EX31b8c49f134b4307924d71a64204099e",
                "type": "extensions"
              }
            },
            "rules": {
              "data": [
                {
                  "id": "RLf7b4f416b2e04ae1ba857ae681fee5bc",
                  "type": "rules"
                }
              ]
            }
          },
          "type": "rule_components"
        }
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `attributes.delegate_descriptor_id` | **（必需）** 您可以定義的規則元件類型由 [擴展包](./extension-packages.md)。 建立新規則元件時，必須提供委託描述符ID以指示此規則元件所基於的擴展包、元件的類型（事件、條件或操作）以及由擴展定義的特定元件的名稱（如核心擴展中的「按一下」事件）。<br><br>請參閱上的指南 [委託描述符ID](../guides/delegate-descriptor-ids.md) 的子菜單。 |
| `attributes.name` | **（必需）** 規則元件的可讀名稱。 |
| `attributes.delay_next` | 一個布爾值，指示是否延遲以後的操作。 |
| `attributes.order` | 一個整數，指示按類型載入元件的順序。 |
| `attributes.rule_order` | 一個整數，指示要觸發的關聯規則的優先順序。 |
| `attributes.settings` | 以字串表示的設定JSON對象。 |
| `attributes.timeout` | 一個整數，指示按順序執行的操作的超時。 |
| `relationships` | 為規則元件建立必要關係的對象。 必須建立兩個關係： <ol><li>`extension`:定義此規則元件的擴展。 此擴展必須是由 `delegate_descriptor_id`。</li><li>`rules`:正在定義此元件的規則。</li></ol>有關關係的更多一般資訊，請參閱 [關係指南](../guides/relationships.md)。 |
| `type` | 正在建立的資源類型。 對於此終結點，值必須為 `rule_components`。 |

{style="table-layout:auto"}

**回應**

成功的響應將返回新建立的規則元件的詳細資訊。

```json
{
  "data": {
    "id": "RC78c44af3cf7644e5927fc0ad61e88940",
    "type": "rule_components",
    "attributes": {
      "created_at": "2020-12-14T17:54:00.232Z",
      "delegate_descriptor_id": "kessel-test::events::click",
      "deleted_at": null,
      "dirty": true,
      "name": "My Example Click Event",
      "negate": false,
      "order": 0,
      "rule_order": 50.0,
      "timeout": 2000,
      "delay_next": true,
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:54:00.232Z",
      "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
    },
    "relationships": {
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/updated_with_extension"
        },
        "data": {
          "id": "EX0019a115a74f401fa0b9bb8f57a0196b",
          "type": "extensions"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/extension"
        },
        "data": {
          "id": "EX31b8c49f134b4307924d71a64204099e",
          "type": "extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/notes"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/origin"
        },
        "data": {
          "id": "RC78c44af3cf7644e5927fc0ad61e88940",
          "type": "rule_components"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR97596432a82549ceb8e2a5d9df05c0e1"
        },
        "data": {
          "id": "PR97596432a82549ceb8e2a5d9df05c0e1",
          "type": "properties"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/rules"
        }
      }
    },
    "links": {
      "extension": "https://reactor.adobe.io/extensions/EX31b8c49f134b4307924d71a64204099e",
      "origin": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940",
      "rules": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940/rules",
      "self": "https://reactor.adobe.io/rule_components/RC78c44af3cf7644e5927fc0ad61e88940"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## 更新規則元件 {#update}

可以通過在PATCH請求的路徑中包含規則元件ID來更新規則元件。

>[!NOTE]
>
>更新規則元件還會更新父規則的 `updated_at` 時間戳。

**API格式**

```http
PATCH /rule_components/{RULE_COMPONENT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `RULE_COMPONENT_ID` | 的 `id` 更新的規則元件。 |

{style="table-layout:auto"}

**要求**

以下請求更新 `order` 和 `settings` 現有規則元件的屬性。

```shell
curl -X PATCH \
  https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'Content-Type: application/json' \
  -d '{
        "data": {
          "attributes": {
            "order": 1,
            "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":false}"
          },
          "type": "rule_components",
          "id": "RC9af052ee231346f28d1e44865ab62c04"
        }
      }'
```

| 屬性 | 說明 |
| --- | --- |
| `attributes` | 其規則元件表示要為規則元件更新的屬性的對象。 可以為規則元件更新以下屬性： <ul><li>`delay_next`</li><li>`delegate_descriptor_id`</li><li>`name`</li><li>`order`</li><li>`rule_order`</li><li>`settings`</li><li>`timeout`</li></ul> |
| `id` | 的 `id` 的子菜單。 這應與 `{RULE_COMPONENT_ID}` 請求路徑中提供的值。 |
| `type` | 要更新的資源類型。 對於此終結點，值必須為 `rule_components`。 |

{style="table-layout:auto"}

**回應**

成功的響應將返回更新的規則元件的詳細資訊。

```json
{
  "data": {
    "id": "RC9af052ee231346f28d1e44865ab62c04",
    "type": "rule_components",
    "attributes": {
      "created_at": "2020-12-14T17:54:50.887Z",
      "delegate_descriptor_id": "kessel-test::events::click",
      "deleted_at": null,
      "dirty": true,
      "name": "My Example Click Event",
      "negate": false,
      "order": 1,
      "rule_order": 50.0,
      "timeout": 2000,
      "delay_next": true,
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:54:52.553Z",
      "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":false}"
    },
    "relationships": {
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/updated_with_extension"
        },
        "data": {
          "id": "EX468796dd09d743858f17d4c5ca52f3e0",
          "type": "extensions"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/extension"
        },
        "data": {
          "id": "EXcedb08a8265c488e8bb98b46245b2486",
          "type": "extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/notes"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/origin"
        },
        "data": {
          "id": "RC9af052ee231346f28d1e44865ab62c04",
          "type": "rule_components"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR986402dc07834fbeb4789c56060dbf41"
        },
        "data": {
          "id": "PR986402dc07834fbeb4789c56060dbf41",
          "type": "properties"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/rules"
        }
      }
    },
    "links": {
      "extension": "https://reactor.adobe.io/extensions/EXcedb08a8265c488e8bb98b46245b2486",
      "origin": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04",
      "rules": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/rules",
      "self": "https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04"
    },
    "meta": {
      "latest_revision_number": 0
    }
  }
}
```

## 刪除規則元件

可以通過將規則元件ID包含在DELETE請求的路徑中來刪除它。

**API格式**

```http
DELETE /rule_components/{RULE_COMPONENT_ID}
```

| 參數 | 說明 |
| --- | --- |
| `RULE_COMPONENT_ID` | 的 `id` 刪除的規則元件。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X DELETE \
  https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}'
```

**回應**

成功的響應返回沒有響應正文的HTTP狀態204（無內容），表示規則元件已被刪除。

## 管理規則元件的注釋 {#notes}

規則元件是「顯著」資源，這意味著您可以為每個資源建立和檢索基於文本的注釋。 查看 [notes endpoint guide（注釋終結點指南）](./notes.md) 的子菜單。

## 檢索規則元件的相關資源 {#related}

以下調用演示了如何檢索規則元件的相關資源。 當 [查找規則元件](#lookup)，這些關係列在 `relationships` 規則元件。

查看 [關係指南](../guides/relationships.md) 的子菜單。

### 列出規則元件的相關規則 {#rules}

可通過附加來列出利用特定規則元件的規則 `/rules` 查找請求的路徑。

**API格式**

```http
GET  /rule_components/{RULE_COMPONENT_ID}/rules
```

| 參數 | 說明 |
| --- | --- |
| `{RULE_COMPONENT_ID}` | 的 `id` 要列出其規則的規則元件。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/rules \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的響應返回使用指定規則元件的規則清單。

```json
{
  "data": [
    {
      "id": "RLf1baa571748941db88f54de8efd119aa",
      "type": "rules",
      "attributes": {
        "created_at": "2020-12-14T17:58:36.072Z",
        "deleted_at": null,
        "dirty": true,
        "enabled": true,
        "name": "Example Rule",
        "published": false,
        "published_at": null,
        "revision_number": 0,
        "updated_at": "2020-12-14T17:58:37.452Z",
        "review_status": "unsubmitted"
      },
      "relationships": {
        "libraries": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/libraries"
          }
        },
        "revisions": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/revisions"
          }
        },
        "notes": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/notes"
          }
        },
        "property": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/property"
          },
          "data": {
            "id": "PR966c4a501e1a43a48cb55e104b4de935",
            "type": "properties"
          }
        },
        "origin": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/origin"
          },
          "data": {
            "id": "RLf1baa571748941db88f54de8efd119aa",
            "type": "rules"
          }
        },
        "rule_components": {
          "links": {
            "related": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/rule_components"
          }
        }
      },
      "links": {
        "property": "https://reactor.adobe.io/properties/PR966c4a501e1a43a48cb55e104b4de935",
        "origin": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa",
        "self": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa",
        "rule_components": "https://reactor.adobe.io/rules/RLf1baa571748941db88f54de8efd119aa/rule_components"
      },
      "meta": {
        "latest_revision_number": 0
      }
    }
  ]
}
```

### 查找規則元件的相關擴展 {#extension}

可通過附加來查找提供規則元件的擴展 `/extension` 查找請求的路徑。

**API格式**

```http
GET /rule_components/{RULE_COMPONENT_ID}/extension
```

| 參數 | 說明 |
| --- | --- |
| `{RULE_COMPONENT_ID}` | 的 `id` 要查找其副檔名的規則元件。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/rule_components/RC9af052ee231346f28d1e44865ab62c04/extension \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的響應返回指定規則元件擴展的詳細資訊。

```json
{
  "data": {
    "id": "EX5644c3eed97d46b39cb2279ea11dde29",
    "type": "extensions",
    "attributes": {
      "created_at": "2020-12-14T17:55:22.634Z",
      "deleted_at": null,
      "dirty": false,
      "enabled": true,
      "name": "kessel-test",
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:55:22.634Z",
      "delegate_descriptor_id": null,
      "display_name": "Kessel Test",
      "review_status": "unsubmitted",
      "version": "1.2.0",
      "settings": "{}"
    },
    "relationships": {
      "libraries": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/libraries"
        }
      },
      "revisions": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/revisions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/notes"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/property"
        },
        "data": {
          "id": "PRcdb3d12504ce48ecbfa4fbbe5b80b6dd",
          "type": "properties"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/origin"
        },
        "data": {
          "id": "EX5644c3eed97d46b39cb2279ea11dde29",
          "type": "extensions"
        }
      },
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29/extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      }
    },
    "links": {
      "property": "https://reactor.adobe.io/properties/PRcdb3d12504ce48ecbfa4fbbe5b80b6dd",
      "origin": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29",
      "self": "https://reactor.adobe.io/extensions/EX5644c3eed97d46b39cb2279ea11dde29",
      "extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a",
      "latest_extension_package": "https://reactor.adobe.io/extension_packages/EP75db2452065b44e2b8a38ca883ce369a"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```

### 查找規則元件的相關原點 {#origin}

可通過附加來查找規則元件的原點（上一版本） `/origin` 查找請求的路徑。

**API格式**

```http
GET /rule_components/{RULE_COMPONENT_ID}/origin
```

| 參數 | 說明 |
| --- | --- |
| `{RULE_COMPONENT_ID}` | 的 `id` 要查找其原點的規則元件。 |

{style="table-layout:auto"}

**要求**

```shell
curl -X GET \
  https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/origin \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -H 'Accept: application/vnd.api+json;revision=1'
```

**回應**

成功的響應返回指定規則元件原點的詳細資訊。

```json
{
  "data": {
    "id": "RC3d0805fde85d42db8988090bc074bb44",
    "type": "rule_components",
    "attributes": {
      "created_at": "2020-12-14T17:55:40.016Z",
      "delegate_descriptor_id": "kessel-test::events::click",
      "deleted_at": null,
      "dirty": false,
      "name": "My Example Click Event",
      "negate": false,
      "order": 0,
      "rule_order": 50.0,
      "timeout": 2000,
      "delay_next": true,
      "published": false,
      "published_at": null,
      "revision_number": 0,
      "updated_at": "2020-12-14T17:55:40.016Z",
      "settings": "{\"elementSelector\":\".accordion\",\"bubbleFireIfChildFired\":true}"
    },
    "relationships": {
      "updated_with_extension_package": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/updated_with_extension_package"
        },
        "data": {
          "id": "EP75db2452065b44e2b8a38ca883ce369a",
          "type": "extension_packages"
        }
      },
      "updated_with_extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/updated_with_extension"
        },
        "data": {
          "id": "EXb713fc209ce344c996bdeb377685e2c4",
          "type": "extensions"
        }
      },
      "extension": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/extension"
        },
        "data": {
          "id": "EXd6e1dce006b2412f874301e24d58ce24",
          "type": "extensions"
        }
      },
      "notes": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/notes"
        }
      },
      "origin": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/origin"
        },
        "data": {
          "id": "RC3d0805fde85d42db8988090bc074bb44",
          "type": "rule_components"
        }
      },
      "property": {
        "links": {
          "related": "https://reactor.adobe.io/properties/PR89c66a560ec44928889b439333255efe"
        },
        "data": {
          "id": "PR89c66a560ec44928889b439333255efe",
          "type": "properties"
        }
      },
      "rules": {
        "links": {
          "related": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/rules"
        }
      }
    },
    "links": {
      "extension": "https://reactor.adobe.io/extensions/EXd6e1dce006b2412f874301e24d58ce24",
      "origin": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44",
      "rules": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44/rules",
      "self": "https://reactor.adobe.io/rule_components/RC3d0805fde85d42db8988090bc074bb44"
    },
    "meta": {
      "latest_revision_number": 1
    }
  }
}
```
