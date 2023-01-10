---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 實體（設定檔存取）API端點
type: Documentation
description: Adobe Experience Platform可讓您使用RESTful API或使用者介面來存取即時客戶設定檔資料。 本指南概述如何使用設定檔API存取實體（通常稱為「設定檔」）。
exl-id: 06a1a920-4dc4-4468-ac15-bf4a6dc885d4
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1732'
ht-degree: 1%

---

# 實體端點（設定檔存取）

Adobe Experience Platform可讓您存取 [!DNL Real-Time Customer Profile] 使用RESTful API或使用者介面的資料。 本指南概述如何使用API存取實體（通常稱為「設定檔」）。 如需使用存取設定檔的詳細資訊，請參閱 [!DNL Platform] UI，請參閱 [設定檔使用手冊](../ui/user-guide.md).

## 快速入門

本指南中使用的API端點屬於 [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en). 繼續之前，請檢閱 [快速入門手冊](getting-started.md) 如需相關檔案的連結、閱讀本檔案中範例API呼叫的指南，以及成功呼叫任何呼叫所需的必要標題的重要資訊 [!DNL Experience Platform] API。

## 依身分存取設定檔資料

您可以存取 [!DNL Profile] 實體，方法是向 `/access/entities` 端點，並將實體的身份作為一系列查詢參數提供。 此身分包含ID值(`entityId`)和身分命名空間(`entityIdNS`)。

請求路徑中提供的查詢參數會指定要存取的資料。 您可以包含多個參數，以&amp;符號分隔。 有效參數的完整清單位於 [查詢參數](#query-parameters) 附錄一節。

**API格式**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**要求**

下列請求會使用身分擷取客戶的電子郵件和名稱：

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

```json
{
    "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA": {
        "entityId": "BVrqzwVv7o2p3naHvnsWpqZXv3KJgA",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    }
}
```

>[!NOTE]
>
>如果相關圖表連結超過50個身分，此服務會傳回HTTP狀態422，並傳回「太多相關身分」訊息。 如果您收到此錯誤，請考慮新增更多查詢參數以縮小搜尋範圍。

## 依身分清單存取設定檔資料

您可以透過多個設定檔實體的身分，向 `/access/entities` 端點，並在裝載中提供身分。 這些身分包含ID值(`entityId`)和身分識別命名空間(`entityIdNS`)。

**API格式**

```http
POST /access/entities
```

**要求**

下列請求會依身分清單擷取數個客戶的名稱和電子郵件地址：

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.profile"
        },
        "fields":[
            "identities",
            "person.name",
            "workEmail"
        ],
        "identities":[
            {
                "entityId":"89149270342662559642753730269986316601",
                "entityIdNS":{
                    "code":"ECID"
                }
            },
            {
                "entityId":"89149270342662559642753730269986316900",
                "entityIdNS":{
                    "code":"ECID"
                }
            },
            {
                "entityId":"89149270342662559642753730269986316602",
                "entityIdNS":{
                    "code":"ECID"
                }
            }
        ],
        "timeFilter": {
            "startTime": 1539838505,
            "endTime": 1539838510
        },
        "limit": 10,
        "orderby": "-timestamp",
        "withCA": true
      }'
```

| 屬性 | 說明 |
|---|---|
| `schema.name` | ***（必要）*** 實體所屬的XDM架構名稱。 |
| `fields` | 要傳回的XDM欄位，為字串的陣列。 依預設，會傳回所有欄位。 |
| `identities` | ***（必要）*** 一個陣列，包含您要存取之實體的身分清單。 |
| `identities.entityId` | 您要存取之實體的ID。 |
| `identities.entityIdNS.code` | 您要存取的實體ID的命名空間。 |
| `timeFilter.startTime` | 包含的時間範圍篩選器的開始時間。 精細度應為毫秒。 預設值（若未指定）是可用時間的開始。 |
| `timeFilter.endTime` | 時間範圍篩選器的結束時間，已排除。 精細度應為毫秒。 如果未指定，預設值為可用時間的結尾。 |
| `limit` | 要返回的記錄數。 僅適用於傳回的體驗事件數。 預設值：1000。 |
| `orderby` | 依時間戳記擷取的體驗事件的排序順序，寫為 `(+/-)timestamp` 預設為 `+timestamp`. |
| `withCA` | 用於啟用計算屬性以供查找的功能標誌。 預設值：false。 |

**回應**
成功的回應會傳回要求內文中指定之實體的要求欄位。

```json
{
    "A29cgveD5y64ezlhxjUXNzcm": {
        "entityId": "A29cgveD5y64ezlhxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316601",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "05DD23564EC4607F0A490D44",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316603",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "janesmith@example.com",
                    "namespace": {
                        "code": "email"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316604",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316700",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316701",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "58832431024964181144308914570411162539",
                    "namespace": {
                        "code": "ecid"
                    }
                },
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-28T20:57:24Z"
    },
    "A29cgveD5y64e2RixjUXNzcm": {
        "entityId": "A29cgveD5y64e2RixjUXNzcm",
        "sources": [
            ""
        ],
        "entity": {},
        "lastModifiedAt": "1970-01-01T00:00:00Z"
    },
    "A29cgveD5y64ezphxjUXNzcm": {
        "entityId": "A29cgveD5y64ezphxjUXNzcm",
        "sources": [
            "1000000000"
        ],
        "entity": {
            "identities": [
                {
                    "id": "89149270342662559642753730269986316602",
                    "namespace": {
                        "code": "ecid"
                    },
                    "primary": true
                },
                {
                    "id": "janedoe@example.com",
                    "namespace": {
                        "code": "email"
                    }
                }
            ],
            "person": {
                "name": {
                    "firstName": "Jane",
                    "middleName": "F",
                    "lastName": "Doe"
                }
            },
            "workEmail": {
                "primary": true,
                "address": "janedoe@example.com",
                "label": "Jane Doe",
                "type": "work",
                "status": "active"
            }
        },
        "lastModifiedAt": "2018-08-27T23:25:52Z"
    }
}
```

## 依身分存取設定檔的時間序列事件

您可以透過對 `/access/entities` 端點。 此身分包含ID值(`entityId`)和身分識別命名空間(`entityIdNS`)。

請求路徑中提供的查詢參數會指定要存取的資料。 您可以包含多個參數，以&amp;符號分隔。 有效參數的完整清單位於 [查詢參數](#query-parameters) 附錄一節。

**API格式**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**要求**

下列請求會依ID尋找設定檔實體，並擷取屬性的值 `endUserIDs`, `web`，和 `channel` 用於與實體相關聯的所有時間序列事件。

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回在請求查詢參數中指定之時間序列事件和相關欄位的編頁清單。

>[!NOTE]
>
>請求指定的限制為(`limit=1`)，因此 `count` 在以下回應中為1，只會傳回一個實體。

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236036",
        "count": 1,
        "next": "c8d11988-6b56-4571-a123-b6ce74236037"
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236036",
            "timestamp": 1531260476000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:49:02Z"
        }
    ],
    "_links": {
        "next": {
            "href": "/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1"
        }
    }
}
```

### 存取後續的結果頁面

擷取時間序列事件時，會對結果進行編頁。 如果有後續的結果頁面，則 `_page.next` 屬性將包含ID。 此外， `_links.next.href` 屬性提供用於檢索下一頁的請求URI。 若要擷取結果，請向 `/access/entities` 不過，您必須確實取代端點 `/entities` 和提供的URI的值。

>[!NOTE]
>
>請務必注意，您不會意外重複 `/entities/` 在請求路徑中。 它只會出現一次， `/access/entities?start=...`

**API格式**

```http
GET /access/{NEXT_URI}
```

| 參數 | 說明 |
|---|---|
| `{NEXT_URI}` | 從 `_links.next.href`. |

**要求**

下列請求會使用 `_links.next.href` URI作為請求路徑。

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回結果的下一頁。 此回應沒有後續的結果頁面，如 `_page.next` 和 `_links.next.href`.

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "c8d11988-6b56-4571-a123-b6ce74236037",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "A29cgveD5y64e2RixjUXNzcm",
            "entityId": "c8d11988-6b56-4571-a123-b6ce74236037",
            "timestamp": 1531260477000,
            "entity": {
                "endUserIDs": {
                    "_experience": {
                        "ecid": {
                            "id": "89149270342662559642753730269986316900",
                            "namespace": {
                                "code": "ecid"
                            }
                        }
                    }
                },
                "channel": {
                    "_type": "web"
                },
                "web": {
                    "webPageDetails": {
                        "name": "Fernie Snow",
                        "pageViews": {
                            "value": 1
                        }
                    }
                }
            },
            "lastModifiedAt": "2018-08-21T06:50:01Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

## 依身分存取多個設定檔的時間序列事件

您可以向發出POST請求，從多個關聯的設定檔存取時間序列事件 `/access/entities` 端點，並在裝載中提供設定檔身分識別。 這些身分每個都包含ID值(`entityId`)和身分識別命名空間(`entityIdNS`)。

**API格式**

```http
POST /access/entities
```

**要求**

下列要求會擷取與設定檔身分清單相關聯的時間系列事件的使用者ID、當地時間和國家/地區代碼：

```shell
curl -X POST \
  https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
    "schema": {
        "name": "_xdm.context.experienceevent"
    },
    "relatedSchema": {
        "name": "_xdm.context.profile"
    },
    "identities": [
        {
            "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW"
        }
        {
            "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY"
        }
    ],
    "fields": [
        "endUserIDs",
        "placeContext.localTime",
        "placeContext.geo.countryCode"
    ],
    
    "timeFilter": {
        "startTime": 11539838505
        "endTime": 1539838510
    },
    "limit": 10
}'
```

| 屬性 | 說明 |
|---|---|
| `schema.name` | **（必要）** 要擷取之實體的XDM架構 |
| `relatedSchema.name` | 若 `schema.name` is `_xdm.context.experienceevent` 此值必須指定與時間序列事件相關的配置檔案實體的架構。 |
| `identities` | **（必要）** 要從中檢索關聯時間序列事件的配置檔案的陣列清單。 陣列中的每個項目以兩種方式之一設定：1)使用由ID值和命名空間組成的完全合格身分識別，或2)提供XID。 |
| `fields` | 將傳回的資料隔離至指定的欄位集。 使用此欄位可篩選擷取的資料中包含哪些結構欄位。 範例：personalEmail,person.name,person.gender |
| `mergePolicyId` | 標識用於管理返回資料的合併策略。 如果未在服務呼叫中指定，則會使用貴組織的該架構預設值。 如果尚未設定預設的合併原則，則預設為不合併設定檔，也不匯整身分。 |
| `orderby` | 依時間戳記擷取的體驗事件的排序順序，寫為 `(+/-)timestamp` 預設為 `+timestamp`. |
| `timeFilter.startTime` | 指定篩選時間序列對象的開始時間（以毫秒為單位）。 |
| `timeFilter.endTime` | 指定篩選時間序列對象的結束時間（以毫秒為單位）。 |
| `limit` | 指定要返回的最大對象數的數值。 預設值：1000 |
| `withCA` | 用於啟用計算屬性以供查找的功能標誌。 預設值：false |

**回應**

成功的回應會傳回與請求中指定的多個設定檔相關聯的編頁時間序列事件清單。

```json
{
    "GkouAW-yD9aoRCPhRYROJ-TetAFW": {
        "_page": {
            "orderby": "timestamp",
            "start": "ee0fa8eb-f09c-4d72-a432-fea7f189cfcd",
            "count": 10,
            "next": "40cb2fb3-78cd-49d3-806f-9bdb22748226"
        },
        "children": [
            {
                "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                "entityId": "ee0fa8eb-f09c-4d72-a432-fea7f189cfcd",
                "timestamp": 1537275882000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "67971860962043911970658021809222795905",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "50353446361742744826197433431642033796",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a00003314-2fd9c00000000026",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-18T13:04:42Z",
                        "geo": {
                            "countryCode": "MX"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:35:01Z"
            },
            {
                "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                "entityId": "a9e137b4-1348-4878-8167-e308af523d8b",
                "timestamp": 1537275889000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "67971860962043911970658021809222795905",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "50353446361742744826197433431642033796",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a00003314-2fd9c00000000026",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-18T13:04:49Z",
                        "geo": {
                            "countryCode": "MX"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:35:01Z"
            }
        ],
        "_links": {
            "next": {
                "href": "/entities",
                "payload": {
                    "schema": {
                        "name": "_xdm.context.experienceevent"
                    },
                    "relatedSchema": {
                        "name": "_xdm.context.profile"
                    },
                    "timeFilter": {
                        "startTime": 1537275882000
                    },
                    "fields": [
                        "endUserIDs",
                        "placeContext.localTime",
                        "placeContext.geo.countryCode"
                    ],
                    "identities": [
                        {
                            "relatedEntityId": "GkouAW-yD9aoRCPhRYROJ-TetAFW",
                            "start": "40cb2fb3-78cd-49d3-806f-9bdb22748226"
                        }
                    ],
                    "limit": 10
                }
            }
        }
    },
    "GkouAW-2u-7iWt5vQ9u2wm40JOZY": {
        "_page": {
            "orderby": "timestamp",
            "start": "2746d0db-fa64-4e29-b67e-324bec638816",
            "count": 9,
            "next": ""
        },
        "children": [
            {
                "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY",
                "entityId": "2746d0db-fa64-4e29-b67e-324bec638816",
                "timestamp": 1537559483000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "76436745599328540420034822220063618863",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "48593470048917738786405847327596263131",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a80007451-03da600000000028",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-21T19:51:23Z",
                        "geo": {
                            "countryCode": "US"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:34:58Z"
            },
            {
                "relatedEntityId": "GkouAW-2u-7iWt5vQ9u2wm40JOZY",
                "entityId": "9bf337a1-3256-431e-a38c-5c0d42d121d1",
                "timestamp": 1537559486000,
                "entity": {
                    "endUserIDs": {
                        "_experience": {
                            "mcid": {
                                "id": "76436745599328540420034822220063618863",
                                "namespace": {
                                    "code": "ECID"
                                }
                            },
                            "aacustomid": {
                                "id": "48593470048917738786405847327596263131",
                                "namespace": {
                                    "code": "CRMID"
                                },
                                "primary": true
                            },
                            "acid": {
                                "id": "2de32e9a80007451-03da600000000028",
                                "namespace": {
                                    "code": "AVID"
                                }
                            }
                        }
                    },
                    "placeContext": {
                        "localTime": "2018-09-21T19:51:26Z",
                        "geo": {
                            "countryCode": "US"
                        }
                    }
                },
                "lastModifiedAt": "2018-10-24T17:34:58Z"
            }
        ],
        "_links": {
            "next": {
                "href": ""
            }
        }
    }
}`
```

在此範例回應中，第一個列出的設定檔(「GkouAW-yD9aoRCPhRYROJ-TetAFW」)提供的值 `_links.next.payload`，表示此設定檔有其他的結果頁面。 請參閱下節，內容如下： [訪問其他結果](#access-additional-results) 以了解如何存取這些額外結果的詳細資訊。

### 訪問其他結果 {#access-additional-results}

擷取時間序列事件時，可能會傳回許多結果，因此，結果通常會採用編頁方式。 如果特定設定檔有後續的結果頁面，則 `_links.next.payload` 該設定檔的值將包含裝載物件。

在要求內文中使用此裝載，您可以對 `access/entities` 端點來擷取該設定檔的後續時間序列資料頁面。

## 訪問多個架構實體中的時間序列事件

您可以訪問通過關係描述符連接的多個實體。 下列範例API呼叫假設已定義兩個結構之間的關係。 有關關係描述符的詳細資訊，請閱讀 [!DNL Schema Registry] API開發人員指南 [descriptors endpoint worke](../../xdm/api/descriptors.md).

您可以在請求路徑中加入查詢參數，以指定要存取的資料。 您可以包含多個參數，以&amp;符號分隔。 有效參數的完整清單位於 [查詢參數](#query-parameters) 附錄一節。

**API格式**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**要求**

以下請求將檢索包含先前建立的關係描述符的實體，以訪問不同架構中的資訊。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/access/entities?relatedSchema.name=_xdm.context.profile&schema.name=_xdm.context.experienceevent&relatedEntityId=GkouAW-2Xkftzer3bBtHiW8GkaFL \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**回應**

成功的回應會傳回與多個實體相關聯的時間序列事件編頁清單。

```json
{
    "_page": {
        "orderby": "timestamp",
        "start": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
        "count": 1,
        "next": ""
    },
    "children": [
        {
            "relatedEntityId": "GkouAW-2Xkftzer3bBtHiW8GkaFL",
            "entityId": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
            "timestamp": 1564614939000,
            "entity": {
                "environment": {
                    "browserDetails": {}
                },
                "identityMap": {
                    "CRMId": [
                        {
                            "id": "78520026455138218785449796480922109723",
                            "primary": true
                        }
                    ]
                },

                "commerce": {
                    "productViews": {
                        "value": 1
                    }
                },
                "productListItems": [
                    {
                        "name": "Red shoe",
                        "quantity": 85,
                        "storesAvailableIn": [
                            "da6dced5-9574-4dda-89b5-9dc106903f80",
                            "981bb433-2ee5-4db0-a19a-449ec9dbf39f"
                        ],
                        "SKU": "8f998279-797b-4da2-9e60-88bf73a9f15a",
                        "priceTotal": 934.8
                    }
                ],
                "_id": "cb10369f-a47b-4e65-afb4-06e1ad78a648",
                "commerce": {
                    "order": {}
                },
                "placeContext": {
                    "geo": {
                        "_schema": {}
                    }
                },
                "device": {},
                "timestamp": "2019-07-31T23:15:39Z",
                "_experience": {
                    "profile": {
                        "identityNamespaces": {
                            "/productListItems[*]/SKU": {
                                "namespace": {
                                    "code": "ECID"
                                }
                            }
                        }
                    }
                }
            },
            "lastModifiedAt": "2019-10-10T00:14:19Z"
        }
    ],
    "_links": {
        "next": {
            "href": ""
        }
    }
}
```

### 存取後續的結果頁面

擷取時間序列事件時，會對結果進行編頁。 如果有後續的結果頁面，則 `_page.next` 屬性將包含ID。 此外， `_links.next.href` 屬性提供請求URI，用於通過向 `access/entities` 端點。

## 後續步驟

依照本指南，您已成功存取 [!DNL Real-Time Customer Profile] 資料欄位、設定檔及時間系列資料。 了解如何存取儲存在 [!DNL Platform]，請參閱 [資料存取概觀](../../data-access/home.md).

## 附錄 {#appendix}

下節提供有關訪問的補充資訊 [!DNL Profile] 資料。

### 查詢參數 {#query-parameters}

路徑中會使用下列參數，以GET `/access/entities` 端點。 它們可用來識別您要存取的設定檔實體，並篩選回應中傳回的資料。 標示必要參數，其餘為選用。

| 參數 | 說明 | 範例 |
|---|---|---|
| `schema.name` | **（必要）** 要擷取之實體的XDM架構 | `schema.name=_xdm.context.experienceevent` |
| `relatedSchema.name` | 若 `schema.name` 為「_xdm.context.experienceevent」，此值必須指定與時間系列事件相關的設定檔實體的結構。 | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **（必要）** 實體的ID。 如果此參數的值不是XID，則還必須提供身分命名空間參數(請參閱 `entityIdNS` )。 | `entityId=janedoe@example.com` |
| `entityIdNS` | 若 `entityId` 未以XID形式提供，此欄位必須指定身分命名空間。 | `entityIdNE=email` |
| `relatedEntityId` | 若 `schema.name` 為「_xdm.context.experienceevent」，此值必須指定相關設定檔實體的身分命名空間。 此值遵循與 `entityId`. | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | 若 `schema.name` 為「_xdm.context.experienceevent」，此值必須為中指定的實體指定身分命名空間 `relatedEntityId`. | `relatedEntityIdNS=CRMID` |
| `fields` | 篩選回應中傳回的資料。 使用此欄位可指定要在擷取的資料中納入的架構欄位值。 若是多個欄位，請以逗號分隔值，其間不含空格 | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | 標識用於管理返回資料的合併策略。 如果未在呼叫中指定，則會使用貴組織的該架構預設值。 如果尚未設定預設的合併原則，則預設為不合併設定檔，也不匯整身分。 | `mergePoilcyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | 依時間戳記擷取的體驗事件的排序順序，寫為 `(+/-)timestamp` 預設為 `+timestamp`. | `orderby=-timestamp` |
| `startTime` | 指定篩選時間序列對象的開始時間（以毫秒為單位）。 | `startTime=1539838505` |
| `endTime` | 指定篩選時間序列對象的結束時間（以毫秒為單位）。 | `endTime=1539838510` |
| `limit` | 指定要返回的最大對象數的數值。 預設值：1000 | `limit=100` |
| `property` | 依屬性值篩選。 支援下列評估工具：=, !=, &lt;, &lt;=, >, >=。 只能與體驗事件搭配使用，最多支援三個屬性。 | `property=webPageDetails.isHomepage=true&property=localTime<="2020-07-20"` |
| `withCA` | 用於啟用計算屬性以供查找的功能標誌。 預設值：false | `withCA=true` |
