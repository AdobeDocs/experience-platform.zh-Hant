---
keywords: Experience Platform;home；熱門主題；策略實施；自動實施；基於API的實施；資料治理；測試
solution: Experience Platform
title: 使用原則服務API強制使用資料原則
topic-legacy: guide
type: Tutorial
description: 一旦您為資料建立了資料使用標籤，並針對這些標籤建立了行銷動作的使用原則，您就可以使用原則服務API來評估在資料集或任意標籤群組上執行的行銷動作是否構成原則違規。 然後，您可以設定自己的內部通訊協定，以根據API回應來處理原則違規。
exl-id: 093db807-c49d-4086-a676-1426426b43fd
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 1%

---

# 使用[!DNL Policy Service] API強制執行資料使用原則

為您的資料建立資料使用標籤並針對這些標籤建立行銷動作的使用原則後，您就可使用[[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml)來評估在資料集或任意標籤群組上執行的行銷動作是否構成原則違規。 然後，您可以設定自己的內部通訊協定，以根據API回應來處理原則違規。

>[!NOTE]
>
>預設情況下，只有狀態設定為`ENABLED`的策略才能參與評估。 要允許`DRAFT`策略參與評估，必須在請求路徑中包含查詢參數`includeDraft=true`。

本檔案提供如何使用[!DNL Policy Service] API來檢查不同情況下是否違反原則的步驟。

## 快速入門

本教學課程需要有效瞭解下列在實施資料使用政策時涉及的主要概念：

* [資料治理](../home.md):強制執行資料使 [!DNL Platform] 用合規性的框架。
   * [資料使用標籤](../labels/overview.md):資料使用標籤會套用至資料集（和／或這些資料集內的個別欄位），並指定資料的使用限制。
   * [資料使用原則](../policies/overview.md):資料使用原則是描述特定資料使用標籤集所允許或限制之行銷動作類型的規則。
* [沙盒](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙盒，可將單一執行個體分 [!DNL Platform] 割為不同的虛擬環境，以協助開發和發展數位體驗應用程式。

在開始本教學課程之前，請先閱讀[開發人員指南](../api/getting-started.md)，以取得成功呼叫[!DNL Policy Service] API所需的重要資訊，包括必要的標題和如何讀取範例API呼叫。

## 使用標籤和行銷動作進行評估

您可以針對資料集內假設存在的資料使用標籤集測試行銷動作，以評估原則。 這是透過使用`duleLabels`查詢參數來完成的，其中標籤是以逗號分隔的值清單提供，如下例所示。

**API格式**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 與您所評估的資料使用政策相關聯的行銷動作名稱。 |
| `{LABEL_1}` | 用於測試行銷動作的資料使用標籤。 必須至少提供一個標籤。 提供多個標籤時，必須以逗號分隔。 |

**要求**

下列請求會針對標籤`C1`和`C3`測試`exportToThirdParty`行銷動作。 由於您在本教學課程中先前建立的資料使用原則將`C1`標籤定義為其原則運算式中的`deny`條件之一，因此行銷動作應觸發原則違規。

>[!NOTE]
>
>資料使用標籤會區分大小寫。 策略違規僅在其策略表達式中定義的標籤完全匹配時才發生。 在此範例中，`C1`標籤會觸發違規，而`c1`標籤則不會觸發違規。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回行銷動作的URL、它所測試的使用標籤，以及測試這些標籤的動作而違反的任何原則清單。 在此範例中，`violatedPolicies`陣列中顯示「將資料匯出至第三方」原則，指出行銷動作觸發預期的原則違規。

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
| `violatedPolicies` | 列出任何違反策略的陣列，這些策略是根據提供的`duleLabels`測試行銷操作（在`marketingActionRef`中指定）。 |

## 使用資料集進行評估

您可以針對一或多個可收集標籤的資料集測試行銷動作，以評估資料使用策略。 若要這麼做，請向`/marketingActions/core/{MARKETING_ACTION_NAME}/constraints`提出POST請求，並在請求內文中提供資料集ID，如下例所示。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 與您所評估之原則相關聯的行銷動作名稱。 |

**要求**

下列請求會針對三個不同的資料集測試`exportToThirdParty`行銷動作。 資料集是由裝載中提供之陣列中的類型和ID所參考。

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
| `entityType` | 裝載陣列中的每個項目都必須指示要定義的實體類型。 在此使用案例中，值一律為&quot;dataSet&quot;。 |
| `entityId` | 裝載陣列中的每個項目都必須提供資料集的唯一ID。 |
| `entityMeta.fields` | （可選）[JSON指針](../../landing/api-fundamentals.md#json-pointer)字串的陣列，參考資料集結構中的特定欄位。 如果包含此陣列，則只有陣列中包含的欄位參與評估。 陣列中未包含的任何架構欄位將不參與評估。<br><br>如果未包含此欄位，則評估中會包含資料集架構中的所有欄位。 |

**回應**

成功的回應會傳回行銷動作的URL、從提供的資料集收集到的使用標籤，以及測試這些標籤的動作而違反的任何原則清單。 在此範例中，`violatedPolicies`陣列中顯示「將資料匯出至第三方」原則，指出行銷動作觸發預期的原則違規。

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
| `duleLabels` | 從請求裝載中提供的資料集擷取的資料使用標籤清單。 |
| `discoveredLabels` | 請求裝載中提供的資料集清單，顯示每個資料集層級和欄位層級標籤。 |
| `violatedPolicies` | 列出任何違反策略的陣列，這些策略是根據提供的`duleLabels`測試行銷操作（在`marketingActionRef`中指定）。 |

## 後續步驟

閱讀本檔案後，您已成功檢查在資料集或一組資料使用標籤上執行行銷動作時是否有違反原則的情況。 使用API回應中傳回的資料，您可以在體驗應用程式中設定通訊協定，以便在發生違反原則的情況時適當強制執行。

如需有關平台如何自動為已啟動的區段提供策略實施的資訊，請參閱[automatic enforcement](./auto-enforcement.md)上的指南。
