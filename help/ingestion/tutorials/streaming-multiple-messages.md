---
keywords: Experience Platform；首頁；熱門主題；串流擷取；擷取；串流多則訊息；多則訊息；
solution: Experience Platform
title: 在單一HTTP要求中傳送多則訊息
type: Tutorial
description: 本檔案提供的教學課程，說明如何使用串流擷取，在單一HTTP請求中傳送多則訊息至Adobe Experience Platform。
exl-id: 04045090-8a2c-42b6-aefa-09c043ee414f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1489'
ht-degree: 1%

---

# 在單一HTTP要求中傳送多則訊息

將資料串流至Adobe Experience Platform時，進行大量HTTP呼叫可能會很昂貴。 舉例來說，比起以1KB裝載建立200個HTTP要求，建立1個HTTP要求（每個要求200個訊息1KB）與200個單一裝載200KB要有效得多。 若正確使用，在單一要求中將多個訊息分組，是最佳化傳送至[!DNL Experience Platform]之資料的絕佳方式。

本檔案提供的教學課程可讓您使用串流擷取，在單一HTTP要求中將多則訊息傳送至[!DNL Experience Platform]。

## 快速入門

此教學課程需要實際瞭解Adobe Experience Platform [!DNL Data Ingestion]。 在開始本教學課程之前，請先檢閱下列檔案：

- [資料擷取概觀](../home.md)：涵蓋[!DNL Experience Platform Data Ingestion]的核心概念，包括擷取方法和資料聯結器。
- [串流擷取總覽](../streaming-ingestion/overview.md)：串流擷取的工作流程和建置區塊，例如串流連線、資料集、[!DNL XDM Individual Profile]和[!DNL XDM ExperienceEvent]。

此教學課程也要求您完成[Adobe Experience Platform驗證](https://www.adobe.com/go/platform-api-authentication-en)教學課程，才能成功呼叫[!DNL Experience Platform] API。 完成驗證教學課程，在本教學課程中提供所有API呼叫所需的Authorization標頭值。 標頭會顯示在範例呼叫中，如下所示：

- 授權：持有人`{ACCESS_TOKEN}`

所有POST請求都需要額外的標頭：

- Content-Type： application/json

## 建立串流連線

您必須先建立串流連線，才能開始將資料串流至[!DNL Experience Platform]。 閱讀[建立串流連線](./create-streaming-connection.md)指南，瞭解如何建立串流連線。

註冊串流連線後，身為資料製作者，您將擁有唯一URL，可用將資料串流至Experience Platform。

## 串流至資料集

以下範例說明如何在單一HTTP請求中，將多則訊息傳送至特定資料集。 在訊息標題中插入資料集ID，讓該訊息直接內嵌到其中。

您可以使用[!DNL Experience Platform] UI或API中的清單操作，取得現有資料集的識別碼。 您可以在[Experience Platform](https://platform.adobe.com)上找到資料集ID，方法是前往&#x200B;**[!UICONTROL 資料集]**&#x200B;索引標籤，按一下您想要ID的資料集，然後從&#x200B;**[!UICONTROL 資訊]**&#x200B;索引標籤上的資料集ID欄位複製字串。 如需有關如何使用API擷取資料集的資訊，請參閱[目錄服務總覽](../../catalog/home.md)。

您可以建立新的資料集，而不使用現有的資料集。 如需使用API建立資料集的詳細資訊，請參閱[使用API建立資料集](../../catalog/api/create-dataset.md)教學課程。

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

成功的回應會傳回HTTP狀態207 （多狀態）。 檢閱回應內文，可提供請求中執行之每個方法成功或失敗的更多詳細資料。 系統會針對請求訊息陣列的每個元素傳回回應。 以下是成功回應且無訊息失敗的範例：

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

如需狀態碼的詳細資訊，請參閱本教學課程附錄中的[回應碼](#response-codes)表格。

## 識別失敗的訊息

相較於使用單一訊息傳送請求，在傳送包含多個訊息的HTTP請求時，還有其他因素需要考慮，例如：如何識別資料何時無法傳送、哪些特定訊息無法傳送以及如何可擷取這些訊息，以及當相同請求中的其他訊息失敗時，成功的資料會發生什麼情況。

在繼續本教學課程之前，建議您先檢閱[擷取失敗的批次](../quality/retrieve-failed-batches.md)指南。

### 傳送含有效及無效訊息的要求裝載

下列範例說明批次包含有效及無效訊息時發生的情況。

請求承載是代表XDM結構描述中事件的JSON物件陣列。 請注意，必須符合下列條件才能成功驗證訊息：
- 訊息標頭中的`imsOrgId`欄位必須符合入口定義。 如果要求裝載未包含`imsOrgId`欄位，[!DNL Data Collection Core Service] (DCCS)會自動新增欄位。
- 訊息的標頭應參考在[!DNL Experience Platform] UI中建立的現有XDM結構描述。
- `datasetId`欄位需要參考[!DNL Experience Platform]中的現有資料集，而且其結構描述需要符合要求內文中所包含每個訊息中`header`物件所提供的結構描述。

**API格式**

```http
POST /collection/batch/{CONNECTION_ID}
```

| 屬性 | 說明 |
| -------- | ----------- |
| `{CONNECTION_ID}` | 已建立資料入口的ID。 |

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

回應承載包含每個訊息的狀態，以及`xactionId`中可用於追蹤的GUID。

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

上述範例回應顯示前一個請求的錯誤訊息。 將此回應與先前的有效回應做比較，您會發現要求導致部分成功，其中一條訊息擷取成功，三則訊息導致失敗。 請注意，兩個回應都會傳回「207」狀態代碼。 如需狀態碼的詳細資訊，請參閱本教學課程附錄中的[回應碼](#response-codes)表格。

第一個訊息已成功傳送至[!DNL Experience Platform]，不受其他訊息結果的影響。 因此，當嘗試重新傳送失敗的訊息時，您不需要重新包含此訊息。

第二個訊息失敗，因為它缺少訊息本文。 集合要求要求訊息元素必須有有效的標頭與內文區段。 在第二則訊息的標頭之後新增下列程式碼將修正請求，並允許第二則訊息通過驗證：

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

第三個訊息因標頭中使用無效的組織ID而失敗。 組織必須符合您嘗試張貼到的{CONNECTION_ID}。 若要判斷哪一個組織識別碼符合您正在使用的串流連線，您可以使用[[!DNL Streaming Ingestion API]](https://developer.adobe.com/experience-platform-apis/references/streaming-ingestion/)執行`GET inlet`要求。 如需如何擷取先前建立的串流連線的範例，請參閱[擷取串流連線](./create-streaming-connection.md#get-data-collection-url)。

第四則訊息失敗，因為它未遵循預期的XDM結構描述。 要求標頭和內文中包含的`xdmSchema`不符合`{DATASET_ID}`的XDM結構描述。 更正訊息標頭與內文中的結構描述，可讓結構描述通過DCCS驗證，並成功傳送至[!DNL Experience Platform]。 訊息本文也必須更新以符合`{DATASET_ID}`的XDM結構描述，才能在[!DNL Experience Platform]上傳遞串流驗證。 如需有關成功串流至Experience Platform的訊息有何動作的詳細資訊，請參閱本教學課程的[確認已擷取的訊息](#confirm-messages-ingested)區段。

### 從[!DNL Experience Platform]擷取失敗的郵件

失敗的訊息會由回應陣列中的錯誤狀態碼來識別。
在`{DATASET_ID}`指定的資料集內，收集無效的訊息並儲存在「錯誤」批次中。

閱讀[擷取失敗的批次](../quality/retrieve-failed-batches.md)指南，以取得有關復原失敗的批次訊息的詳細資訊。

## 確認已擷取的訊息

通過DCCS驗證的訊息會串流至[!DNL Experience Platform]。 在[!DNL Experience Platform]，批次訊息在被擷取到[!DNL Data Lake]之前，會先透過串流驗證進行測試。 批次的狀態（無論是否成功）會顯示在`{DATASET_ID}`所指定的資料集中。

您可以使用[Experience Platform UI](https://platform.adobe.com)檢視成功串流至[!DNL Experience Platform]的批次訊息的狀態，方法是前往&#x200B;**[!UICONTROL 資料集]**&#x200B;標籤，按一下您要串流至的資料集，然後檢查&#x200B;**[!UICONTROL 資料集活動]**&#x200B;標籤。

在[!DNL Experience Platform]上通過串流驗證的批次訊息已擷取到[!DNL Data Lake]。 然後這些訊息便可用於分析或匯出。

## 後續步驟

現在您知道如何在單一要求中傳送多則訊息，並驗證訊息何時成功擷取至目標資料集，您就可以開始將自己的資料串流至[!DNL Experience Platform]。 如需如何從[!DNL Experience Platform]查詢及擷取內嵌資料的概觀，請參閱[[!DNL Data Access]](../../data-access/tutorials/dataset-data.md)指南。

## 附錄

本節包含教學課程的補充資訊。

### 回應代碼

下表顯示成功和失敗回應訊息傳回的狀態代碼。

| 狀態代碼 | 說明 |
| :---: | --- |
| 207 | 雖然將「207」用作整體回應狀態代碼，但收件者需要查閱多狀態回應主體的內容，以取得有關方法執行成功或失敗的進一步資訊。 回應程式碼會用於成功、部分成功及失敗情況。 |
| 400 | 請求發生問題。 如需更具體的錯誤訊息，請參閱回應內文（例如，訊息裝載缺少必填欄位，或訊息未知xdm格式）。 |
| 401 | 未獲授權：請求缺少有效的授權標頭。 系統只會對已啟用驗證的Inlet傳回此值。 |
| 403 | 未獲授權：提供的授權權杖無效或過期。 系統只會對已啟用驗證的Inlet傳回此值。 |
| 413 | 承載太大 — 當承載要求總數大於1MB時擲回。 |
| 429 | 指定期間內有太多要求。 |
| 500 | 處理裝載時發生錯誤。 檢視更具體的錯誤訊息的回應內文（例如，未指定訊息裝載結構描述，或不符合[!DNL Experience Platform]中的XDM定義）。 |
| 503 | 服務目前無法使用。 使用者端應使用指數回退策略重試至少3次。 |
