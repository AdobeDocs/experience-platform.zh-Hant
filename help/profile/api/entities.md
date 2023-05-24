---
keywords: Experience Platform；配置；即時客戶配置；故障排除；API
title: 實體（配置檔案訪問）API終結點
type: Documentation
description: Adobe Experience Platform使您能夠使用REST風格的API或用戶介面訪問即時客戶配置檔案資料。 本指南概述了如何使用配置檔案API訪問實體（通常稱為「配置檔案」）。
exl-id: 06a1a920-4dc4-4468-ac15-bf4a6dc885d4
source-git-commit: 0f7ef438db5e7141197fb860a5814883d31ca545
workflow-type: tm+mt
source-wordcount: '1732'
ht-degree: 1%

---

# 實體端點（配置檔案訪問）

Adobe Experience Platform允許您訪問 [!DNL Real-Time Customer Profile] 使用REST風格的API或用戶介面的資料。 本指南概述了如何使用API訪問實體（通常稱為「配置檔案」）。 有關使用訪問配置檔案的詳細資訊 [!DNL Platform] UI，請參閱 [配置檔案使用手冊](../ui/user-guide.md)。

## 快速入門

本指南中使用的API終結點是 [[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en)。 在繼續之前，請查看 [入門指南](getting-started.md) 有關指向相關文檔的連結、閱讀本文檔中示例API調用的指南，以及成功調用任何文檔所需的標題的重要資訊 [!DNL Experience Platform] API。

## 按身份訪問配置檔案資料

您可以訪問 [!DNL Profile] 實體，方法為向 `/access/entities` 將實體標識作為一系列查詢參數提供。 此標識由ID值(`entityId`)和標識命名空間(`entityIdNS`)。

請求路徑中提供的查詢參數指定要訪問的資料。 可以包括多個參數，以和符號(&amp;)分隔。 中提供了有效參數的完整清單 [查詢參數](#query-parameters) 的下界。

**API格式**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**要求**

以下請求使用標識檢索客戶的電子郵件和名稱：

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
>如果相關圖連結的標識數超過50個，則此服務將返回HTTP狀態422，並返回消息「相關標識太多」。 如果收到此錯誤，請考慮添加更多查詢參數以縮小搜索範圍。

## 按身份清單訪問配置檔案資料

您可以通過向以下對象發出POST請求來按其身份訪問多個配置檔案實體 `/access/entities` 並在負載中提供標識。 這些標識由ID值(`entityId`)和標識命名空間(`entityIdNS`)。

**API格式**

```http
POST /access/entities
```

**要求**

以下請求通過標識清單檢索多個客戶的名稱和電子郵件地址：

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
| `schema.name` | ***（必需）*** 實體所屬的XDM架構的名稱。 |
| `fields` | 要返回的XDM欄位，作為字串陣列。 預設情況下，將返回所有欄位。 |
| `identities` | ***（必需）*** 包含要訪問的實體標識清單的陣列。 |
| `identities.entityId` | 要訪問的實體的ID。 |
| `identities.entityIdNS.code` | 要訪問的實體ID的命名空間。 |
| `timeFilter.startTime` | 包括的時間範圍篩選器的開始時間。 應以毫秒的粒度。 如果未指定，則預設值是可用時間的開始。 |
| `timeFilter.endTime` | 排除的時間範圍篩選器的結束時間。 應以毫秒的粒度。 如果未指定，則預設值為可用時間的結束。 |
| `limit` | 要返回的記錄數。 僅適用於返回的體驗事件數。 預設值：1000。 |
| `orderby` | 按時間戳（寫入方式）檢索的體驗事件的排序順序 `(+/-)timestamp` 預設值為 `+timestamp`。 |
| `withCA` | 用於啟用計算屬性以進行查找的功能標誌。 預設值：錯誤。 |

**響應**
成功的響應返回請求正文中指定的實體的請求欄位。

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

## 按身份訪問配置檔案的時間系列事件

您可以通過向以下對象發出GET請求來按其關聯配置檔案實體的標識訪問時間系列事件 `/access/entities` 端點。 此標識由ID值(`entityId`)和標識命名空間(`entityIdNS`)。

請求路徑中提供的查詢參數指定要訪問的資料。 可以包括多個參數，以和符號(&amp;)分隔。 中提供了有效參數的完整清單 [查詢參數](#query-parameters) 的下界。

**API格式**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**要求**

以下請求按ID查找配置檔案實體，並檢索屬性的值 `endUserIDs`。 `web`, `channel` 與實體關聯的所有時間系列事件。

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回在請求查詢參數中指定的時間系列事件和關聯欄位的分頁清單。

>[!NOTE]
>
>請求指定了一個限制(`limit=1`)，因此 `count` 在下面的響應中為1，並且只返回一個實體。

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

### 訪問後續結果頁

檢索時間系列事件時，將對結果進行分頁。 如果有後續頁面的結果， `_page.next` 屬性將包含ID。 此外， `_links.next.href` 屬性提供用於檢索下一頁的請求URI。 要檢索結果，請向 `/access/entities` 但是，必須確保替換 `/entities` 提供的URI的值。

>[!NOTE]
>
>確保你不會不小心重複 `/entities/` 的子菜單。 它應該只出現一次， `/access/entities?start=...`

**API格式**

```http
GET /access/{NEXT_URI}
```

| 參數 | 說明 |
|---|---|
| `{NEXT_URI}` | 取自的URI值 `_links.next.href`。 |

**要求**

以下請求使用 `_links.next.href` URI作為請求路徑。

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應將返回結果的下一頁。 此響應沒有後續的結果頁，如空字串值所示 `_page.next` 和 `_links.next.href`。

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

## 按身份訪問多個配置檔案的時間系列事件

您可以通過向以下站點發出POST請求，從多個關聯配置檔案訪問時間系列事件 `/access/entities` 在負載中提供配置檔案標識。 這些標識每個都由ID值(`entityId`)和標識命名空間(`entityIdNS`)。

**API格式**

```http
POST /access/entities
```

**要求**

以下請求檢索與配置檔案標識清單關聯的時間系列事件的用戶ID、本地時間和國家代碼：

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
| `schema.name` | **（必需）** 要檢索的實體的XDM架構 |
| `relatedSchema.name` | 如果 `schema.name` 是 `_xdm.context.experienceevent` 此值必須指定與時間系列事件相關的配置檔案實體的架構。 |
| `identities` | **（必需）** 要從中檢索關聯時間序列事件的配置檔案的陣列清單。 陣列中的每個條目都通過以下兩種方式之一進行設定：1)使用由ID值和命名空間組成的完全限定的標識，或2)提供XID。 |
| `fields` | 將返回的資料隔離到指定的一組欄位。 使用此選項可篩選檢索到的資料中包含的架構欄位。 示例：personalEmail,person.name,person.gedem |
| `mergePolicyId` | 標識用於管理返回資料的合併策略。 如果未在服務呼叫中指定，則將使用組織對該架構的預設設定。 如果尚未配置預設合併策略，則預設為無配置檔案合併和無標識拼接。 |
| `orderby` | 按時間戳（寫入方式）檢索的體驗事件的排序順序 `(+/-)timestamp` 預設值為 `+timestamp`。 |
| `timeFilter.startTime` | 指定篩選時間序列對象的開始時間（以毫秒為單位）。 |
| `timeFilter.endTime` | 指定篩選時間序列對象的結束時間（以毫秒為單位）。 |
| `limit` | 指定要返回的最大對象數的數值。 預設值：1000 |
| `withCA` | 用於啟用計算屬性以進行查找的功能標誌。 預設值：假 |

**回應**

成功的響應返回與請求中指定的多個配置檔案相關聯的分頁時間系列事件清單。

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

在本示例響應中，第一個列出的配置檔案(「GkouAW-yD9aoRCPhRYROJ-TetAFW」)為 `_links.next.payload`，表示此配置檔案有其他結果頁。 請參閱以下關於 [訪問其他結果](#access-additional-results) 獲取有關如何訪問這些附加結果的詳細資訊。

### 訪問其他結果 {#access-additional-results}

檢索時間序列事件時，可能會返回許多結果，因此結果通常被分頁。 如果某個配置檔案有後續的結果頁， `_links.next.payload` 該配置檔案的值將包含負載對象。

使用請求正文中的此負載，您可以對 `access/entities` 終結點，以檢索該配置檔案的時間序列資料的後續頁。

## 訪問多個架構實體中的時間序列事件

您可以訪問通過關係描述符連接的多個實體。 以下示例API調用假定在兩個架構之間已定義了關係。 有關關係描述符的詳細資訊，請閱讀 [!DNL Schema Registry] API開發人員指南 [描述符端點指南](../../xdm/api/descriptors.md)。

可以在請求路徑中包括查詢參數，以指定要訪問的資料。 可以包括多個參數，以和符號(&amp;)分隔。 中提供了有效參數的完整清單 [查詢參數](#query-parameters) 的下界。

**API格式**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

**要求**

以下請求檢索包含先前建立的關係描述符的實體，以訪問不同架構中的資訊。

```shell
curl -X GET \
  https://platform.adobe.io/data/core/ups/access/entities?relatedSchema.name=_xdm.context.profile&schema.name=_xdm.context.experienceevent&relatedEntityId=GkouAW-2Xkftzer3bBtHiW8GkaFL \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
```

**回應**

成功的響應返回與多個實體相關聯的時間系列事件的分頁清單。

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

### 訪問後續結果頁

檢索時間系列事件時，將對結果進行分頁。 如果有後續頁面的結果， `_page.next` 屬性將包含ID。 此外， `_links.next.href` 屬性提供請求URI，用於通過向URI提供其他GET請求來檢索後續頁 `access/entities` 端點。

## 後續步驟

按照本指南，您已成功訪問 [!DNL Real-Time Customer Profile] 資料欄位、配置檔案和時間系列資料。 瞭解如何訪問儲存在 [!DNL Platform]，請參見 [資料存取概述](../../data-access/home.md)。

## 附錄 {#appendix}

以下部分提供了有關訪問 [!DNL Profile] 資料。

### 查詢參數 {#query-parameters}

以下參數用於GET到 `/access/entities` 端點。 它們用於標識要訪問的配置檔案實體並過濾在響應中返回的資料。 將標籤所需參數，而其餘參數為可選參數。

| 參數 | 說明 | 範例 |
|---|---|---|
| `schema.name` | **（必需）** 要檢索的實體的XDM架構 | `schema.name=_xdm.context.experienceevent` |
| `relatedSchema.name` | 如果 `schema.name` 為&quot;_xdm.context.experenceevent&quot;，此值必須指定與時間系列事件相關的配置檔案實體的架構。 | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **（必需）** 實體的ID。 如果此參數的值不是XID，則還必須提供標識命名空間參數(請參見 `entityIdNS` )。 | `entityId=janedoe@example.com` |
| `entityIdNS` | 如果 `entityId` 未作為XID提供，此欄位必須指定標識命名空間。 | `entityIdNE=email` |
| `relatedEntityId` | 如果 `schema.name` 為「_xdm.context.experenceevent」，此值必須指定相關配置檔案實體的標識命名空間。 此值遵循與 `entityId`。 | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | 如果 `schema.name` 為&quot;_xdm.context.experenceevent&quot;，此值必須指定中指定的實體的標識命名空間 `relatedEntityId`。 | `relatedEntityIdNS=CRMID` |
| `fields` | 篩選在響應中返回的資料。 使用此選項可指定要在檢索的資料中包括的架構欄位值。 對於多個欄位，用逗號分隔值，在 | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | 標識用於管理返回資料的合併策略。 如果未在呼叫中指定，則將使用組織對該架構的預設設定。 如果尚未配置預設合併策略，則預設為無配置檔案合併和無標識拼接。 | `mergePoilcyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | 按時間戳（寫入方式）檢索的體驗事件的排序順序 `(+/-)timestamp` 預設值為 `+timestamp`。 | `orderby=-timestamp` |
| `startTime` | 指定篩選時間序列對象的開始時間（以毫秒為單位）。 | `startTime=1539838505` |
| `endTime` | 指定篩選時間序列對象的結束時間（以毫秒為單位）。 | `endTime=1539838510` |
| `limit` | 指定要返回的最大對象數的數值。 預設值：1000 | `limit=100` |
| `property` | 按屬性值篩選。 支援以下計算器：=, !=, &lt;, &lt;=, >, >=。 只能用於體驗事件，最多支援三個屬性。 | `property=webPageDetails.isHomepage=true&property=localTime<="2020-07-20"` |
| `withCA` | 用於啟用計算屬性以進行查找的功能標誌。 預設值：假 | `withCA=true` |
