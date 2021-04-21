---
keywords: Experience Platform; home；熱門主題；流處理；接收；流處理多個消息；多個消息；
solution: Experience Platform
title: 在單一HTTP請求中傳送多則訊息
topic-legacy: tutorial
type: Tutorial
description: 本檔案提供教學課程，可讓您使用串流擷取功能，在單一HTTP要求內傳送多則訊息至Adobe Experience Platform。
exl-id: 04045090-8a2c-42b6-aefa-09c043ee414f
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1492'
ht-degree: 1%

---

# 在單一HTTP請求中傳送多則訊息

將資料串流至Adobe Experience Platform時，進行大量HTTP呼叫可能會很昂貴。 例如，建立1KB負載的200個HTTP請求，而不是建立1KB負載的200個HTTP請求，建立200個每個1KB訊息的1HTTP請求，而且單一負載為200KB，效率更高。 正確使用時，將多個訊息分組在單一要求中是最佳化傳送至[!DNL Experience Platform]資料的絕佳方式。

本檔案提供教學課程，可讓您使用串流擷取功能，在單一HTTP要求內傳送多則訊息至[!DNL Experience Platform]。

## 快速入門

本教學課程需要對Adobe Experience Platform[!DNL Data Ingestion]有充分的瞭解。 在開始本教學課程之前，請先閱讀下列檔案：

- [資料擷取概觀](../home.md):涵蓋核心概念， [!DNL Experience Platform Data Ingestion]包括擷取方法和資料連接器。
- [串流擷取概觀](../streaming-ingestion/overview.md):串流擷取的工作流程和建立區塊，例如串流連線、資料集 [!DNL XDM Individual Profile]和 [!DNL XDM ExperienceEvent]。

本教學課程還要求您完成[對Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en)的驗證教學課程，以便成功呼叫[!DNL Platform] API。 完成驗證教學課程時，提供本教學課程中所有API呼叫所需之「授權」標題的值。 標題在範例呼叫中顯示如下：

- 授權：載體`{ACCESS_TOKEN}`

所有POST請求都需要額外的標題：

- 內容類型：application/json

## 建立串流連線

您必須先建立串流連線，才能開始將資料串流至[!DNL Experience Platform]。 閱讀[建立串流連線](./create-streaming-connection.md)指南，瞭解如何建立串流連線。

在註冊串流連線後，身為資料產生者的您將擁有可用來將資料串流至平台的唯一URL。

## 串流至資料集

下列範例說明如何在單一HTTP請求中傳送多則訊息至特定資料集。 將資料集ID插入訊息標題中，讓該訊息直接被收錄進來。

您可以使用[!DNL Platform] UI或使用API中的清單操作來取得現有資料集的ID。 在[Experience Platform](https://platform.adobe.com)上可找到資料集ID，方法是前往&#x200B;**[!UICONTROL Datasets]**&#x200B;標籤，按一下您要取得ID的資料集，然後從&#x200B;**[!UICONTROL Info]**&#x200B;標籤上的資料集ID欄位複製字串。 有關如何使用API檢索資料集的資訊，請參見[目錄服務概述](../../catalog/home.md)。

您可以建立新資料集，而不是使用現有資料集。 請閱讀[使用API建立資料集](../../catalog/api/create-dataset.md)教學課程，以取得有關使用API建立資料集的詳細資訊。

**API格式**

```http
POST /collection/batch/{CONNECTION_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 已建立串流連線的ID。 |

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
        "imsOrgId": "{IMS_ORG}",
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
        "imsOrgId": "{IMS_ORG}",
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

成功的回應會傳回HTTP狀態207（多狀態）。 檢閱回應內文可提供請求中執行之每個方法之成功或失敗的詳細資訊。 對請求消息陣列的每個元素返迴響應。 以下是成功回應且無訊息失敗的範例：

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

有關狀態代碼的詳細資訊，請參閱本教程附錄中的[響應代碼](#response-codes)表。

## 標識失敗消息

與使用單一訊息傳送請求相比，當傳送含有多則訊息的HTTP請求時，需考慮其他因素，例如：如何識別資料何時無法傳送、哪些特定訊息無法傳送、如何擷取，以及當相同請求中的其他訊息失敗時，成功的資料會發生什麼情況。

繼續本教程之前，建議先閱讀[檢索失敗批次](../quality/retrieve-failed-batches.md)指南。

### 傳送含有效和無效訊息的請求裝載

以下示例顯示當批處理包含有效和無效消息時會發生什麼情況。

請求裝載是JSON物件的陣列，代表XDM架構中的事件。 請注意，成功驗證訊息需要符合下列條件：
- 消息標題中的`imsOrgId`欄位必須與入口定義匹配。 如果請求裝載未包含`imsOrgId`欄位，[!DNL Data Collection Core Service](DCCS)會自動新增欄位。
- 消息的標題應引用在[!DNL Platform] UI中建立的現有XDM模式。
- `datasetId`欄位需要參考[!DNL Platform]中的現有資料集，其架構需要符合請求主體中每個訊息中`header`物件中提供的架構。

**API格式**

```http
POST /collection/batch/{CONNECTION_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 已建立資料引入的ID。 |

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
        "imsOrgId": "{IMS_ORG}",
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
        "imsOrgId": "{IMS_ORG}",
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
        "imsOrgId": "{IMS_ORG}",
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
        "imsOrgId": "{IMS_ORG}",
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

響應裝載包括每條消息的狀態，以及`xactionId`中可用於跟蹤的GUID。

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
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{IMS_ORG}] Message has unknown xdm format"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{IMS_ORG}] Message has an absent or wrong ims org in the header"
        },
        {
            "statusCode": 400,
            "message": "inletId: [9b0cb233972f3b0092992284c7353f5eead496218e8441a79b25e9421ea127f5] imsOrgId: [{IMS_ORG}] Message has unknown xdm format"
        }
    ]
}
```

上述範例回應顯示先前請求的錯誤訊息。 透過將此回應與先前的有效回應比較，您可以發現請求導致部分成功，其中一則訊息已成功擷取，另外三則訊息導致失敗。 請注意，這兩個回應都會傳回&#39;207&#39;狀態代碼。 有關狀態代碼的詳細資訊，請參閱本教程附錄中的[響應代碼](#response-codes)表。

第一條消息已成功發送到[!DNL Platform]，並不受其他消息結果的影響。 因此，嘗試重新發送失敗的消息時，不需要重新包含此消息。

第二個消息失敗，因為它缺少消息正文。 收集請求會要求訊息元素具有有效的標題和內文區段。 將下列程式碼新增至第二則訊息的標題後，將會修正請求，讓第二則訊息傳遞驗證：

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

第三則訊息因標題中使用的IMS組織ID無效而失敗。 IMS組織必須符合您嘗試張貼至的{CONNECTION_ID}。 若要判斷哪個IMS組織ID符合您使用的串流連線，您可以使用[[!DNL Data Ingestion API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/ingest-api.yaml)執行`GET inlet`請求。 如需如何擷取先前建立之串流連線的範例，請參閱[擷取串流連線](./create-streaming-connection.md#get-data-collection-url)。

第四條消息失敗，因為它未遵循預期的XDM模式。 請求的標頭和正文中包含的`xdmSchema`與`{DATASET_ID}`的XDM模式不匹配。 修正訊息標題和內文中的架構，可讓它傳遞DCCS驗證並成功傳送至[!DNL Platform]。 還必須更新消息主體，使其與`{DATASET_ID}`的XDM模式匹配，以便通過[!DNL Platform]的流驗證。 有關成功流到平台的消息的更多資訊，請參見本教程的[confirm messages ingested](#confirm-messages-ingested)部分。

### 從[!DNL Platform]檢索失敗消息

失敗消息由響應陣列中的錯誤狀態代碼標識。
無效訊息會收集並儲存在`{DATASET_ID}`所指定資料集內的「error」批次中。

有關恢復失敗批處理消息的詳細資訊，請參閱[檢索失敗批處理](../quality/retrieve-failed-batches.md)指南。

## 確認已收錄的訊息

通過DCCS驗證的消息流式化到[!DNL Platform]。 在[!DNL Platform]上，批消息在被收錄到[!DNL Data Lake]之前，通過流驗證進行測試。 批次的狀態（無論是否成功）顯示在由`{DATASET_ID}`指定的資料集中。

您可以前往&#x200B;**[!UICONTROL Datasets]**&#x200B;標籤，按一下您要串流至的資料集，並勾選&#x200B;**[!UICONTROL Dataset Activity]**&#x200B;標籤，使用[Experience PlatformUI](https://platform.adobe.com)檢視成功串流至[!DNL Platform]的批次訊息狀態。

在[!DNL Platform]上通過流驗證的批處理消息將被吸收到[!DNL Data Lake]中。 然後，這些訊息便可供分析或匯出。

## 後續步驟

現在，您知道如何在單一請求中傳送多個訊息並驗證訊息是否成功傳入目標資料集，您可以開始將您自己的資料串流至[!DNL Platform]。 有關如何從[!DNL Platform]查詢和檢索收錄資料的概述，請參閱[[!DNL Data Access]](../../data-access/tutorials/dataset-data.md)指南。

## 附錄

本節包含教學課程的補充資訊。

### 回應代碼

下表顯示成功和失敗響應消息返回的狀態代碼。

| 狀態代碼 | 說明 |
| :---: | --- |
| 207 | 雖然「207」用作整體響應狀態代碼，但接收方需要查閱多狀態響應主體的內容，以瞭解有關方法執行的成功或失敗的進一步資訊。 回應程式碼用於成功、部分成功以及失敗情況。 |
| 400 | 請求有問題。 請參閱回應內文以取得更具體的錯誤訊息（例如，「訊息裝載遺失必要欄位，或「訊息」為未知xdm格式）。 |
| 401 | 未授權：請求缺少有效的授權標題。 僅對啟用了身份驗證的入口返回。 |
| 403 | 未授權： 提供的授權Token無效或已過期。 僅對啟用了身份驗證的入口返回。 |
| 413 | 裝載過大——當總裝載要求大於1MB時拋出。 |
| 429 | 指定時段內的請求過多。 |
| 500 | 處理負載時出錯。 有關更具體的錯誤消息，請參見響應主體（例如，未指定消息裝載模式，或與[!DNL Platform]中的XDM定義不匹配）。 |
| 503 | 服務目前不提供。 客戶端應使用指數式回退策略至少重試3次。 |
