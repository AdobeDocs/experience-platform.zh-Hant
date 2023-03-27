---
keywords: Experience Platform；首頁；熱門主題；串流內嵌；內嵌；串流多則訊息；多則訊息；
solution: Experience Platform
title: 在單一HTTP要求中傳送多則訊息
type: Tutorial
description: 本檔案提供教學課程，說明如何使用串流內嵌，在單一HTTP要求內傳送多則訊息至Adobe Experience Platform。
exl-id: 04045090-8a2c-42b6-aefa-09c043ee414f
source-git-commit: 3ad5c06db07b360df255d3afb1c177cc5de613bb
workflow-type: tm+mt
source-wordcount: '1490'
ht-degree: 1%

---

# 在單一HTTP要求中傳送多則訊息

將資料串流至Adobe Experience Platform時，進行大量HTTP呼叫可能會相當昂貴。 例如，建立1個HTTP要求（每封200則訊息為1KB），而不是使用1KB裝載來建立200個HTTP要求，效率會高很多，而且單一裝載為200KB。 正確使用時，在單一請求中分組多個訊息是最佳化傳送至之資料的絕佳方式 [!DNL Experience Platform].

本檔案提供將多則訊息傳送至 [!DNL Experience Platform] 內，使用串流內嵌。

## 快速入門

本教學課程需要妥善了解Adobe Experience Platform [!DNL Data Ingestion]. 開始本教學課程之前，請檢閱下列檔案：

- [資料擷取概觀](../home.md):涵蓋 [!DNL Experience Platform Data Ingestion]，包括擷取方法和Data Connectors。
- [串流獲取概觀](../streaming-ingestion/overview.md):串流獲取的工作流程和建置區塊，例如串流連線、資料集、 [!DNL XDM Individual Profile]，和 [!DNL XDM ExperienceEvent].

本教學課程也要求您完成 [驗證Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en) 教學課程，以便成功呼叫 [!DNL Platform] API。 完成驗證教學課程，提供本教學課程中所有API呼叫所需的Authorization標題值。 標題在範例呼叫中顯示，如下所示：

- 授權：承載 `{ACCESS_TOKEN}`

所有POST請求都需要額外的標題：

- 內容類型：application/json

## 建立串流連線

您必須先建立串流連線，才能開始將資料串流至 [!DNL Experience Platform]. 閱讀 [建立串流連線](./create-streaming-connection.md) 指南，了解如何建立串流連線。

註冊串流連線後，您（身為資料製作者）會有一個唯一URL，可用來將資料串流至Platform。

## 串流至資料集

下列範例說明如何在單一HTTP要求內傳送多則訊息至特定資料集。 在訊息標題中插入資料集ID，直接內嵌該訊息。

您可以使用 [!DNL Platform] UI或在API中使用清單操作。 可在上找到資料集ID [Experience Platform](https://platform.adobe.com) 去 **[!UICONTROL 資料集]** 標籤，按一下您要用於的資料集，然後從 **[!UICONTROL 資訊]** 標籤。 請參閱 [目錄服務概述](../../catalog/home.md) 以取得如何使用API擷取資料集的資訊。

您可以建立新資料集，而不使用現有資料集。 請閱讀 [使用API建立資料集](../../catalog/api/create-dataset.md) 教學課程，以取得使用API建立資料集的詳細資訊。

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

成功的回應會傳回HTTP狀態207（多狀態）。 檢閱回應內文，可提供要求中執行之每個方法之成敗的詳細資訊。 會針對要求訊息陣列的每個元素傳回回應。 以下是成功回應且沒有訊息失敗的範例：

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

有關狀態代碼的詳細資訊，請參閱 [回應代碼](#response-codes) 本教學課程附錄中的表格。

## 識別失敗的消息

與使用單一訊息傳送請求相比，在使用多個訊息傳送HTTP請求時，需考慮其他因素，例如：如何識別資料無法傳送的時間、無法傳送哪些特定訊息以及如何擷取訊息，以及相同請求中的其他訊息失敗時成功的資料會發生什麼事。

繼續本教學課程之前，建議您先檢閱 [檢索失敗的批](../quality/retrieve-failed-batches.md) 指南。

### 傳送含有有效和無效訊息的要求裝載

以下示例說明了當批包含有效和無效消息時會發生什麼情況。

要求裝載是JSON物件的陣列，代表XDM結構中的事件。 請注意，若要成功驗證訊息，必須符合下列條件：
- 此 `imsOrgId` 報文標題中的欄位必須符合匯入定義。 如果要求裝載未包含 `imsOrgId` 欄位， [!DNL Data Collection Core Service] (DCCS)會自動新增欄位。
- 訊息的標題應參考中建立的現有XDM架構 [!DNL Platform] UI。
- 此 `datasetId` 欄位需要參考 [!DNL Platform]，及其架構必須符合 `header` 要求內文中包含的每則訊息內的物件。

**API格式**

```http
POST /collection/batch/{CONNECTION_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 建立的資料入口ID。 |

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

回應裝載包含每個訊息的狀態，以及 `xactionId` 可用於追蹤。

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

上述範例回應顯示先前請求的錯誤訊息。 將此回應與先前的有效回應進行比較，您可以發現要求導致部分成功，其中一則訊息成功擷取，三則訊息導致失敗。 請注意，兩個回應都會傳回「207」狀態代碼。 有關狀態代碼的詳細資訊，請參閱 [回應代碼](#response-codes) 本教學課程附錄中的表格。

已成功將第一條消息發送到 [!DNL Platform] 和不受其他訊息結果的影響。 因此，在嘗試重新發送失敗的消息時，不需要重新包含此消息。

第二條消息失敗，因為它缺少消息正文。 收集要求要求訊息元素必須具有有效的標題和內文區段。 在第二則訊息的標題後面新增下列程式碼，可修正要求，讓第二則訊息通過驗證：

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

第三則訊息失敗，因為標題中使用的組織ID無效。 組織必須與您嘗試張貼到的{CONNECTION_ID}相符。 若要判斷哪個組織ID符合您使用的串流連線，您可以執行 `GET inlet` 使用 [[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/). 請參閱 [檢索流連接](./create-streaming-connection.md#get-data-collection-url) ，以了解如何擷取先前建立的串流連線。

第四則訊息失敗，因為未遵循預期的XDM架構。 此 `xdmSchema` 請求的標題和內文中包含的XDM結構不符合 `{DATASET_ID}`. 修正訊息標題和內文中的結構，可讓其通過DCCS驗證，並成功傳送至 [!DNL Platform]. 也必須更新訊息內文，以符合 `{DATASET_ID}` 供it透過串流驗證 [!DNL Platform]. 如需成功串流至Platform之訊息有何變化的詳細資訊，請參閱 [確認已擷取訊息](#confirm-messages-ingested) 一節。

### 從檢索失敗的消息 [!DNL Platform]

失敗的消息由響應陣列中的錯誤狀態代碼標識。
無效訊息會收集並儲存在指定資料集內的「錯誤」批次中 `{DATASET_ID}`.

閱讀 [檢索失敗的批](../quality/retrieve-failed-batches.md) 有關恢復失敗批處理消息的詳細資訊的指南。

## 確認已擷取的訊息

通過DCCS驗證的報文流到 [!DNL Platform]. 開啟 [!DNL Platform]，批次訊息會先透過串流驗證測試，再匯入至 [!DNL Data Lake]. 批次狀態（無論是否成功）會顯示在指定的資料集內 `{DATASET_ID}`.

您可以檢視成功串流至的批次訊息的狀態 [!DNL Platform] 使用 [Experience PlatformUI](https://platform.adobe.com) 去 **[!UICONTROL 資料集]** 標籤，按一下您要串流至的資料集，然後檢查 **[!UICONTROL 資料集活動]** 標籤。

透過串流驗證的批次訊息 [!DNL Platform] 被吸入 [!DNL Data Lake]. 然後，這些訊息便可供分析或匯出。

## 後續步驟

現在您知道如何在單一請求中傳送多則訊息，並確認訊息是否成功內嵌至目標資料集，即可開始將您的資料串流至 [!DNL Platform]. 如需如何查詢及擷取擷取資料的概述 [!DNL Platform]，請參閱 [[!DNL Data Access]](../../data-access/tutorials/dataset-data.md) 指南。

## 附錄

本節包含教學課程的補充資訊。

### 回應代碼

下表顯示成功和失敗響應消息返回的狀態代碼。

| 狀態代碼 | 說明 |
| :---: | --- |
| 207 | 雖然將「207」用作整體響應狀態代碼，但接收者需要查閱多狀態響應主體的內容，以獲得有關方法執行的成功或失敗的進一步資訊。 回應程式碼用於成功、部分成功，以及失敗情況。 |
| 400 | 請求有問題。 如需更具體的錯誤訊息，請參閱回應內文（例如，訊息裝載遺失必要欄位，或訊息為未知xdm格式）。 |
| 401 | 未授權：請求缺少有效的授權標頭。 這只會針對已啟用驗證的入口傳回。 |
| 403 | 未授權：提供的授權Token無效或已過期。 這只會針對已啟用驗證的入口傳回。 |
| 413 | 裝載過大 — 當總裝載請求大於1MB時引發。 |
| 429 | 在指定的時段內請求太多。 |
| 500 | 處理裝載時出錯。 如需更具體的錯誤訊息，請參閱回應內文(例如，未指定訊息裝載結構，或不符合 [!DNL Platform])。 |
| 503 | 服務當前不可用。 客戶端應使用指數式回退策略至少重試3次。 |
