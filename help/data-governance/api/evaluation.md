---
keywords: Experience Platform；首頁；熱門主題；原則執行；自動執行；API型執行；資料控管
solution: Experience Platform
title: 策略評估API端點
description: 建立了行銷操作並定義了策略後，您可以使用策略服務API來評估某些操作是否違反了任何策略。 傳回的限制會採取一組原則的形式，這些原則會因為嘗試對包含資料使用標籤的指定資料執行行銷動作而遭到違反。
exl-id: f9903939-268b-492c-aca7-63200bfe4179
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1542'
ht-degree: 1%

---

# 策略評估終結點

建立行銷動作並定義資料使用原則後，您就可以使用 [!DNL Policy Service] 評估某些動作是否違反任何原則的API。 傳回的限制會採取一組原則的形式，這些原則會因為嘗試對包含資料使用標籤的指定資料執行行銷動作而遭到違反。

預設情況下，僅策略的狀態設定為 `ENABLED` 參與評價。 不過，您可以使用查詢參數 `?includeDraft=true` 包含 `DRAFT` 評估中的政策。

評估請求可通過以下三種方式之一：

1. 如果有行銷動作和一組資料使用量標籤，該動作是否違反任何原則？
1. 如果行銷動作和一或多個資料集，動作是否違反任何原則？
1. 若執行行銷動作、一或多個資料集，以及這些資料集中一或多個欄位的子集，動作是否會違反任何原則？

## 快速入門

本指南中使用的API端點屬於 [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/). 繼續之前，請檢閱 [快速入門手冊](./getting-started.md) 如需相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何呼叫所需的必要標題的重要資訊 [!DNL Experience Platform] API。

## 使用資料使用標籤評估策略違規 {#labels}

您可以根據特定資料使用量標籤集的存在，使用 `duleLabels` 查詢參數。

**API格式**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 針對一組資料使用量標籤測試的行銷動作名稱。 您可以透過 [GET向行銷動作端點提出請求](./marketing-actions.md#list). |
| `{LABELS_LIST}` | 以逗號分隔的資料使用量標籤名稱清單，用以測試行銷動作。 例如： `duleLabels=C1,C2,C3`<br><br>請注意，標籤名稱會區分大小寫。 請確定您在 `duleLabels` 參數。 |

**要求**

以下範例要求會根據標籤C1和C3評估行銷動作。

>[!IMPORTANT]
>
>請注意 `AND` 和 `OR` 運算子。 在下列範例中，如果`C1` 或 `C3`)，行銷動作就不會違反此政策。 會採用兩個標籤(`C1` 和 `C3`)，以傳回違反的原則。 請務必仔細評估策略，並以平等的謹慎定義策略表達式。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應包含 `violatedPolicies` 陣列，包含因對提供的標籤執行行銷動作而違反之原則的詳細資訊。 如果未違反任何原則，則 `violatedPolicies` 陣列將為空。

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

## 使用資料集評估違反策略的情況 {#datasets}

您可以根據一組資料集評估策略違規情況，資料使用標籤可從這些資料集收集。 若要這麼做，請對 `/constraints` 端點，以取得特定行銷動作和在請求內文中提供資料集ID清單。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 針對一或多個資料集測試的行銷動作名稱。 您可以透過 [GET向行銷動作端點提出請求](./marketing-actions.md#list). |

**要求**

下列請求會執行 `crossSiteTargeting` 針對一組三個資料集執行行銷動作，以評估是否有任何違反政策的情況。

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
| `entityType` | 其ID在同層級中指示的實體類型 `entityId` 屬性。 目前，唯一接受的值是 `dataSet`. |
| `entityId` | 用來測試行銷動作的資料集ID。 向提出GET要求，即可取得資料集及其對應ID的清單 `/dataSets` 端點 [!DNL Catalog Service] API。 請參閱 [清單 [!DNL Catalog] 物件](../../catalog/api/list-objects.md) 以取得更多資訊。 |

**回應**

成功的回應包含 `violatedPolicies` 陣列，其中包含對提供的資料集執行行銷動作後所違反之原則的詳細資訊。 如果未違反任何原則，則 `violatedPolicies` 陣列將為空。

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
| `duleLabels` | 回應物件包含 `duleLabels` 陣列，包含在指定資料集中找到的所有標籤的統一清單。 此清單包含資料集內所有欄位的資料集和欄位層級標籤。 |
| `discoveredLabels` | 回應也包含 `discoveredLabels` 陣列，包含每個資料集的物件，顯示 `datasetLabels` 劃分為資料集和欄位層級標籤。 每個欄位層級標籤都顯示含有該標籤之特定欄位的路徑。 |

## 使用特定資料集欄位評估違反策略的情況 {#fields}

您可以根據一個或多個資料集中的欄位子集評估策略違規情況，以便僅評估應用了這些欄位的資料使用標籤。

使用資料集欄位評估策略時，請記住以下事項：

* **欄位名稱區分大小寫**:提供欄位時，必須如實寫入資料集中的欄位(例如 `firstName` vs `firstname`)。
* **資料集標籤繼承**:資料集中的個別欄位會繼承在資料集層級套用的任何標籤。 如果您的策略評估未如預期返回，請務必檢查除了欄位層級套用的標籤之外，還是從資料集層級繼承到欄位的標籤。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 針對資料集欄位子集進行測試的行銷動作名稱。 您可以透過 [GET向行銷動作端點提出請求](./marketing-actions.md#list). |

**要求**

下列請求會測試行銷動作 `crossSiteTargeting` 在屬於三個資料集的特定欄位集上。 裝載類似於 [僅限資料集的評估請求](#datasets)，新增每個資料集的特定欄位以從中收集標籤。

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
| `entityType` | 其ID在同層級中指示的實體類型 `entityId` 屬性。 目前，唯一接受的值是 `dataSet`. |
| `entityId` | 要根據行銷動作評估其欄位的資料集ID。 向提出GET要求，即可取得資料集及其對應ID的清單 `/dataSets` 端點 [!DNL Catalog Service] API。 請參閱 [清單 [!DNL Catalog] 物件](../../catalog/api/list-objects.md) 以取得更多資訊。 |
| `entityMeta.fields` | 資料集結構內特定欄位的路徑陣列，以JSON指標字串形式提供。 請參閱 [JSON指標](../../landing/api-fundamentals.md#json-pointer) （位於API基礎指南中），以取得這些字串接受語法的詳細資訊。 |

**回應**

成功的回應包含 `violatedPolicies` 陣列，包含因對提供的資料集欄位執行行銷動作而違反之原則的詳細資訊。 如果未違反任何原則，則 `violatedPolicies` 陣列將為空。

將以下範例回應與 [僅資料集的回應](#datasets)，請注意收集的標籤清單較短。 此 `discoveredLabels` 每個資料集的欄位也已減少，因為這些欄位僅包含要求內文中指定的欄位。 此外，之前違反的政策 `Targeting Ads or Content` 兩者兼有 `C4 AND C6` 標籤呈現，因此不再違反空白的 `violatedPolicies` 陣列。

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

## 大量評估策略 {#bulk}

此 `/bulk-eval` 端點可讓您在單一API呼叫中執行多個評估作業。

**API格式**

```http
POST /bulk-eval
```

**要求**

大量評估請求的裝載應為一個物件陣列；每個要執行的評估作業各一個。 針對根據資料集和欄位評估的作業， `entityList` 必須提供陣列。 對於根據資料使用量標籤評估的作業， `labels` 必須提供陣列。

>[!WARNING]
>
>如果列出的任何評估作業都包含 `entityList` 和 `labels` 陣列，則會產生錯誤。 如果您想要根據資料集和標籤評估相同的行銷動作，則必須為該行銷動作包含個別的評估工作。

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
| `evalRef` | 針對違反原則的標籤或資料集測試的行銷動作URI。 |
| `includeDraft` | 預設情況下，只有啟用的策略才參與評估。 若 `includeDraft` 設為 `true`，中的原則 `DRAFT` 狀態也會參與。 |
| `labels` | 用來測試行銷動作的資料使用標籤陣列。<br><br>**重要**:使用此屬性時， `entityList` 屬性不得包含在相同物件中。 若要使用資料集和/或欄位評估相同的行銷動作，您必須在包含 `entityList` 陣列。 |
| `entityList` | 這些資料集中的資料集陣列和（選擇性）特定欄位，以測試行銷動作。<br><br>**重要**:使用此屬性時， `labels` 屬性不得包含在相同物件中。 若要使用特定資料使用方式標籤來評估相同的行銷動作，您必須在包含的請求裝載中包含個別物件 `labels` 陣列。 |
| `entityType` | 要測試行銷動作的實體類型。 目前，僅 `dataSet` 支援。 |
| `entityId` | 用來測試行銷動作的資料集ID。 |
| `entityMeta.fields` | （選用）資料集內用來測試行銷動作的特定欄位清單。 |

**回應**

成功的響應返回一系列評估結果；請求中發送的每個策略評估作業各一個。

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

## 策略評估 [!DNL Real-Time Customer Profile]

此 [!DNL Policy Service] API也可用來檢查是否有違反使用 [!DNL Real-Time Customer Profile] 區段。 請參閱 [強制遵循對象區段的資料使用方式](../../segmentation/tutorials/governance.md) 以取得更多資訊。
