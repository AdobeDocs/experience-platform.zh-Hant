---
keywords: Experience Platform；首頁；熱門主題；原則執行；自動執行；API型執行；資料控管；測試
solution: Experience Platform
title: 使用策略服務API強制資料使用策略
topic-legacy: guide
type: Tutorial
description: 為資料建立了資料使用標籤，並針對這些標籤建立了市場營銷操作的使用策略後，您可以使用策略服務API來評估對資料集或任意標籤組執行的市場營銷操作是否構成策略違規。 然後，您可以設定自己的內部通訊協定，以根據API回應處理違反政策的情況。
exl-id: 093db807-c49d-4086-a676-1426426b43fd
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 1%

---

# 使用[!DNL Policy Service] API強制執行資料使用原則

為資料建立了資料使用標籤，並針對這些標籤建立了市場營銷操作的使用策略後，您可以使用[[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/)評估對資料集或任意標籤組執行的市場營銷操作是否構成策略違規。 然後，您可以設定自己的內部通訊協定，以根據API回應處理違反政策的情況。

>[!NOTE]
>
>預設情況下，只有狀態設定為`ENABLED`的策略才能參與評估。 若要允許`DRAFT`原則參與評估，您必須在請求路徑中加入查詢參數`includeDraft=true`。

本檔案提供如何使用[!DNL Policy Service] API來檢查不同情況下是否有違反原則的情況。

## 快速入門

本教學課程需要妥善了解執行資料使用原則時涉及的下列重要概念：

* [資料控管](../home.md):強制資料使用 [!DNL Platform] 法規遵循的框架。
   * [資料使用量標籤](../labels/overview.md):資料使用量標籤會套用至資料集（和/或這些資料集內的個別欄位），並指定該資料的使用方式限制。
   * [資料使用原則](../policies/overview.md):資料使用原則是描述特定資料使用標籤集允許或限制的行銷動作類型的規則。
* [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供可將單一執行個體分割成個 [!DNL Platform] 別虛擬環境的虛擬沙箱，以協助開發及改進數位體驗應用程式。

開始本教學課程之前，請檢閱[開發人員指南](../api/getting-started.md)中的重要資訊，以取得您需要知道的重要資訊，以便成功呼叫[!DNL Policy Service] API，包括必要的標題以及如何讀取範例API呼叫。

## 使用標籤和行銷動作進行評估

您可以針對資料集中假設存在的資料使用量標籤集測試行銷動作，以評估原則。 這需透過使用`duleLabels`查詢參數來完成，其中標籤是以逗號分隔的值清單提供，如下列範例所示。

**API格式**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 與您評估的資料使用政策相關聯的行銷動作名稱。 |
| `{LABEL_1}` | 用於測試行銷動作的資料使用量標籤。 必須至少提供一個標籤。 提供多個標籤時，必須以逗號分隔。 |

**要求**

下列請求會針對標籤`C1`和`C3`測試`exportToThirdParty`行銷動作。 由於您在本教學課程前面建立的資料使用原則會將`C1`標籤定義為其原則運算式中的`deny`條件之一，因此行銷動作應會觸發原則違反。

>[!NOTE]
>
>資料使用量標籤區分大小寫。 只有當其策略表達式中定義的標籤完全匹配時，才會發生策略違規。 在此範例中，`C1`標籤會觸發違反，而`c1`標籤則不會觸發。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回行銷動作的URL、其所測試的使用標籤，以及因針對這些標籤測試動作而違反的任何原則清單。 在此示例中，`violatedPolicies`陣列中顯示了「將資料導出到第三方」策略，表明市場操作觸發了預期的策略違規。

```json
{
    "timestamp": 1565727821209,
    "clientId": "string",
    "userId": "string",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
    "duleLabels": [
        "C1",
        "C3"
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
            "deny": {
                "operator": "OR",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "AND",
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
            "created": 1565651746693,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER",
            "updated": 1565723012139,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
                }
            },
            "id": "5d51f322e553c814e67af1a3"
        }
    ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `violatedPolicies` | 列出任何違反之原則的陣列，針對提供的`duleLabels`測試行銷動作（在`marketingActionRef`中指定）。 |

## 使用資料集進行評估

您可以針對一或多個可收集標籤的資料集測試行銷動作，以評估資料使用政策。 若要這麼做，請向`/marketingActions/core/{MARKETING_ACTION_NAME}/constraints`提出POST要求，並在要求內文中提供資料集ID，如下列範例所示。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 與您評估之政策相關聯的行銷動作名稱。 |

**要求**

下列請求會針對三個不同的資料集測試`exportToThirdParty`行銷動作。 資料集會依裝載中提供之陣列中的類型和ID來參照。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
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
      "entityId": "5cc1fb685410ef14b748c55f",
      "entityMeta": {
          "fields": [
              "/properties/personalEmail/properties/address",
              "/properties/person/properties/name/properties/fullName"
          ]
      }
    }
  ]'
```

| 屬性 | 說明 |
| --- | --- |
| `entityType` | 有效負載陣列中的每個項目必須指示要定義的實體類型。 在此使用案例中，值一律為「dataSet」。 |
| `entityId` | 裝載陣列中的每個項目都必須為資料集提供唯一ID。 |
| `entityMeta.fields` | （選用）[JSON指標](../../landing/api-fundamentals.md#json-pointer)字串的陣列，會參考資料集結構中的特定欄位。 如果包含此陣列，則只有陣列中包含的欄位參與評估。 陣列中未包含的任何架構欄位將不參與評估。<br><br>如果未包含此欄位，評估中將會包含資料集結構中的所有欄位。 |

**回應**

成功的回應會傳回行銷動作的URL、從提供的資料集收集的使用標籤，以及因針對這些標籤測試動作而違反的任何原則清單。 在此示例中，`violatedPolicies`陣列中顯示了「將資料導出到第三方」策略，表明市場操作觸發了預期的策略違規。

```json
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{IMS_ORG}",
    "marketingActionRef": "https://platform.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty",
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
                        "path": "/properties/personalEmail/properties/address",
                    },
                    {
                        "labels": [
                            "C5"
                        ],
                        "path": "/properties/person/properties/name/properties/fullName"
                    }
                ]
            }
        }
    ],
    "violatedPolicies": [
        {
            "name": "Export Data to Third Party",
            "status": "ENABLED",
            "marketingActionRefs": [
                "https://platform-stage.adobe.io:443/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty"
            ],
            "description": "Conditions under which data cannot be exported to a third party",
            "deny": {
                "operator": "OR",
                "operands": [
                    {
                        "label": "C1"
                    },
                    {
                        "operator": "AND",
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
            "created": 1565651746693,
            "createdClient": "{CREATED_CLIENT}",
            "createdUser": "{CREATED_USER",
            "updated": 1565723012139,
            "updatedClient": "{UPDATED_CLIENT}",
            "updatedUser": "{UPDATED_USER}",
            "_links": {
                "self": {
                    "href": "https://platform-stage.adobe.io/data/foundation/dulepolicy/policies/custom/5d51f322e553c814e67af1a3"
                }
            },
            "id": "5d51f322e553c814e67af1a3"
        }
    ]
}
```

| 屬性 | 說明 |
| --- | --- |
| `duleLabels` | 從請求裝載中提供的資料集擷取的資料使用量標籤清單。 |
| `discoveredLabels` | 請求裝載中提供的資料集清單，顯示在每個資料集層級和欄位層級標籤。 |
| `violatedPolicies` | 列出任何違反之原則的陣列，針對提供的`duleLabels`測試行銷動作（在`marketingActionRef`中指定）。 |

## 後續步驟

閱讀本檔案後，您就成功檢查了對資料集或一組資料使用標籤執行行銷動作時是否違反原則。 使用API回應中傳回的資料，您可以在體驗應用程式中設定通訊協定，以在發生原則違規時適當強制執行。

有關Platform如何自動為已激活的段提供策略實施的資訊，請參閱[自動實施](./auto-enforcement.md)的指南。
