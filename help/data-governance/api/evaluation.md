---
keywords: Experience Platform；首頁；熱門主題；策略實施；自動實施；基於API的實施；資料治理
solution: Experience Platform
title: 策略評估API終結點
description: 建立市場營銷操作並定義策略後，您可以使用策略服務API評估某些操作是否違反了任何策略。 返回的約束採用一組策略的形式，這些策略將通過嘗試對包含資料使用標籤的指定資料執行市場營銷操作而受到違反。
exl-id: f9903939-268b-492c-aca7-63200bfe4179
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1542'
ht-degree: 1%

---

# 策略評估終結點

建立市場營銷操作並定義資料使用策略後，您可以使用 [!DNL Policy Service] 評估某些操作是否違反任何策略的API。 返回的約束採用一組策略的形式，這些策略將通過嘗試對包含資料使用標籤的指定資料執行市場營銷操作而受到違反。

預設情況下，只有狀態設定為 `ENABLED` 參與評估。 但是，可以使用查詢參數 `?includeDraft=true` 包括 `DRAFT` 策略。

評估請求可以通過以下三種方式之一進行：

1. 給定市場營銷操作和一組資料使用標籤，該操作是否違反任何策略？
1. 如果有市場營銷操作和一個或多個資料集，該操作是否違反任何策略？
1. 如果給定市場營銷操作、一個或多個資料集以及每個資料集中一個或多個欄位的子集，該操作是否違反任何策略？

## 快速入門

本指南中使用的API端點是 [[!DNL Policy Service] API](https://www.adobe.io/experience-platform-apis/references/policy-service/)。 在繼續之前，請查看 [入門指南](./getting-started.md) 有關指向相關文檔的連結、閱讀本文檔中示例API調用的指南，以及成功調用任何文檔所需的標題的重要資訊 [!DNL Experience Platform] API。

## 使用資料使用標籤評估策略違規 {#labels}

您可以使用 `duleLabels` 查詢參數。

**API格式**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABELS_LIST}
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 要針對一組資料用法標籤test的市場營銷操作的名稱。 通過建立 [GET對市場營銷操作終結點的請求](./marketing-actions.md#list)。 |
| `{LABELS_LIST}` | 以逗號分隔的資料使用標籤名稱清單，用於test市場營銷操作。 例如： `duleLabels=C1,C2,C3`<br><br>請注意，標籤名稱區分大小寫。 確保在中列出時使用正確的案例 `duleLabels` 的下界。 |

**要求**

下面的示例請求針對標籤C1和C3評估市場營銷操作。

>[!IMPORTANT]
>
>注意 `AND` 和 `OR` 策略表達式中的運算子。 在下面的示例中，如果`C1` 或 `C3`)在請求中單獨出現，營銷操作不會違反此策略。 它需要兩個標籤(`C1` 和 `C3`)以返回違反的策略。 確保您仔細評估策略，並同等謹慎地定義策略表達式。

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功響應包括 `violatedPolicies` 陣列，其中包含因對提供的標籤執行市場營銷操作而違反的策略的詳細資訊。 如果未違反策略， `violatedPolicies` 陣列將為空。

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

## 使用資料集評估策略違規 {#datasets}

您可以基於一組一個或多個資料集評估策略違規情況，從這些資料集可以收集資料使用標籤。 這是通過對執行POST請求 `/constraints` 用於特定市場營銷操作的端點，並在請求正文中提供資料集ID的清單。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 針對一個或多個資料集進行test的市場營銷操作的名稱。 通過建立 [GET對市場營銷操作終結點的請求](./marketing-actions.md#list)。 |

**要求**

以下請求執行 `crossSiteTargeting` 針對三個資料集的市場營銷操作，以評估是否存在任何策略違規。

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
| `entityType` | 其ID在同級中指示的實體類型 `entityId` 屬性。 當前，唯一接受的值是 `dataSet`。 |
| `entityId` | 要test市場營銷操作的資料集的ID。 通過向該資料庫發出GET請求，可以獲得資料集清單及其相應ID `/dataSets` 端點 [!DNL Catalog Service] API。 請參閱上的指南 [上市 [!DNL Catalog] 對象](../../catalog/api/list-objects.md) 的子菜單。 |

**回應**

成功響應包括 `violatedPolicies` 陣列，其中包含由於對提供的資料集執行市場營銷操作而違反的策略的詳細資訊。 如果未違反策略， `violatedPolicies` 陣列將為空。

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
| `duleLabels` | 響應對象包括 `duleLabels` 包含指定資料集中找到的所有標籤的統一清單的陣列。 此清單包括資料集內所有欄位上的資料集和欄位級別標籤。 |
| `discoveredLabels` | 響應還包括 `discoveredLabels` 陣列包含每個資料集的對象，顯示 `datasetLabels` 細分為資料集和欄位級標籤。 每個欄位級標籤都顯示帶有該標籤的特定欄位的路徑。 |

## 使用特定資料集欄位評估策略違規 {#fields}

您可以根據一個或多個資料集內的欄位子集評估策略違規情況，以便只評估應用了這些欄位的資料使用標籤。

使用資料集欄位評估策略時，請牢記以下事項：

* **欄位名區分大小寫**:提供欄位時，必須與資料集中顯示的欄位完全相同(例如， `firstName` 與 `firstname`)。
* **資料集標籤繼承**:資料集中的各個欄位繼承在資料集級別應用的所有標籤。 如果策略評估未按預期返回，請確保除了在欄位級別應用的標籤外，檢查從資料集級別繼承到欄位的任何標籤。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 針對資料集欄位子集進行test的市場營銷操作的名稱。 通過建立 [GET對市場營銷操作終結點的請求](./marketing-actions.md#list)。 |

**要求**

以下請求test市場營銷活動 `crossSiteTargeting` 屬於三個資料集的特定欄位集。 負載類似於 [評估請求僅涉及資料集](#datasets)，為每個資料集添加特定欄位以從中收集標籤。

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
| `entityType` | 其ID在同級中指示的實體類型 `entityId` 屬性。 當前，唯一接受的值是 `dataSet`。 |
| `entityId` | 要根據市場營銷操作評估其欄位的資料集的ID。 通過向該資料庫發出GET請求，可以獲得資料集清單及其相應ID `/dataSets` 端點 [!DNL Catalog Service] API。 請參閱上的指南 [上市 [!DNL Catalog] 對象](../../catalog/api/list-objects.md) 的子菜單。 |
| `entityMeta.fields` | 以JSON指針字串形式提供的資料集架構中特定欄位的路徑陣列。 請參閱 [JSON指針](../../landing/api-fundamentals.md#json-pointer) API基礎知識指南中，瞭解有關這些字串的接受語法的詳細資訊。 |

**回應**

成功響應包括 `violatedPolicies` 陣列，其中包含由於對提供的資料集欄位執行市場營銷操作而違反的策略的詳細資訊。 如果未違反策略， `violatedPolicies` 陣列將為空。

將下面的示例響應與 [僅涉及資料集的響應](#datasets)，請注意收集的標籤清單較短。 的 `discoveredLabels` 對於每個資料集也已縮減，因為它們只包括請求正文中指定的欄位。 此外，以前違反的策略 `Targeting Ads or Content` 要求 `C4 AND C6` 將顯示的標籤，因此不再違反空 `violatedPolicies` 陣列。

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

## 批量評估策略 {#bulk}

的 `/bulk-eval` 終結點允許您在單個API調用中運行多個評估作業。

**API格式**

```http
POST /bulk-eval
```

**要求**

批量評估請求的負載應為對象陣列；每個要執行的評估作業各執行一個。 對於基於資料集和欄位進行評估的作業， `entityList` 必須提供陣列。 對於基於資料使用標籤評估的作業， `labels` 必須提供陣列。

>[!WARNING]
>
>如果任何列出的評估作業都包含 `entityList` 和 `labels` 陣列，將導致錯誤。 如果要根據資料集和標籤對同一市場營銷活動進行評估，則必須為該市場營銷活動包括單獨的評估作業。

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
| `evalRef` | 針對標籤或資料集test策略違規的市場營銷操作的URI。 |
| `includeDraft` | 預設情況下，只有啟用的策略參與評估。 如果 `includeDraft` 設定為 `true`，策略 `DRAFT` 狀態也將參與。 |
| `labels` | 一組資料使用標籤，用於test市場推廣操作。<br><br>**重要**:使用此屬性時， `entityList` 屬性不能包含在同一對象中。 要使用資料集和/或欄位評估相同的市場營銷操作，必須在請求負載中包含一個單獨的對象，該對象包含 `entityList` 陣列。 |
| `entityList` | 這些資料集中的一組資料集和（可選）特定欄位，以test針對的營銷操作。<br><br>**重要**:使用此屬性時， `labels` 屬性不能包含在同一對象中。 要使用特定資料使用標籤評估同一市場營銷操作，必須在請求負載中包含一個單獨的對象，該對象包含 `labels` 陣列。 |
| `entityType` | 要test市場營銷活動的實體類型。 當前，僅 `dataSet` 支援。 |
| `entityId` | 要test市場營銷操作的資料集的ID。 |
| `entityMeta.fields` | （可選）資料集中特定欄位的清單，以test市場營銷操作。 |

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

的 [!DNL Policy Service] API還可用於檢查是否存在與使用 [!DNL Real-Time Customer Profile] 段。 請參閱上的教程 [強制對受眾群實施資料使用合規性](../../segmentation/tutorials/governance.md) 的子菜單。
