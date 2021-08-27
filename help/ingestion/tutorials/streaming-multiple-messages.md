---
keywords: Experience Platform；首頁；熱門主題；串流內嵌；內嵌；串流多則訊息；多則訊息；
solution: Experience Platform
title: 在單一HTTP要求中傳送多則訊息
topic-legacy: tutorial
type: Tutorial
description: 本檔案提供教學課程，說明如何使用串流內嵌，在單一HTTP要求內傳送多則訊息至Adobe Experience Platform。
exl-id: 04045090-8a2c-42b6-aefa-09c043ee414f
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
workflow-type: tm+mt
source-wordcount: '1493'
ht-degree: 1%

---

# 在單一HTTP要求中傳送多則訊息

將資料串流至Adobe Experience Platform時，進行大量HTTP呼叫可能會相當昂貴。 例如，建立1個HTTP要求（每封200則訊息為1KB），而不是使用1KB裝載來建立200個HTTP要求，效率會高很多，而且單一裝載為200KB。 正確使用時，在單一請求中分組多個訊息是最佳化傳送至[!DNL Experience Platform]之資料的絕佳方式。

本檔案提供教學課程，說明如何使用串流內嵌，在單一HTTP要求內傳送多個訊息至[!DNL Experience Platform]。

## 快速入門

本教學課程需要妥善了解Adobe Experience Platform [!DNL Data Ingestion]。 開始本教學課程之前，請檢閱下列檔案：

- [資料擷取概觀](../home.md):涵蓋的核心概 [!DNL Experience Platform Data Ingestion]念，包括擷取方法和Data Connector。
- [串流獲取概觀](../streaming-ingestion/overview.md):串流獲取的工作流程和建置區塊，例如串流連線、資料 [!DNL XDM Individual Profile]集和 [!DNL XDM ExperienceEvent]。

此外，本教學課程還需要您完成[驗證Adobe Experience Platform](https://www.adobe.com/go/platform-api-authentication-en)教學課程，才能成功呼叫[!DNL Platform] API。 完成驗證教學課程，提供本教學課程中所有API呼叫所需的Authorization標題值。 標題在範例呼叫中顯示，如下所示：

- 授權：承載`{ACCESS_TOKEN}`

所有POST請求都需要額外的標題：

- 內容類型：application/json

## 建立串流連線

您必須先建立串流連線，才能開始將資料串流至[!DNL Experience Platform]。 請參閱[建立串流連線](./create-streaming-connection.md)指南，了解如何建立串流連線。

註冊串流連線後，您（身為資料製作者）會有一個唯一URL，可用來將資料串流至Platform。

## 串流至資料集

下列範例說明如何在單一HTTP要求內傳送多則訊息至特定資料集。 在訊息標題中插入資料集ID，直接內嵌該訊息。

您可以使用[!DNL Platform] UI或在API中使用清單操作來取得現有資料集的ID。 前往&#x200B;**[!UICONTROL 資料集]**&#x200B;標籤，按一下您要用於的資料集，然後從&#x200B;**[!UICONTROL Info]**&#x200B;標籤上的資料集ID欄位複製字串，即可在[Experience Platform](https://platform.adobe.com)上找到資料集ID。 如需如何使用API擷取資料集的相關資訊，請參閱[目錄服務概述](../../catalog/home.md) 。

您可以建立新資料集，而不使用現有資料集。 請參閱[使用API建立資料集](../../catalog/api/create-dataset.md)教學課程，以取得有關使用API建立資料集的詳細資訊。

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

有關狀態代碼的詳細資訊，請參閱本教學課程附錄中的[回應代碼](#response-codes)表。

## 識別失敗的消息

與使用單一訊息傳送請求相比，在使用多個訊息傳送HTTP請求時，需考慮其他因素，例如：如何識別資料無法傳送的時間、無法傳送哪些特定訊息以及如何擷取訊息，以及相同請求中的其他訊息失敗時成功的資料會發生什麼事。

繼續本教程之前，建議先查看[檢索失敗批次](../quality/retrieve-failed-batches.md)指南。

### 傳送含有有效和無效訊息的要求裝載

以下示例說明了當批包含有效和無效消息時會發生什麼情況。

要求裝載是JSON物件的陣列，代表XDM結構中的事件。 請注意，若要成功驗證訊息，必須符合下列條件：
- 消息標題中的`imsOrgId`欄位必須與入口定義匹配。 如果要求裝載未包含`imsOrgId`欄位， [!DNL Data Collection Core Service](DCCS)會自動新增欄位。
- 訊息的標題應參考在[!DNL Platform] UI中建立的現有XDM架構。
- `datasetId`欄位需要參考[!DNL Platform]中的現有資料集，其架構需要符合要求內文所含每則訊息中`header`物件中提供的架構。

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

回應裝載包含每則訊息的狀態，以及`xactionId`中可用於追蹤的GUID。

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

上述範例回應顯示先前請求的錯誤訊息。 將此回應與先前的有效回應進行比較，您可以發現要求導致部分成功，其中一則訊息成功擷取，三則訊息導致失敗。 請注意，兩個回應都會傳回「207」狀態代碼。 有關狀態代碼的詳細資訊，請參閱本教學課程附錄中的[回應代碼](#response-codes)表。

第一條消息已成功發送到[!DNL Platform]，並且不受其他消息的結果的影響。 因此，在嘗試重新發送失敗的消息時，不需要重新包含此消息。

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

第三則訊息失敗，因為標題中使用的IMS組織ID無效。 IMS組織必須符合您嘗試張貼到的{CONNECTION_ID}。 若要判斷哪個IMS組織ID符合您使用的串流連線，您可以使用[[!DNL Data Ingestion API]](https://www.adobe.io/experience-platform-apis/references/data-ingestion/)執行`GET inlet`請求。 如需如何擷取先前建立的串流連線的範例，請參閱[擷取串流連線](./create-streaming-connection.md#get-data-collection-url)。

第四則訊息失敗，因為未遵循預期的XDM架構。 請求的標題和正文中包含的`xdmSchema`不符合`{DATASET_ID}`的XDM架構。 更正消息標頭和正文中的架構，使其能夠通過DCCS驗證並成功發送到[!DNL Platform]。 還必須更新訊息內文，以符合`{DATASET_ID}`的XDM架構，該架構才能在[!DNL Platform]上通過串流驗證。 如需成功串流至Platform之訊息有何變化的詳細資訊，請參閱本教學課程的[確認已內嵌的訊息](#confirm-messages-ingested)一節。

### 從[!DNL Platform]檢索失敗消息

失敗的消息由響應陣列中的錯誤狀態代碼標識。
無效消息將在`{DATASET_ID}`指定的資料集內以「error」批次收集並儲存。

有關恢復失敗批消息的詳細資訊，請參閱[檢索失敗批](../quality/retrieve-failed-batches.md)指南。

## 確認已擷取的訊息

通過DCCS驗證的消息流式化到[!DNL Platform]。 在[!DNL Platform]上，在將批次訊息擷取到[!DNL Data Lake]之前，會先透過串流驗證來測試。 批次狀態（無論是否成功）會顯示在`{DATASET_ID}`所指定的資料集中。

您可以前往&#x200B;**[!UICONTROL 資料集]**&#x200B;標籤，按一下要串流到的資料集，然後勾選&#x200B;**[!UICONTROL 資料集活動]**&#x200B;標籤，檢視使用[Experience PlatformUI](https://platform.adobe.com)成功串流到[!DNL Platform]的批次訊息狀態。

在[!DNL Platform]上通過串流驗證的批次訊息會內嵌至[!DNL Data Lake]。 然後，這些訊息便可供分析或匯出。

## 後續步驟

現在您知道如何在單一請求中傳送多則訊息，以及確認訊息是否成功內嵌至目標資料集，可以開始將您的資料串流至[!DNL Platform]。 如需如何從[!DNL Platform]查詢和擷取擷取擷取資料的概觀，請參閱[[!DNL Data Access]](../../data-access/tutorials/dataset-data.md)指南。

## 附錄

本節包含教學課程的補充資訊。

### 回應代碼

下表顯示成功和失敗響應消息返回的狀態代碼。

| 狀態代碼 | 說明 |
| :---: | --- |
| 207 | 雖然將「207」用作整體響應狀態代碼，但接收者需要查閱多狀態響應主體的內容，以獲得有關方法執行的成功或失敗的進一步資訊。 回應程式碼用於成功、部分成功，以及失敗情況。 |
| 400 | 請求有問題。 如需更具體的錯誤訊息，請參閱回應內文（例如，訊息裝載遺失必要欄位，或訊息為未知xdm格式）。 |
| 401 | 未授權：請求缺少有效的授權標頭。 這只會針對已啟用驗證的入口傳回。 |
| 403 | 未授權： 提供的授權Token無效或已過期。 這只會針對已啟用驗證的入口傳回。 |
| 413 | 裝載過大 — 當總裝載請求大於1MB時引發。 |
| 429 | 在指定的時段內請求太多。 |
| 500 | 處理裝載時出錯。 請參閱回應內文，以了解更具體的錯誤訊息（例如，未指定訊息裝載架構，或不符合[!DNL Platform]中的XDM定義）。 |
| 503 | 服務當前不可用。 客戶端應使用指數式回退策略至少重試3次。 |
