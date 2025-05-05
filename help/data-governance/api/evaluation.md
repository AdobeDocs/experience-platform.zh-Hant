---
keywords: Experience Platform；首頁；熱門主題；原則執行；自動執行；API型執行；資料控管
solution: Experience Platform
title: 原則評估API端點
description: 建立行銷動作並定義原則後，您就可以使用原則服務API來評估某些動作是否違反了原則。 傳回的限制會採取一組原則的形式，這些原則會在嘗試對包含資料使用標籤的指定資料執行行銷動作時遭到違反。
role: Developer
exl-id: f9903939-268b-492c-aca7-63200bfe4179
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '1538'
ht-degree: 1%

---

# 原則評估端點

建立行銷動作並定義資料使用原則後，您就可以使用[!DNL Policy Service] API來評估某些動作是否違反任何原則。 傳回的限制會採取一組原則的形式，這些原則會在嘗試對包含資料使用標籤的指定資料執行行銷動作時遭到違反。

依預設，只有狀態設定為`ENABLED`的原則才會參與評估。 不過，您可以使用查詢引數`?includeDraft=true`在評估中包含`DRAFT`原則。

您可以透過下列三種方式之一提出評估請求：

1. 指定行銷動作和一組資料使用標籤，該動作是否違反任何原則？
1. 指定行銷動作和一個或多個資料集，該動作是否違反任何政策？
1. 指定行銷動作、一個或多個資料集，以及這些資料集中一個或多個欄位的子集，該動作是否違反任何政策？

## 快速入門

本指南中使用的API端點是[[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/)的一部分。 繼續之前，請先檢閱[快速入門手冊](./getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的手冊，以及有關成功呼叫任何[!DNL Experience Platform] API所需必要標題的重要資訊。

## 使用資料使用標籤評估原則違規 {#labels}

您可以使用GET要求中的`duleLabels`查詢引數，根據特定資料使用標籤集是否存在，評估原則違規。

**API格式**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 針對一組資料使用標籤進行測試的行銷動作名稱。 您可以向行銷動作端點[&#128279;](./marketing-actions.md#list)發出GET要求，以擷取可用的行銷動作清單。 |
| `{LABELS_LIST}` | 以逗號分隔的資料使用標簽名稱清單，用於測試行銷動作。 例如： `duleLabels=C1,C2,C3`<br><br>請注意，標簽名稱區分大小寫。 在`duleLabels`引數中列出這些專案時，請確定您使用正確的大小寫。 |

**要求**

以下範例請求會針對標籤C1和C3評估行銷動作。

>[!IMPORTANT]
>
>請注意原則運算式中的`AND`和`OR`運運算元。 在以下範例中，如果標籤（`C1`或`C3`）單獨出現在請求中，行銷動作將不會違反此原則。 需要兩個標籤（`C1`和`C3`）才能傳回違反的原則。 請務必謹慎評估原則，並謹慎定義原則運算式。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應包括`violatedPolicies`陣列，其中包含對提供的標籤執行行銷動作所違反原則的詳細資料。 如果未違反任何原則，`violatedPolicies`陣列將是空的。

```JSON
{
    "timestamp": 1551134846737,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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

## 使用資料集評估原則違規 {#datasets}

您可以根據一組可以從中收集資料使用標籤的一個或多個資料集來評估原則違規。 若要這麼做，請針對特定行銷動作對`/constraints`端點執行POST要求，並在要求內文中提供資料集ID清單。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 針對一或多個資料集進行測試的行銷動作名稱。 您可以向行銷動作端點[&#128279;](./marketing-actions.md#list)發出GET要求，以擷取可用的行銷動作清單。 |

**要求**

下列要求會針對一組三個資料集執行`crossSiteTargeting`行銷動作，以評估任何原則違規。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `entityType` | 其識別碼在同層級`entityId`屬性中指示的實體型別。 目前唯一接受的值為`dataSet`。 |
| `entityId` | 用來測試行銷動作的資料集ID。 藉由向[!DNL Catalog Service] API中的`/dataSets`端點發出GET要求，即可取得資料集清單及其對應的ID。 如需詳細資訊，請參閱[清單 [!DNL Catalog] 物件](../../catalog/api/list-objects.md)的指南。 |

**回應**

成功的回應包括`violatedPolicies`陣列，其中包含對提供的資料集執行行銷動作所違反原則的詳細資料。 如果未違反任何原則，`violatedPolicies`陣列將是空的。

```JSON
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
| `duleLabels` | 回應物件包含`duleLabels`陣列，其中包含指定資料集中找到的所有標籤的整合清單。 此清單包含資料集內所有欄位上的資料集和欄位層級標籤。 |
| `discoveredLabels` | 回應也包含包含每個資料集物件的`discoveredLabels`陣列，其中顯示`datasetLabels`已細分為資料集和欄位層級標籤。 每個欄位層級標籤會顯示具有該標籤之特定欄位的路徑。 |

## 使用特定資料集欄位評估原則違規 {#fields}

您可以根據一或多個資料集中的欄位子集來評估原則違規，以便只評估套用這些欄位的資料使用標籤。

使用資料集欄位評估原則時，請記住下列事項：

* **欄位名稱區分大小寫**：提供欄位時，必須依照資料集中顯示的樣式來撰寫（例如，`firstName`與`firstname`）。
* **資料集標籤繼承**：資料集中的個別欄位會繼承已在資料集層級套用的任何標籤。 如果原則評估未如預期傳回，除了在欄位層級套用的標籤之外，請務必檢查是否從資料集層級向下繼承到欄位的任何標籤。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 針對資料集欄位子集進行測試的行銷動作名稱。 您可以向行銷動作端點[&#128279;](./marketing-actions.md#list)發出GET要求，以擷取可用的行銷動作清單。 |

**要求**

下列要求會對屬於三個資料集的特定欄位集測試行銷動作`crossSiteTargeting`。 承載類似於僅涉及資料集[&#128279;](#datasets)的評估請求，為要從中收集標籤的每個資料集新增特定欄位。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/crossSiteTargeting/constraints \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `entityType` | 其識別碼在同層級`entityId`屬性中指示的實體型別。 目前唯一接受的值為`dataSet`。 |
| `entityId` | 資料集的ID，其欄位將根據行銷動作進行評估。 藉由向[!DNL Catalog Service] API中的`/dataSets`端點發出GET要求，即可取得資料集清單及其對應的ID。 如需詳細資訊，請參閱[清單 [!DNL Catalog] 物件](../../catalog/api/list-objects.md)的指南。 |
| `entityMeta.fields` | 資料集結構描述中特定欄位的路徑陣列，以JSON指標字串形式提供。 請參閱API基本指南中[JSON指標](../../landing/api-fundamentals.md#json-pointer)的相關小節，以取得這些字串所接受語法的詳細資訊。 |

**回應**

成功的回應包含`violatedPolicies`陣列，其中包含對提供的資料集欄位執行行銷動作時所違反原則的詳細資料。 如果未違反任何原則，`violatedPolicies`陣列將是空的。

將下列範例回應與僅涉及資料集[&#128279;](#datasets)的回應進行比較，請注意，收集的標籤清單較短。 每個資料集的`discoveredLabels`也已減少，因為它們僅包含在要求內文中指定的欄位。 此外，先前違反的原則`Targeting Ads or Content`需要同時存在`C4 AND C6`個標籤，因此不再違反空的`violatedPolicies`陣列所指示的原則。

```JSON
{
    "timestamp": 1556325503038,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
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

## 大量評估原則 {#bulk}

`/bulk-eval`端點可讓您在單一API呼叫中執行多個評估工作。

**API格式**

```http
POST /bulk-eval
```

**要求**

大量評估請求的裝載應為物件陣列；每個要執行的評估工作各一個。 對於根據資料集和欄位進行評估的工作，必須提供`entityList`陣列。 針對根據資料使用標籤進行評估的工作，必須提供`labels`陣列。

>[!WARNING]
>
>如果任何列出的評估工作同時包含`entityList`和`labels`陣列，將會產生錯誤。 如果您想要根據資料集和標籤評估相同的行銷動作，則必須為該行銷動作包含個別評估工作。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/bulk-eval \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
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
| `evalRef` | 用於根據標籤或資料集測試原則違規的行銷動作URI。 |
| `includeDraft` | 依預設，只有啟用的原則會參與評估。 如果`includeDraft`設定為`true`，則處於`DRAFT`狀態的原則也會參與。 |
| `labels` | 用於測試行銷動作的一系列資料使用標籤。<br><br>**重要**：使用此屬性時，`entityList`屬性不可包含在相同物件中。 若要使用資料集和/或欄位評估相同的行銷動作，您必須在包含`entityList`陣列的請求裝載中包含個別的物件。 |
| `entityList` | 資料集陣列，以及這些資料集內用於測試行銷動作的特定欄位（選擇性）。<br><br>**重要**：使用此屬性時，`labels`屬性不可包含在相同物件中。 若要使用特定資料使用標籤來評估相同的行銷動作，您必須在包含`labels`陣列的請求裝載中包含個別物件。 |
| `entityType` | 測試行銷動作的實體型別。 目前僅支援`dataSet`。 |
| `entityId` | 用來測試行銷動作的資料集ID。 |
| `entityMeta.fields` | （選用）資料集中要用來測試行銷動作的特定欄位清單。 |

**回應**

成功的回應會傳回評估結果的陣列；請求中傳送的每個原則評估工作各一個。

```json
[
  {
    "status": 200,
    "body": {
      "timestamp": 1595866566165,
      "clientId": "{CLIENT_ID}",
      "userId": "{USER_ID}",
      "imsOrg": "{ORG_ID}",
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
      "imsOrg": "{ORG_ID}",
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
          "imsOrg": "{ORG_ID}",
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

## [!DNL Real-Time Customer Profile]的原則評估

[!DNL Policy Service] API也可用來檢查涉及使用[!DNL Real-Time Customer Profile]區段的原則違規。 如需詳細資訊，請參閱有關[強制對象區段](../../segmentation/tutorials/governance.md)遵守資料使用規範的教學課程。
