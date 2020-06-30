---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 策略
topic: developer guide
translation-type: tm+mt
source-git-commit: 1a835c6c20c70bf03d956c601e2704b68d4f90fa
workflow-type: tm+mt
source-wordcount: '940'
ht-degree: 0%

---


# 政策評估

建立行銷動作並定義原則後，您就可以使用「原則服務API」來評估是否有某些動作違反了任何原則。 傳回的限制採用一組原則的形式，這些原則會因嘗試對包含資料使用標籤的指定資料執行行銷動作而遭到違反。

預設情況下， **只有狀態設定為「ENABLED」的策略才參與評估**，但您可以使用查詢參數 `?includeDraft=true` ，在評估中包括「DRAFT」策略。

評量要求可透過下列三種方式之一提出：

1. 若有一組資料使用標籤和行銷動作，此動作是否違反任何原則？
1. 如果有一或多個資料集和行銷動作，此動作會違反任何原則嗎？
1. 給定一個或多個資料集以及每個資料集中一個或多個欄位的子集，此操作是否違反任何策略？

## 使用資料使用標籤和行銷動作評估原則

根據資料使用標籤的存在性評估違反原則的情況時，您必須指定在請求期間資料上會顯示的標籤集。 這是透過使用查詢參數來完成的，其中資料使用標籤會以逗號分隔的值清單提供，如下列範例所示。

**API格式**

```http
GET /marketingActions/core/{marketingActionName}/constraints?duleLabels={value1},{value2}
GET /marketingActions/custom/{marketingActionName}/constraints?duleLabels={value1},{value2}
```

**請求**

以下的範例請求會評估標籤C1和C3的行銷動作。 使用資料使用標籤評估原則時，請牢記下列事項：
* **資料使用標籤區分大小寫。** 上述請求會傳回違反的原則，而使用小寫標籤提出相同的請求(例如： `"c1,c3"`, `"C1,c3"`, `"c1,C3"`)否。
* **請注意您的原則運`AND`算式`OR`中的和運算子。** 在此範例中，如果請求中單獨顯`C1` 示了標籤( `C3`或)，行銷動作就不會違反此政策。 需要兩個標籤(`C1 AND C3`)才能傳回違反的原則。 請確定您正在仔細評估政策，並同時定義政策陳述式。

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/sampleMarketingAction/constraints?duleLabels=C1,C3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

回應物件包含 `duleLabels` 應符合請求中所傳送之標籤的陣列。 如果對資料使用標籤執行指定的行銷操作違反策略，陣 `violatedPolicies` 列將包含受影響策略（或策略）的詳細資訊。 如果未違反任何策略，則陣 `violatedPolicies` 列將顯示為空(`[]`)。

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

## 使用資料集和行銷動作評估策略

您也可以指定可從中收集資料使用標籤的一或多個資料集的ID，以評估違反原則的情況。 這是透過對行銷動作的核心或自訂端點執行POST要求，並在 `/constraints` 要求內文中指定資料集ID，如下所示。

**API格式**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**請求**

請求主體包含一個陣列，每個資料集ID都有一個物件。 由於您要傳送請求內文，因此「內容類型： application/json&quot;請求標題為必要項目，如下列範例所示。

```SHELL
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

**回應**

響應對象包括一個 `duleLabels` 陣列，該陣列包含在指定資料集內找到的所有標籤的統一清單。 此清單包含資料集內所有欄位的資料集和欄位層級標籤。

該響應還包括一個 `discoveredLabels` 包含每個資料集的對象的陣列，該陣列 `datasetLabels` 顯示細分為資料集和欄位級標籤。 每個欄位層級標籤都會顯示含有該標籤之特定欄位的路徑。

如果指定的行銷動作違反了涉及資料集內 `duleLabels` 的策略，則陣 `violatedPolicies` 列將包含受影響策略（或策略）的詳細資訊。 如果未違反任何策略，則陣 `violatedPolicies` 列將顯示為空(`[]`)。

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

## 使用資料集、欄位和行銷動作評估原則

除了提供一個或多個資料集ID外，還可以指定來自每個資料集內的欄位的子集，指示僅應評估這些欄位上的資料使用標籤。 與僅包含資料集的POST請求類似，此請求會將每個資料集的特定欄位新增至請求主體。

使用資料集欄位評估原則時，請牢記下列事項：

* **欄位名稱區分大小寫。** 提供欄位時，必須如實地寫入欄位，如資料集中的欄位( `firstName` vs `firstname`)。
* **資料集標籤繼承。** 資料使用標籤可套用至多個層級，並可向下繼承。 如果您的策略評估未按您所認為的方式返回，請務必將資料集的繼承標籤檢查到欄位，以及欄位層級上套用的標籤。

**API格式**

```http
POST /marketingActions/core/{marketingActionName}/constraints
POST /marketingActions/custom/{marketingActionName}/constraints
```

**請求**

請求主體包含一個陣列，每個資料集ID包含一個對象，該資料集內應用於評估的欄位子集。 由於您要傳送請求內文，因此「內容類型： application/json&quot;請求標題為必要項目，如下列範例所示。

```SHELL
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

**回應**

響應對象包括一個 `duleLabels` 陣列，該陣列包含在指定欄位上找到的統一標籤清單。 請記住，這也包含資料集標籤，因為這些標籤會繼承至欄位。

如果對提供欄位中的資料執行指定的行銷動作而違反原則，陣列將 `violatedPolicies` 包含受影響之原則（或原則）的詳細資料。 如果未違反任何策略，則陣 `violatedPolicies` 列將顯示為空(`[]`)。

在以下回應中，您會看到清單變短 `duleLabels` ，每個資料集的清單也變短，因 `discoveredLabels` 為它只包含請求內文中指定的欄位。 您也會注意到，先前違反的原則「定位廣告或內容」需要兩個標 `C4 AND C6` 簽，因此不再違反該原則，而數 `violatedPolicies` 組會顯示空白。

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

## 策略評估 [!DNL Real-time Customer Profile]

此 [!DNL Policy Service] API也可用來檢查與使用區段有關的原則違 [!DNL Real-time Customer Profile] 規。 如需詳細資訊，請參 [閱關於強制受眾區段資料使用符合性](../../segmentation/tutorials/governance.md) 的教學課程。