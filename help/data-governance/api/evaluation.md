---
keywords: Experience Platform;home；熱門主題；策略實施；自動實施；基於API的實施；資料治理
solution: Experience Platform
title: 策略評估API端點
topic-legacy: developer guide
description: 建立行銷動作並定義原則後，您就可以使用「原則服務API」來評估是否有某些動作違反了任何原則。 傳回的限制採用一組原則的形式，這些原則會因嘗試對包含資料使用標籤的指定資料執行行銷動作而遭到違反。
exl-id: f9903939-268b-492c-aca7-63200bfe4179
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 1%

---

# 策略評估端點

建立行銷動作並定義原則後，您可以使用[!DNL Policy Service] API來評估某些動作是否違反任何原則。 傳回的限制採用一組原則的形式，這些原則會因嘗試對包含資料使用標籤的指定資料執行行銷動作而遭到違反。

預設情況下，只有狀態設定為`ENABLED`的策略才參與評估。 不過，您可以使用查詢參數`?includeDraft=true`在評估中包含`DRAFT`策略。

評量要求可透過下列三種方式之一提出：

1. 若有行銷動作和一組資料使用標籤，此動作是否違反任何原則？
1. 如果有行銷動作和一或多個資料集，此動作會違反任何原則嗎？
1. 如果有行銷動作、一或多個資料集，以及每個資料集中一或多個欄位的子集，此動作會違反任何原則嗎？

## 快速入門

本指南中使用的API端點是[[!DNL Policy Service] API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)的一部分。 在繼續之前，請先閱讀[快速入門手冊](./getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何[!DNL Experience Platform] API所需之必要標題的重要資訊。

## 使用資料使用標籤{#labels}評估違反原則的情況

您可以使用GET請求中的`duleLabels`查詢參數，根據特定資料使用標籤集的存在來評估策略違規。

**API格式**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 要針對一組資料使用標籤進行測試的行銷動作名稱。 您可以透過向行銷動作端點[提出](./marketing-actions.md#list)的GET請求，擷取可用行銷動作的清單。 |
| `{LABELS_LIST}` | 以逗號分隔的資料使用標籤名稱清單，以測試其行銷動作。 例如：`duleLabels=C1,C2,C3`<br><br>請注意，標籤名稱區分大小寫。 在`duleLabels`參數中列出這些參數時，請務必使用正確的大小寫。 |

**要求**

以下的範例請求會評估標籤C1和C3的行銷動作。

>[!IMPORTANT]
>
>請注意策略表達式中的`AND`和`OR`運算子。 在下列範例中，如果請求中單獨出現標籤（`C1`或`C3`），行銷動作將不會違反此政策。 需要標籤（`C1`和`C3`）才能返回違反的策略。 請確定您正在仔細評估政策，並同時定義政策陳述式。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應包括`violatedPolicies`陣列，該陣列包含因對提供的標籤執行市場營銷操作而違反的策略的詳細資訊。 如果未違反任何策略，則`violatedPolicies`陣列將為空。

```JSON
{
    "timestamp": 1551134846737,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io/marketingActions/custom/sampleMarketingAction",
    "duleLabels": [
        "C1",
        "C3"
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction"
            ],
            "description": "NEW content for description.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "OR",
                        "operands": [
                            {
                                "label": "C3"
                            },
                            {
                                "label": "C7"
                            }
                        ]
                    }
                ]
            },
            "imsOrg": "{IMS_ORG}",
            "created": 1550703519823,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1550714340335,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io/data/foundation/dulepolicy/policies/custom/5c6ddb9f5c404513dc2dc454"
                }
            },
            "id": "5c6ddb9f5c404513dc2dc454"
        }
    ]
}
```

## 使用資料集{#datasets}評估策略違規情況

您可以根據一組或多組資料集評估是否違反原則，這些資料集可從中收集資料使用標籤。 這是透過對特定行銷動作的`/constraints`端點執行POST要求，並在請求主體內提供資料集ID清單來完成。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 針對一或多個資料集進行測試的行銷動作名稱。 您可以透過向行銷動作端點[提出](./marketing-actions.md#list)的GET請求，擷取可用行銷動作的清單。 |

**要求**

以下請求對一組三個資料集執行`crossSiteTargeting`行銷操作，以評估是否有任何策略違規。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319"
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e"
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f"
        }
      ]'
```

| 屬性 | 說明 |
| --- | --- |
| `entityType` | 其ID在同級`entityId`屬性中指示的實體類型。 目前，唯一接受的值是`dataSet`。 |
| `entityId` | 測試行銷動作的資料集ID。 通過向[!DNL Catalog Service] API中的`/dataSets`端點發出GET請求，可以獲取資料集清單及其相應的ID。 如需詳細資訊，請參閱[清單 [!DNL Catalog] 物件](../../catalog/api/list-objects.md)上的指南。 |

**回應**

成功的響應包括`violatedPolicies`陣列，該陣列包含因對提供的資料集執行市場營銷操作而違反的策略的詳細資訊。 如果未違反任何策略，則`violatedPolicies`陣列將為空。

```JSON
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting",
    "duleLabels": [
        "C1",
        "C2",
        "C4",
        "C5",
        "C6"
    ],
    "discoveredLabels": [
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C6"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C4",
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    },
                    {
                        "labels": [
                            "C4"
                        ],
                        "path": "/properties/identityMap"
                    },
                    {
                        "labels": [
                            "C4"
                        ],
                        "path": "/properties/journeyAI"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/createdByBatchID"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    },
                    {
                        "labels": [
                            "C1"
                        ],
                        "path": "/properties/identityMap"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/createdByBatchID"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        }
    ],
    "violatedPolicies": [
        {
            "name": "Targeting Ads or Content",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting"
            ],
            "description": "Data cannot be used for targeting any ads or content, either on-site or cross-site.",
            "deny": {
                "operator": "AND",
                "operands": [
                    {
                        "label": "C4"
                    },
                    {
                        "label": "C6"
                    }
                ]
            },
            "imsOrg": "{IMS_ORG}",
            "created": 1551141210463,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER}",
            "updated": 1551146178603,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/policies/custom/5c74895a74744d13dc2d87cc"
                }
            },
            "id": "5c74895a74744d13dc2d87cc"
        }
    ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `duleLabels` | 響應對象包括`duleLabels`陣列，該陣列包含在指定資料集內找到的所有標籤的統一清單。 此清單包含資料集內所有欄位的資料集和欄位層級標籤。 |
| `discoveredLabels` | 此回應也包含`discoveredLabels`陣列，其中包含每個資料集的物件，其中顯示細分為資料集和欄位層級標籤的`datasetLabels`。 每個欄位層級標籤都會顯示含有該標籤之特定欄位的路徑。 |

## 使用特定資料集欄位{#fields}評估違反原則的情況

您可以根據一個或多個資料集內的欄位子集評估策略違規情況，以便僅評估應用了這些欄位的資料使用標籤。

使用資料集欄位評估原則時，請牢記下列事項：

* **欄位名稱區分大小寫**:提供欄位時，必須正確寫入欄位，如資料集中的欄位( `firstName` vs `firstname`)。
* **資料集標籤繼承**:資料集中的個別欄位會繼承在資料集層級套用的任何標籤。如果您的原則評估未如預期般傳回，請務必檢查除了欄位層級套用的標籤外，資料集層級下層可能繼承到欄位的標籤。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 要針對資料集欄位子集進行測試的行銷動作名稱。 您可以透過向行銷動作端點[提出](./marketing-actions.md#list)的GET請求，擷取可用行銷動作的清單。 |

**要求**

下列請求會測試屬於三個資料集的特定欄位集上的行銷動作`crossSiteTargeting`。 裝載類似於僅涉及資料集](#datasets)的[評估請求，為每個資料集添加特定欄位以收集標籤。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "entityMeta": {
                "fields": [
                    "/properties/_customer",
                    "/properties/faxPhone"
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "entityMeta": {
                "fields": [
                    "/properties/_customer",
                    "/properties/geoUnit"
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "entityMeta": {
                "fields": [
                    "/properties/faxPhone"
                ]
            }
        }
      ]'
```

| 屬性 | 說明 |
| --- | --- |
| `entityType` | 其ID在同級`entityId`屬性中指示的實體類型。 目前，唯一接受的值是`dataSet`。 |
| `entityId` | 要根據行銷動作評估其欄位的資料集ID。 通過向[!DNL Catalog Service] API中的`/dataSets`端點發出GET請求，可以獲取資料集清單及其相應的ID。 如需詳細資訊，請參閱[清單 [!DNL Catalog] 物件](../../catalog/api/list-objects.md)上的指南。 |
| `entityMeta.fields` | 資料集結構中特定欄位的路徑陣列，以JSON指針字串的形式提供。 如需這些字串所接受語法的詳細資訊，請參閱API基礎指南中[JSON指針](../../landing/api-fundamentals.md#json-pointer)一節。 |

**回應**

成功的響應包括`violatedPolicies`陣列，該陣列包含對提供的資料集欄位執行行銷操作時所違反的策略的詳細資訊。 如果未違反任何策略，則`violatedPolicies`陣列將為空。

將下面的示例響應與僅涉及資料集](#datasets)的[響應進行比較，請注意收集的標籤清單較短。 每個資料集的`discoveredLabels`也已減少，因為它們只包含請求主體中指定的欄位。 此外，先前違反的策略`Targeting Ads or Content`要求同時顯示`C4 AND C6`標籤，因此不再違反空`violatedPolicies`陣列。

```JSON
{
    "timestamp": 1556325503038,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting",
    "duleLabels": [
        "C2",
        "C5",
        "C6"
    ],
    "discoveredLabels": [
        {
            "entityType": "dataSet",
            "entityId": "5c423dc25f2f2e00005e2319",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C6"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc323e15410ef14b749481e",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C2",
                            "C5"
                        ],
                        "path": "/properties/_customer"
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/geoUnit"
                    }
                ]
            }
        },
        {
            "entityType": "dataSet",
            "entityId": "5cc1fb685410ef14b748c55f",
            "dataSetLabels": {
                "connection": {
                    "labels": []
                },
                "dataSet": {
                    "labels": [
                        "C5"
                    ]
                },
                "fields": [
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/faxPhone"
                    }
                ]
            }
        }
    ],
    "violatedPolicies": []
}
```

## 大量評估策略{#bulk}

`/bulk-eval`端點可讓您在單一API呼叫中執行多個評估工作。

**API格式**

```http
POST /bulk-eval
```

**要求**

批量評估請求的有效載荷應是一組對象；每個評估作業各執行一個。 對於基於資料集和欄位進行評估的作業，必須提供`entityList`陣列。 對於根據資料使用標籤評估的作業，必須提供`labels`陣列。

>[!WARNING]
>
>如果列出的任何評估作業同時包含`entityList`和`labels`陣列，則會導致錯誤。 如果您想要根據資料集和標籤來評估相同的行銷動作，則必須針對該行銷動作包含個別的評估工作。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/bulk-eval \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '[
        {
          "evalRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting/constraints",
          "includeDraft": false,
          "labels": [
            "C1",
            "C2",
            "C3"
          ]
        },
        {
          "evalRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting/constraints",
          "includeDraft": false,
          "entityList": [
            {
              "entityType": "dataSet",
              "entityId": "5b67f4dd9f6e710000ea9da4",
              "entityMeta": {
                "fields": [
                  "address"
                ]
              }
            }
          ]
        }
      ]'
```

| 屬性 | 說明 |
| --- | --- |
| `evalRef` | 針對違反原則的標籤或資料集測試行銷動作的URI。 |
| `includeDraft` | 預設情況下，只有啟用的策略參與評估。 如果`includeDraft`設定為`true`，則處於`DRAFT`狀態的策略也將參與。 |
| `labels` | 一系列資料使用標籤，用以測試行銷動作。<br><br>**重要**:使用此屬性時， `entityList` 不能將屬性包含在同一對象中。若要使用資料集和／或欄位評估相同的行銷動作，您必須在包含`entityList`陣列的請求裝載中包含個別物件。 |
| `entityList` | 這些資料集內的資料集陣列和（可選）特定欄位，以測試行銷動作。<br><br>**重要**:使用此屬性時， `labels` 不能將屬性包含在同一對象中。若要使用特定資料使用標籤來評估相同的行銷動作，您必須在包含`labels`陣列的請求裝載中包含個別物件。 |
| `entityType` | 要測試其行銷動作的實體類型。 目前僅支援`dataSet`。 |
| `entityId` | 測試行銷動作的資料集ID。 |
| `entityMeta.fields` | （選用）資料集內用來測試行銷動作的特定欄位清單。 |

**回應**

成功的回應會傳回一系列評估結果；每個策略評估作業在請求中發送一個。

```json
[
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{IMS_ORG}",
      "sandboxName": "prod",
      "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting",
      "duleLabels": [
        "C1",
        "C2",
        "C3"
      ],
      "violatedPolicies": []
    }
  },
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{IMS_ORG}",
      "sandboxName": "prod",
      "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting",
      "duleLabels": [
        "C1",
        "C2"
      ],
      "discoveredLabels": [
        {
          "entityType": "dataset",
          "entityId": "5b67f4dd9f6e710000ea9da4",
          "dataSetLabels": {
            "connection": {
              "labels": [

              ]
            },
            "dataset": {
              "labels": [
                "C1",
                "C2"
              ]
            },
            "fields": []
          }
        }
      ],
      "violatedPolicies": [
        {
          "name": "Email Policy",
          "status": "DRAFT",
          "marketingActionRefs": [
            "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/core/emailTargeting"
          ],
          "description": "Conditions under which we won't send marketing-based email",
          "deny": {
            "label": "C1",
            "operator": "AND",
            "operands": [
              {
                "label": "C1"
              },
              {
                "label": "C3"
              }
            ]
          },
          "id": "76131228-7654-11e8-adc0-fa7ae01bbebc",
          "imsOrg": "{IMS_ORG}",
          "created": 1529696681413,
          "createdClient": "{CLIENT_ID}",
          "createdUser": "{USER_ID}",
          "updated": 1529697651972,
          "updatedClient": "{CLIENT_ID}",
          "updatedUser": "{USER_ID}",
          "_links": {
            "self": {
              "href": "./76131228-7654-11e8-adc0-fa7ae01bbebc"
            }
          }
        }
      ]
    }
  }
]
```

## [!DNL Real-time Customer Profile]的策略評估

[!DNL Policy Service] API也可用於檢查與使用[!DNL Real-time Customer Profile]區段有關的違反原則的情況。 如需詳細資訊，請參閱[教學課程，強化觀眾區段的資料使用合規性。](../../segmentation/tutorials/governance.md)
