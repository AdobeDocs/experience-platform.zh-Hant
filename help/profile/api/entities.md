---
keywords: Experience Platform；設定檔；即時客戶設定檔；疑難排解；API
title: 實體（設定檔存取） API端點
type: Documentation
description: Adobe Experience Platform可讓您使用RESTful API或使用者介面存取即時客戶個人檔案資料。 本指南概述如何使用設定檔API存取實體（通常稱為「設定檔」）。
role: Developer
exl-id: 06a1a920-4dc4-4468-ac15-bf4a6dc885d4
source-git-commit: 9f9823a23c488e63b8b938cb885f050849836e36
workflow-type: tm+mt
source-wordcount: '2181'
ht-degree: 3%

---

# 實體端點（設定檔存取）

Adobe Experience Platform可讓您使用RESTful API或使用者介面存取[!DNL Real-Time Customer Profile]資料。 本指南會概述如何使用API存取實體（通常稱為「設定檔」）。 如需使用[!DNL Platform] UI存取設定檔的詳細資訊，請參閱[設定檔使用手冊](../ui/user-guide.md)。

## 快速入門

本指南中使用的API端點是[[!DNL Real-Time Customer Profile API]](https://www.adobe.com/go/profile-apis-en)的一部分。 繼續之前，請先檢閱[快速入門手冊](getting-started.md)，以取得相關檔案的連結、閱讀本檔案中範例API呼叫的手冊，以及有關成功呼叫任何[!DNL Experience Platform] API所需必要標題的重要資訊。

## 擷取實體 {#retrieve-entity}

您可以透過向`/access/entities`端點發出GET請求以及所需的查詢引數，來擷取設定檔實體或其時間序列資料。

>[!BEGINTABS]

>[!TAB 設定檔實體]

**API格式**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

請求路徑中提供的查詢引數會指定要存取的資料。 您可以包含多個引數，以&amp;分隔。

若要存取設定檔實體，您&#x200B;**必須**&#x200B;提供下列查詢引數：

- `schema.name`：實體的XDM結構描述的名稱。 在此使用案例中，`schema.name=_xdm.context.profile`。
- `entityId`：您嘗試擷取的實體識別碼。
- `entityIdNS`：您嘗試擷取的實體的名稱空間。 如果`entityId`是&#x200B;**而非** XID，則必須提供此值。

附錄的[查詢引數](#query-parameters)區段中提供了有效引數的完整清單。

**要求**

以下請求會使用身分來擷取客戶的電子郵件和名稱。

+++ 使用身分擷取實體的範例要求

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email&fields=identities,person.name,workEmail' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回HTTP狀態200和要求的實體。

+++ 包含請求實體的範例回應

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
                    "id": "johnsmith@example.com",
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

+++

>[!NOTE]
>
>如果相關圖表連結超過50個身分，此服務將傳回HTTP狀態422和「太多相關身分」訊息。 如果收到此錯誤，請考慮新增更多查詢引數來縮小搜尋範圍。

>[!TAB 時間序列事件]

**API格式**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

請求路徑中提供的查詢引數會指定要存取的資料。 您可以包含多個引數，以&amp;分隔。

若要存取時間序列事件資料，您&#x200B;**必須**&#x200B;提供下列查詢引數：

- `schema.name`：實體的XDM結構描述的名稱。 在此使用案例中，這個值為`schema.name=_xdm.context.experienceevent`。
- `relatedSchema.name`：相關結構描述的名稱。 由於結構描述名稱是Experience Event，因此&#x200B;**的值必須**&#x200B;為`relatedSchema.name=_xdm.context.profile`。
- `relatedEntityId`：相關實體的識別碼。
- `relatedEntityIdNS`：相關實體的名稱空間。 如果`relatedEntityId`是&#x200B;**而非** XID，則必須提供此值。

附錄的[查詢引數](#query-parameters)區段中提供了有效引數的完整清單。

**要求**

下列要求會依ID尋找設定檔實體，並擷取與該實體相關聯之所有時間序列事件的屬性`endUserIDs`、`web`和`channel`的值。

+++ 擷取與實體相關之時間序列事件的範例要求

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回HTTP狀態200，其中包含要求查詢引數中指定的時間序列事件和相關欄位的分頁清單。

>[!NOTE]
>
>要求指定一個(`limit=1`)的限制，因此下列回應中的`count`為1，且僅傳回一個實體。

+++ 包含請求的時間序列事件資料的範例回應

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

+++

>[!TAB B2B帳戶]

**API格式**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

請求路徑中提供的查詢引數會指定要存取的資料。 您可以包含多個引數，以&amp;分隔。

若要存取B2B帳戶資料，您&#x200B;**必須**&#x200B;提供下列查詢引數：

- `schema.name`：實體的XDM結構描述的名稱。 在此使用案例中，這個值為`schema.name=_xdm.context.account`。
- `entityId`：您嘗試擷取的實體識別碼。
- `entityIdNS`：您嘗試擷取的實體的名稱空間。 如果`entityId`是&#x200B;**而非** XID，則必須提供此值。

附錄的[查詢引數](#query-parameters)區段中提供了有效引數的完整清單。

**要求**

+++ 擷取B2B帳戶的範例要求

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.account&entityIdNs=b2b_account&entityId=2334262' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回HTTP狀態200和要求的實體。

+++ 包含請求實體的範例回應

```json
{
    "GuQ-AUFjgjaeIw": {
        "entityId": "GuQ-AUFjgjaeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "{SOURCE_ID}",
                    "sourceKey": "{SOURCE_KEY}",
                    "sourceInstanceID": "{SOURCE_INSTANCE_ID}",
                    "sourceType": "{SOURCE_TYPE}"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "{SOURCE_ID}"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!TAB B2B機會]

**API格式**

```http
GET /access/entities?{QUERY_PARAMETERS}
```

請求路徑中提供的查詢引數會指定要存取的資料。 您可以包含多個引數，以&amp;分隔。

若要存取B2B機會實體，您&#x200B;**必須**&#x200B;提供下列查詢引數：

- `schema.name`：實體的XDM結構描述的名稱。 在此使用案例中，`schema.name=_xdm.context.opportunity`。
- `entityId`：您嘗試擷取的實體識別碼。
- `entityIdNS`：您嘗試擷取的實體的名稱空間。 如果`entityId`是&#x200B;**而非** XID，則必須提供此值。

附錄的[查詢引數](#query-parameters)區段中提供了有效引數的完整清單。

**要求**

+++ 擷取B2B機會實體的範例要求

```shell
curl -X GET 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.opportunity&entityIdNs=b2b_opportunity&entityId=2334262' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回HTTP狀態200和要求的實體。

+++ 包含請求實體的範例回應

```json
{
  "Ggw_AUFjgjaeIw": {
        "entityId": "Ggw_AUFjgjaeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!ENDTABS]

## 擷取多個實體 {#retrieve-entities}

您可以對`/access/entities`端點發出POST要求，並在承載中提供身分，以擷取多個設定檔實體或時間序列事件。

>[!BEGINTABS]

>[!TAB 設定檔實體]

**API格式**

```http
POST /access/entities
```

**要求**

以下請求會根據身分清單擷取多個客戶的名稱和電子郵件地址。

+++擷取多個實體的範例請求

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
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
        "orderby": "-timestamp"
      }'
```

| 屬性 | 類型 | 說明 |
| -------- |----- | ----------- |
| `schema.name` | 字串 | **（必要）**&#x200B;實體所屬的XDM結構描述名稱。 |
| `fields` | 陣列 | 要以字串陣列形式傳回的XDM欄位。 預設會傳回所有欄位。 |
| `identities` | 陣列 | **（必要）**&#x200B;陣列，包含您要存取之實體的身分清單。 |
| `identities.entityId` | 字串 | 您要存取之實體的ID。 |
| `identities.entityIdNS.code` | 字串 | 您要存取之實體ID的名稱空間。 |
| `timeFilter.startTime` | 整數 | 指定篩選設定檔實體的開始時間（毫秒）。 預設情況下，此值會設定為可用時間的開始。 |
| `timeFilter.endTime` | 整數 | 指定篩選設定檔實體的結束時間（毫秒）。 預設情況下，此值會設定為可用時間的結尾。 |
| `limit` | 整數 | 要傳回的最大記錄數。 預設情況下，此值會設為1000。 |
| `orderby` | 字串 | 依時間戳記擷取的體驗事件排序順序，寫入為`(+/-)timestamp`，預設為`+timestamp`。 |

+++

**回應**

成功的回應會傳回HTTP狀態200，並在要求內文中指定實體的要求欄位。

+++ 包含請求實體的範例回應

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

+++

>[!TAB 時間序列事件]

**API格式**

```http
POST /access/entities
```

**要求**

下列請求會擷取與設定檔身分識別清單相關之時間序列事件的使用者ID、當地時間和國家/地區代碼。

+++ 擷取時間序列資料的範例要求

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
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
    "limit": 10,
    "orderby": "-timestamp"
}'
```

| 屬性 | 類型 | 說明 |
| -------- | ---- | ----------- |
| `schema.name` | 字串 | **（必要）**&#x200B;實體所屬的XDM結構描述名稱。 |
| `relatedSchema.name` | 字串 | 如果`schema.name`是`_xdm.context.experienceevent`，此值必須指定時間序列事件相關之設定檔實體的結構描述。 |
| `identities` | 陣列 | **（必要）**&#x200B;要從中擷取關聯時間序列事件的設定檔陣列清單。 陣列中的每個專案都是以兩種方式之一設定的： <ol><li>使用包含ID值和名稱空間的完整身分識別</li><li>提供XID</li></ol> |
| `fields` | 字串 | 要以字串陣列形式傳回的XDM欄位。 預設會傳回所有欄位。 |
| `orderby` | 字串 | 依時間戳記擷取的體驗事件排序順序，寫入為`(+/-)timestamp`，預設為`+timestamp`。 |
| `timeFilter.startTime` | 整數 | 指定篩選時間序列物件的開始時間（毫秒）。 預設情況下，此值會設定為可用時間的開始。 |
| `timeFilter.endTime` | 整數 | 指定篩選時間序列物件的結束時間（毫秒）。 預設情況下，此值會設定為可用時間的結尾。 |
| `limit` | 整數 | 要傳回的最大記錄數。 預設情況下，此值會設為1,000。 |

+++

**回應**

成功的回應會傳回HTTP狀態200，其中包含與要求中指定的多個設定檔相關聯的時間序列事件分頁清單。

+++ 包含時間序列事件的範例回應

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

+++

>[!NOTE]
>
>在此範例回應中，列出的第一個設定檔(「GkouAW-yD9aoRCPhRYROJ-TetAFW」)提供`_links.next.payload`的值，表示此設定檔還有其他結果頁面。
>
>若要存取這些結果，您可以對`/access/entities`端點執行其他POST要求，並將列出的裝載作為要求內文。

>[!TAB B2B帳戶]

**API格式**

```http
POST /access/entities
```

**要求**

以下請求會擷取請求的B2B帳戶。

+++擷取多個實體的範例請求

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.account"
        },
        "identities": [
            {
                "entityId": "2334262",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            },
            {
                "entityId": "2334263",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            },
            {
                "entityId": "2334264",
                "entityIdNS": {
                    "code":"b2b_account"
                }
            }
        ]
    }'
```

| 屬性 | 類型 | 說明 |
| -------- |----- | ----------- |
| `schema.name` | 字串 | **（必要）**&#x200B;實體所屬的XDM結構描述名稱。 |
| `identities` | 陣列 | **（必要）**&#x200B;陣列，包含您要存取之實體的身分清單。 |
| `identities.entityId` | 字串 | 您要存取之實體的ID。 |
| `identities.entityIdNS.code` | 字串 | 您要存取之實體ID的名稱空間。 |

+++

**回應**

成功的回應會傳回HTTP狀態200以及請求的實體。

+++ 包含請求實體的範例回應

```json
{
    "GuQ-AUFjgjeeIw": {
        "requestedIdentity": {
            "entityId": "2334263",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjeeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "GuQ-AUFjgjaeIw": {
        "requestedIdentity": {
            "entityId": "2334262",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjaeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_account": [
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    },
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "GuQ-AUFjgjmeIw": {
        "requestedIdentity": {
            "entityId": "2334265",
            "entityIdNS": {
                "code": "b2b_account"
            }
        },
        "entityId": "GuQ-AUFjgjmeIw",
        "mergePolicy": {
            "id": "a6150f47-a94f-4c9d-bfa0-958a370020ee"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334265",
            "identityMap": {
            "b2b_account": [
                {
                    "id": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                },
                {
                    "id": "2334265"
                }
            ]
        },
        "isDeleted": false,
        "accountKey": {
            "sourceID": "2334265",
            "sourceKey": "2334265",
            "sourceInstanceID": "2334265",
            "sourceType": "Random"
        }
    }
}
```

+++

>[!TAB B2B機會]

**API格式**

```http
POST /access/entities
```

**要求**

以下請求會擷取請求的B2B商機。

+++ 擷取多個實體的範例請求

```shell
curl -X POST https://platform.adobe.io/data/core/ups/access/entities \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "schema":{
            "name":"_xdm.context.opportunity"
        },
        "identities": [
            {
                "entityId": "2334262",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334263",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334264",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            },
            {
                "entityId": "2334265",
                "entityIdNS": {
                    "code":"b2b_opportunity"
                }
            }
        ]
    }'
```

| 屬性 | 類型 | 說明 |
| -------- |----- | ----------- |
| `schema.name` | 字串 | **（必要）**&#x200B;實體所屬的XDM結構描述名稱。 |
| `identities` | 陣列 | **（必要）**&#x200B;陣列，包含您要存取之實體的身分清單。 |
| `identities.entityId` | 字串 | 您要存取之實體的ID。 |
| `identities.entityIdNS.code` | 字串 | 您要存取之實體ID的名稱空間。 |

+++

**回應**

成功的回應會傳回HTTP狀態200以及請求的實體。

+++ 包含請求實體的範例回應

```json
{
    "Ggw_AUFjgjaeIw": {
        "requestedIdentity": {
            "entityId": "2334262",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjaeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "Ggw_AUFjgjieIw": {
        "requestedIdentity": {
            "entityId": "2334264",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjieIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0041c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334264",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "2334264"
                    },
                    {
                        "id": "0041c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334264",
                "sourceKey": "2334264",
                "sourceInstanceID": "2334264",
                "sourceType": "Salesforce"
            }
        }
    },
    "Ggw_AUFjgjeeIw": {
        "requestedIdentity": {
            "entityId": "2334263",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjeeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334262",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "0043c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    },
                    {
                        "id": "2334263"
                    },
                    {
                        "id": "2334262"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            }
        }
    },
    "Ggw_AUFjgjmeIw": {
        "requestedIdentity": {
            "entityId": "2334265",
            "entityIdNS": {
                "code": "b2b_opportunity"
            }
        },
        "entityId": "Ggw_AUFjgjmeIw",
        "mergePolicy": {
            "id": "162824be-07f5-4cd0-aa85-2ff3c8f6c775"
        },
        "sources": [
            "er_m_attr"
        ],
        "entity": {
            "_id": "id1",
            "extSourceSystemAudit": {
                "lastReferencedDate": "2024-03-09 12:21:43.0",
                "lastActivityDate": "2024-03-09 12:21:43.0",
                "lastUpdatedDate": "2024-03-09 12:21:43.0",
                "lastUpdatedBy": "{USER_ID}",
                "externalKey": {
                    "sourceID": "00394S0001xpG6xABE",
                    "sourceKey": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce",
                    "sourceInstanceID": "00DC0000000Q35nMAC",
                    "sourceType": "Salesforce"
                },
                "lastViewedDate": "2024-03-09 12:21:43.0",
                "createdDate": "2024-03-09 12:21:43.0"
            },
            "accountID": "2334265",
            "identityMap": {
                "b2b_opportunity": [
                    {
                        "id": "2334265"
                    },
                    {
                        "id": "0054c329201xpG6xAAE@00DC0000000Q35nWIN.Salesforce"
                    }
                ]
            },
            "isDeleted": false,
            "opportunityKey": {
                "sourceID": "2334262",
                "sourceKey": "2334262",
                "sourceInstanceID": "2334262",
                "sourceType": "Random"
            },
            "accountKey": {
                "sourceID": "2334265",
                "sourceKey": "2334265",
                "sourceInstanceID": "2334265",
                "sourceType": "Random"
            }
        }
    }
}
```

+++

>[!ENDTABS]

### 存取後續結果頁面

擷取時間序列事件時，結果會分頁。 如果有後續結果頁面，`_page.next`屬性將包含ID。 此外，`_links.next.href`屬性提供要求URI以擷取下一頁。 若要擷取結果，請對`/access/entities`端點提出另一個GET要求，並以提供的URI值取代`/entities`。

>[!NOTE]
>
>請確定您未意外在請求路徑中重複`/entities/`。 它應該只會出現一次，例如`/access/entities?start=...`

**API格式**

```http
GET /access/{NEXT_URI}
```

| 參數 | 說明 |
|---|---|
| `{NEXT_URI}` | URI值取自`_links.next.href`。 |

**要求**

下列要求會使用`_links.next.href` URI做為要求路徑，以擷取結果的下一頁。

+++ 存取下一頁結果的範例要求

```shell
curl -X GET \
  'https://platform.adobe.io/data/core/ups/access/entities?start=c8d11988-6b56-4571-a123-b6ce74236037&orderby=timestamp&schema.name=_xdm.context.experienceevent&relatedSchema.name=_xdm.context.profile&relatedEntityId=89149270342662559642753730269986316900&relatedEntityIdNS=ECID&fields=endUserIDs,web,channel&startTime=1531260476000&endTime=1531260480000&limit=1' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回結果的下一頁。 此回應沒有後續結果頁面，如`_page.next`和`_links.next.href`的空字串值所指示。

+++ 包含實體下一頁的範例回應

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

+++

## 刪除實體 {#delete-entity}

您可以透過向`/access/entities`端點發出DELETE請求以及所需的查詢引數，從設定檔存放區中刪除實體。

**API格式**

```http
DELETE /access/entities?{QUERY_PARAMETERS}
```

請求路徑中提供的查詢引數會指定要存取的資料。 您可以包含多個引數，以&amp;分隔。

若要刪除實體，您&#x200B;**必須**&#x200B;提供下列查詢引數：

- `schema.name`：實體的XDM結構描述的名稱。 在此使用案例中，您只能&#x200B;**使用** `schema.name=_xdm.context.profile`。
- `entityId`：您嘗試擷取的實體識別碼。
- `entityIdNS`：您嘗試擷取的實體的名稱空間。 如果`entityId`是&#x200B;**而非** XID，則必須提供此值。
- `mergePolicyId`：實體的合併原則識別碼。 合併原則包含身分拼接和索引鍵/值XDM物件合併的相關資訊。 如果未提供此值，則會使用預設合併原則。

**要求**

以下請求會刪除指定的實體。

+++ 刪除實體的範例請求

```shell
curl -X DELETE 'https://platform.adobe.io/data/core/ups/access/entities?schema.name=_xdm.context.profile&entityId=janedoe@example.com&entityIdNS=email' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

+++

**回應**

成功的回應會傳回HTTP狀態202和空白的回應本文。

## 後續步驟

依照本指南，您已成功存取[!DNL Real-Time Customer Profile]資料欄位、設定檔和時間序列資料。 若要瞭解如何存取儲存在[!DNL Platform]中的其他資料資源，請參閱[資料存取總覽](../../data-access/home.md)。

## 附錄 {#appendix}

下節提供有關使用API存取[!DNL Profile]資料的補充資訊。

### 查詢參數 {#query-parameters}

下列引數用於`/access/entities`端點之GET要求的路徑。 它們用於識別您要存取的設定檔實體，並篩選回應中傳回的資料。 必要引數會加上標籤，其餘引數則為選用。

| 參數 | 說明 | 範例 |
| --------- | ----------- | ------- |
| `schema.name` | **（必要）**&#x200B;實體的XDM結構描述名稱。 | `schema.name=_xdm.context.experienceevent` |
| `relatedSchema.name` | 如果`schema.name`是`_xdm.context.experienceevent`，此值&#x200B;**必須**&#x200B;為時間序列事件相關的設定檔實體指定結構描述。 | `relatedSchema.name=_xdm.context.profile` |
| `entityId` | **（必要）**&#x200B;實體的識別碼。 如果此引數的值不是XID，則必須也提供身分名稱空間引數(`entityIdNS`)。 | `entityId=janedoe@example.com` |
| `entityIdNS` | 如果未提供`entityId`作為XID，此欄位&#x200B;**必須**&#x200B;指定身分名稱空間。 | `entityIdNS=email` |
| `relatedEntityId` | 如果`schema.name`是`_xdm.context.experienceevent`，此值&#x200B;**必須**&#x200B;指定相關設定檔實體的識別碼。 此值遵循與`entityId`相同的規則。 | `relatedEntityId=69935279872410346619186588147492736556` |
| `relatedEntityIdNS` | 如果`schema.name`是「_xdm.context.experienceevent」，此值必須為`relatedEntityId`中指定的實體指定身分名稱空間。 | `relatedEntityIdNS=CRMID` |
| `fields` | 篩選回應中傳回的資料。 使用此專案來指定要包含在擷取之資料中的結構描述欄位值。 針對多個欄位，請使用逗號分隔值，且中間不應有空格。 | `fields=personalEmail,person.name,person.gender` |
| `mergePolicyId` | 識別用來控管傳回資料的合併原則。 如果未在呼叫中指定，則會使用您組織對該結構描述的預設值。 如果尚未設定預設合併原則，預設值為無設定檔合並且無身分拼接。 | `mergePolicyId=5aa6885fcf70a301dabdfa4a` |
| `orderBy` | 依時間戳記所擷取實體的排序順序。 這會寫入為`(+/-)timestamp`，預設為`+timestamp`。 | `orderby=-timestamp` |
| `startTime` | 指定篩選實體的開始時間（毫秒）。 | `startTime=1539838505` |
| `endTime` | 指定篩選實體的結束時間（毫秒）。 | `endTime=1539838510` |
| `limit` | 指定要傳回的最大實體數。 預設情況下，此值會設為1000。 | `limit=100` |
| `property` | 依屬性值篩選。 此查詢引數支援下列求值器： =、！=， &lt;， &lt;=， >， >=。 這只能用於體驗事件，最多支援三個屬性。 | `property=webPageDetails.isHomepage=true&property=localTime<="2020-07-20"` |
