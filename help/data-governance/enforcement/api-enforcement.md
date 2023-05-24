---
keywords: Experience Platform；首頁；熱門主題；策略實施；自動實施；基於API的實施；資料治理；測試
solution: Experience Platform
title: 使用策略服務API強制實施資料使用策略
type: Tutorial
description: 為資料建立了資料使用量標籤，並針對這些標籤建立了市場營銷操作的使用量策略後，您可以使用策略服務API來評估在資料集或任意標籤組上執行的市場營銷操作是否構成策略違規。 然後，您可以設定自己的內部協定，以根據API響應處理策略違規。
exl-id: 093db807-c49d-4086-a676-1426426b43fd
source-git-commit: 7b15166ae12d90cbcceb9f5a71730bf91d4560e6
workflow-type: tm+mt
source-wordcount: '1002'
ht-degree: 1%

---

# 使用 [!DNL Policy Service] API

為資料建立了資料使用標籤，並為針對這些標籤的市場營銷操作建立了使用策略後，您就可以使用 [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/) 評估在資料集或任意標籤組上執行的市場營銷操作是否構成策略違規。 然後，您可以設定自己的內部協定，以根據API響應處理策略違規。

>[!NOTE]
>
>預設情況下，只有狀態設定為 `ENABLED` 可以參與評估。 允許 `DRAFT` 要參與評估的策略，必須包括查詢參數 `includeDraft=true` 的子菜單。

本文檔提供了有關如何使用 [!DNL Policy Service] 用於檢查不同方案中的策略違規的API。

## 快速入門

本教程要求對實施資料使用策略所涉及的下列關鍵概念有正確理解：

* [資料治理](../home.md):框架 [!DNL Platform] 強制實施資料使用合規性。
   * [資料使用標籤](../labels/overview.md):資料使用標籤被應用到資料集（和/或這些資料集中的各個欄位），指定了如何使用該資料的限制。
   * [資料使用策略](../policies/overview.md):資料使用策略是描述某些資料使用標籤集允許或限制的市場營銷操作類型的規則。
* [沙箱](../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

在開始本教程之前，請複習 [開發者指南](../api/getting-started.md) 獲取您需要瞭解的重要資訊，以便成功撥打 [!DNL Policy Service] API，包括所需的標頭以及如何讀取示例API調用。

## 使用標籤和市場營銷操作評估

您可以通過針對資料集中假設存在的一組資料使用標籤測試市場營銷操作來評估策略。 這是通過 `duleLabels` 查詢參數，其中標籤以逗號分隔的值清單形式提供，如下例所示。

**API格式**

```http
GET /marketingActions/core/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
GET /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints?duleLabels={LABEL_1},{LABEL_2}
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 與您正在評估的資料使用策略關聯的市場營銷操作的名稱。 |
| `{LABEL_1}` | 用於test市場營銷操作的資料使用標籤。 必須至少提供一個標籤。 提供多個標籤時，必須用逗號分隔。 |

**要求**

以下請求test `exportToThirdParty` 針對標籤的營銷操作 `C1` 和 `C3`。 由於您在本教程前面建立的資料使用策略定義了 `C1` 標籤為 `deny` 策略表達式中的條件，市場營銷操作應觸發策略違規。

>[!NOTE]
>
>資料使用標籤區分大小寫。 僅當其策略表達式中定義的標籤完全匹配時，才會發生策略違規。 在此示例中， `C1` 標籤將觸發違規，而 `c1` 標籤不會。

```shell
curl -X GET \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints?duleLabels=C1,C3 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應將返回市場營銷操作的URL、它所測試的使用標籤，以及由於針對這些標籤測試操作而違反的任何策略的清單。 在本示例中，「將資料導出到第三方」策略如 `violatedPolicies` 陣列，指示市場營銷操作觸發了預期的策略違規。

```json
{
    "timestamp": 1565727821209,
    "clientId": "string",
    "userId": "string",
    "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
| `violatedPolicies` | 列出測試市場營銷操作所違反的任何策略的陣列(在 `marketingActionRef`) `duleLabels`。 |

## 使用資料集評估

您可以通過針對一個或多個資料集測試市場營銷操作來評估資料使用策略，可從這些資料集收集標籤。 這是通過向 `/marketingActions/core/{MARKETING_ACTION_NAME}/constraints` 並在請求體中提供資料集ID，如下例所示。

**API格式**

```http
POST /marketingActions/core/{MARKETING_ACTION_NAME}/constraints
POST /marketingActions/custom/{MARKETING_ACTION_NAME}/constraints
```

| 參數 | 說明 |
| --- | --- |
| `{MARKETING_ACTION_NAME}` | 與要評估的策略關聯的市場營銷操作的名稱。 |

**要求**

以下請求test `exportToThirdParty` 針對三個不同的資料集執行營銷操作。 資料集由負載中提供的陣列中的類型和ID引用。

```shell
curl -X POST \
  https://platform.adobe.io/data/foundation/dulepolicy/marketingActions/custom/exportToThirdParty/constraints
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
| `entityType` | 負載陣列中的每個項目必須指示要定義的實體類型。 對於此使用情形，值將始終為&quot;dataSet&quot;。 |
| `entityId` | 負載陣列中的每個項必須為資料集提供唯一ID。 |
| `entityMeta.fields` | （可選） [JSON指針](../../landing/api-fundamentals.md#json-pointer) 字串，引用資料集架構中的特定欄位。 如果包含此陣列，則只有該陣列中包含的欄位參與評估。 陣列中未包括的任何架構欄位將不參與評估。<br><br>如果未包括此欄位，則資料集架構中的所有欄位都將包括在評估中。 |

**回應**

成功的響應返回市場營銷操作的URL、從提供的資料集收集的用法標籤，以及由於針對這些標籤測試操作而違反的任何策略的清單。 在本示例中，「將資料導出到第三方」策略如 `violatedPolicies` 陣列，指示市場營銷操作觸發了預期的策略違規。

```json
{
    "timestamp": 1556324277895,
    "clientId": "{CLIENT_ID}",
    "userId": "{USER_ID}",
    "imsOrg": "{ORG_ID}",
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
            "imsOrg": "{ORG_ID}",
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
| `duleLabels` | 從請求負載中提供的資料集中提取的資料使用標籤的清單。 |
| `discoveredLabels` | 請求負載中提供的資料集清單，其中顯示了在每個負載中找到的資料集級別和欄位級別標籤。 |
| `violatedPolicies` | 列出測試市場營銷操作所違反的任何策略的陣列(在 `marketingActionRef`) `duleLabels`。 |

## 後續步驟

通過閱讀此文檔，您在資料集或一組資料使用標籤上執行市場營銷操作時成功檢查了策略違規。 使用API響應中返回的資料，您可以在體驗應用程式內設定協定，以在發生策略違規時適當強制執行策略違規。

有關平台如何為激活的段自動提供策略實施的資訊，請參見上的指南 [自動執行](./auto-enforcement.md)。
