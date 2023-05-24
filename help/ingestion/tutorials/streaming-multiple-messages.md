---
keywords: Experience Platform；首頁；熱門主題；流接收；接收；多條消息；
solution: Experience Platform
title: 在單個HTTP請求中發送多個消息
type: Tutorial
description: 本文檔提供一個教程，用於在單個HTTP請求內使用流接收向Adobe Experience Platform發送多條消息。
exl-id: 04045090-8a2c-42b6-aefa-09c043ee414f
source-git-commit: 3ad5c06db07b360df255d3afb1c177cc5de613bb
workflow-type: tm+mt
source-wordcount: '1490'
ht-degree: 1%

---

# 在單個HTTP請求中發送多個消息

將資料流式傳輸到Adobe Experience Platform時，進行大量HTTP調用可能會非常昂貴。 例如，建立1KB負載的1個HTTP請求時，不必建立200個HTTP請求，而建立200條每條1KB消息的1個HTTP請求時，只需200KB負載，效率要高得多。 正確使用時，在單個請求中對多個消息進行分組是優化發送到的資料的最佳方法 [!DNL Experience Platform]。

本文檔提供了將多個消息發送到 [!DNL Experience Platform] 在單個HTTP請求中使用流接收。

## 快速入門

本教程需要對Adobe Experience Platform進行有效的瞭解 [!DNL Data Ingestion]。 在開始本教程之前，請查看以下文檔：

- [資料接收概述](../home.md):涵蓋 [!DNL Experience Platform Data Ingestion]包括攝取方法和資料連接器。
- [流攝入概述](../streaming-ingestion/overview.md):工作流和流式接收的構建塊，如流連接、資料集、 [!DNL XDM Individual Profile], [!DNL XDM ExperienceEvent]。

本教程還要求您完成 [驗證到Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) 教程，以便成功調用 [!DNL Platform] API。 完成身份驗證教程提供了本教程中所有API調用所需的授權標頭的值。 標頭在示例調用中顯示如下：

- 授權：持 `{ACCESS_TOKEN}`

所有POST請求都需要附加標題：

- 內容類型：應用程式/json

## 建立流連接

必須先建立流連接，然後才能啟動流資料到 [!DNL Experience Platform]。 閱讀 [建立流連接](./create-streaming-connection.md) 的子菜單。

註冊流連接後，作為資料生成者，您將擁有一個唯一的URL，該URL可用於將資料流傳輸到平台。

## 流到資料集

以下示例說明如何在單個HTTP請求中向特定資料集發送多個消息。 在消息標頭中插入資料集ID，以便直接將該消息接收到它中。

可以使用 [!DNL Platform] UI或使用API中的清單操作。 可在上找到資料集ID [Experience Platform](https://platform.adobe.com) 去 **[!UICONTROL 資料集]** 頁籤，按一下要為其指定ID的資料集，然後從 **[!UICONTROL 資訊]** 頁籤。 查看 [目錄服務概述](../../catalog/home.md) 有關如何使用API檢索資料集的資訊。

您可以建立新資料集，而不是使用現有資料集。 請閱讀 [使用API建立資料集](../../catalog/api/create-dataset.md) 教程，瞭解有關使用API建立資料集的詳細資訊。

**API格式**

```http
POST /collection/batch/{CONNECTION_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 建立的流連接的ID。 |

**要求**

```shell
curl -X POST https://dcs.adobedc.net/collection/batch/{CONNECTION_ID} \
  -H 'Content-Type: application/json' \
  -d '{
  "messages": [
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Fernie Snow",
              "quantity": 30,
              "priceTotal": 7.8
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "gregdorcey@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "7af6adcc-dc9e-4692-b826-55d2abe68c11",
          "timestamp": "2019-02-23T22:07:31Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Carmine Santiago",
              "quantity": 10,
              "priceTotal": 5.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "emilyong@example.com"
                  }
                }
              }
            }
          }
        }
      }
    }
  ]
}'
```

**回應**

成功的響應返回HTTP狀態207（多狀態）。 查看響應正文可提供有關請求中執行的每個方法的成功或失敗的詳細資訊。 為請求消息陣列的每個元素返迴響應。 以下是無消息失敗的成功響應示例：

```json
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565628583792:1485:153",
    "receivedTimeMs": 1565628583854,
    "responses": [
        {
            "xactionId": "1565628583792:1485:153:0"
        },
        {
            "xactionId": "1565628583792:1485:153:1"
        }
    ]
}
```

有關狀態代碼的詳細資訊，請參閱 [響應碼](#response-codes) 的下一頁。

## 識別失敗消息

與使用單條消息發送請求相比，當發送具有多條消息的HTTP請求時，還需要考慮其他因素，例如：如何確定資料何時發送失敗、哪些特定消息無法發送以及如何檢索這些消息，以及當同一請求中的其他消息失敗時成功的資料將發生什麼情況。

在繼續本教程之前，建議先查看 [檢索失敗批](../quality/retrieve-failed-batches.md) 的子菜單。

### 發送包含有效和無效消息的請求負載

以下示例顯示當批處理包含有效和無效消息時會發生的情況。

請求負載是表示XDM架構中事件的JSON對象的陣列。 請注意，要成功驗證消息，需要滿足以下條件：
- 的 `imsOrgId` 消息標頭中的欄位必須與入口定義匹配。 如果請求負載不包括 `imsOrgId` 的 [!DNL Data Collection Core Service] (DCCS)將自動添加欄位。
- 消息的標頭應引用在 [!DNL Platform] UI。
- 的 `datasetId` 欄位需要在中引用現有資料集 [!DNL Platform]，及其架構需要與中提供的架構匹配 `header` 請求正文中包含的每個消息中的對象。

**API格式**

```http
POST /collection/batch/{CONNECTION_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 建立的資料入口的ID。 |

**要求**

```shell
curl -X POST https://dcs.adobedc.net/collection/batch/{CONNECTION_ID} \
  -H 'Content-Type: application/json' \
  -d '{
  "messages": [
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Tip Top Collection",
              "quantity": 15,
              "priceTotal": 9.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "rogerkanagawa@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      }
    },
    {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "invalidIMSOrg@AdobeOrg",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Carmine Santiago",
              "quantity": 10,
              "priceTotal": 5.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          },
          "_experience": {
            "campaign": {
              "message": {
                "profileSnapshot": {
                  "workEmail": {
                    "address": "mohandeewar@example.com"
                  }
                }
              }
            }
          }
        }
      }
    },
   {
      "header": {
        "schemaRef": {
          "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
          "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
          "environment": {
            "browserDetails": {
              "userAgent": "Mozilla/5.0 (Windows NT 5.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/29.0.1547.57 Safari/537.36 OPR/16.0.1196.62",
              "acceptLanguage": "en-US",
              "cookiesEnabled": true,
              "javaScriptVersion": "1.6",
              "javaEnabled": true
            },
            "colorDepth": 32,
            "viewportHeight": 799,
            "viewportWidth": 414
          },
          "productListItems": [
            {
              "SKU": "CC",
              "name": "Tip Top Collection",
              "quantity": 15,
              "priceTotal": 9.5
            }
          ],
          "commerce": {
            "productViews": {
              "value": 1
            }
          }
        }
      }
    },
    {
      "header": {
        "msgType": "xdmEntityCreate",
        "msgId": "79d2e715-f25f-4c36",
        "xdmSchema": {
          "name": "_xdm.context.experienceevent"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "createdAt": 1526283801869
      },
      "body": {
        "xdmMeta": {
          "xdmSchema": {
            "name": "_xdm.context.experienceevent"
          }
        },
        "xdmEntity": {
          "_id": "abc",
          "dataSource": {
            "_id": "http://abc.com/abc"
          },
          "timestamp": "2018-05-18T15:28:25Z",
          "endUserIDs": {
            "_vendor": {
              "adobe": {
                "experience": {
                  "mcId": {
                    "id": "http://abc.com/abc"
                  }
                }
              }
            }
          }
        }
      }
    }
  ]
}'
```

**回應**

響應負載包括每個消息的狀態以及中的GUID `xactionId` 可用於跟蹤。

```JSON
{
    "inletId": "9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5",
    "batchId": "1565638336649:1750:244",
    "receivedTimeMs": 1565638336705,
    "responses": [
        {
            "xactionId": "1565650704337:2124:92:3"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has unknown xdm format"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has an absent or wrong ims org in the header"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{ORG_ID}] Message has unknown xdm format"
        }
    ]
}
```

上面的示例響應顯示上一個請求的錯誤消息。 通過將此響應與先前的有效響應進行比較，您可以觀察到請求導致部分成功，其中一條消息被成功接收，三條消息導致失敗。 請注意，這兩個響應都返回「207」狀態代碼。 有關狀態代碼的詳細資訊，請參閱 [響應碼](#response-codes) 的下一頁。

第一條消息已成功發送到 [!DNL Platform] 不受其他消息結果的影響。 因此，在嘗試重新發送失敗消息時，不需要重新包含此消息。

第二個消息失敗，因為它缺少消息正文。 收集請求要求消息元素具有有效的標頭和正文部分。 在第二條消息的標頭後添加以下代碼將修復請求，允許第二條消息通過驗證：

```JSON
      "body": {
        "xdmMeta": {
          "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;{SCHEMA_VERSION}"
          }
        },
        "xdmEntity": {
          "_id": "9af5adcc-db9c-4692-b826-65d3abe68c22",
          "timestamp": "2019-02-23T22:07:01Z",
        }
    },
```

第三條消息失敗，因為標頭中使用的組織ID無效。 組織必須與您嘗試發佈到的{CONNECTION_ID}匹配。 要確定與您使用的流連接匹配的組織ID，您可以執行 `GET inlet` 使用 [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)。 請參閱 [檢索流連接](./create-streaming-connection.md#get-data-collection-url) 例如，如何檢索以前建立的流連接。

第四條消息失敗，因為它未遵循預期的XDM架構。 的 `xdmSchema` 請求的標頭和正文中包含的XDM架構與 `{DATASET_ID}`。 更正消息標頭和正文中的架構允許其通過DCCS驗證並成功發送到 [!DNL Platform]。 還必須更新消息正文，以匹配 `{DATASET_ID}` 通過流驗證 [!DNL Platform]。 有關成功流入平台的消息將發生什麼情況的詳細資訊，請參見 [確認已發送的消息](#confirm-messages-ingested) 本教程中的「」部分。

### 從中檢索失敗的消息 [!DNL Platform]

失敗消息由響應陣列中的錯誤狀態代碼標識。
無效消息將收集並儲存在由指定的資料集中的「錯誤」批中 `{DATASET_ID}`。

閱讀 [檢索失敗批](../quality/retrieve-failed-batches.md) 的子菜單。

## 確認接收的消息

通過DCCS驗證的消息流式傳輸到 [!DNL Platform]。 開 [!DNL Platform]，在將批消息接收到 [!DNL Data Lake]。 批處理的狀態（無論成功與否）顯示在由 `{DATASET_ID}`。

您可以查看成功流到的批處理消息的狀態 [!DNL Platform] 使用 [Experience PlatformUI](https://platform.adobe.com) 去 **[!UICONTROL 資料集]** 頁籤，按一下要流式處理的資料集，然後檢查 **[!UICONTROL 資料集活動]** 頁籤。

通過流驗證的批消息 [!DNL Platform] 被攝入 [!DNL Data Lake]。 然後，這些消息可用於分析或導出。

## 後續步驟

現在，您知道如何在單個請求中發送多個消息並驗證何時將消息成功接收到目標資料集中，您就可以開始將自己的資料流式傳輸到 [!DNL Platform]。 有關如何從中查詢和檢索已接收資料的概述 [!DNL Platform]，請參見 [[!DNL Data Access]](../../data-access/tutorials/dataset-data.md) 的子菜單。

## 附錄

本節包含本教程的補充資訊。

### 回應代碼

下表顯示了成功和失敗響應消息返回的狀態代碼。

| 狀態代碼 | 說明 |
| :---: | --- |
| 207 | 儘管「207」被用作整體響應狀態代碼，但接收者需要查詢多狀態響應體的內容，以獲得關於方法執行的成功或失敗的進一步資訊。 響應代碼用於成功、部分成功以及失敗情況。 |
| 400 | 請求有問題。 有關更具體的錯誤消息，請參見響應正文（例如，消息負載缺少必需欄位，或消息為未知xdm格式）。 |
| 401 | 未授權：請求缺少有效的授權標頭。 僅對啟用了身份驗證的入口返回此選項。 |
| 403 | 未授權：提供的授權令牌無效或已過期。 僅對啟用了身份驗證的入口返回此選項。 |
| 413 | 負載太大 — 當總負載請求大於1MB時拋出。 |
| 429 | 在指定的時長內請求過多。 |
| 500 | 處理負載時出錯。 有關更特定的錯誤消息（例如，未指定消息負載架構或與中的XDM定義不匹配），請參見響應正文 [!DNL Platform])。 |
| 503 | 服務當前不可用。 客戶端應至少使用指數式回退策略重試3次。 |
