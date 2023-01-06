---
keywords: Experience Platform；首頁；熱門主題；身分；身分
solution: Experience Platform
title: 清單身分對應
description: 對應是叢集中指定命名空間之所有身分識別的集合。
exl-id: db80c783-620b-4ba3-b55c-75c1fd6e90b1
source-git-commit: 6d01bb4c5212ed1bb69b9a04c6bfafaad4b108f9
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 1%

---

# 列出標識映射

對應是叢集中指定命名空間之所有身分識別的集合。

## 取得單一身分的身分對應

在提供身分識別後，請使用與請求中的身分識別所代表的相同命名空間來擷取所有相關身分識別。

**API格式**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/mapping
```

**要求**

選項1:將身分提供為命名空間(`nsId`，依ID)和ID值(`id`)。

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

選項2:將身分提供為命名空間(`ns`，依名稱)和ID值(`id`)。

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

選項3:將標識提供為XID(`xid`)。 如需如何取得身分識別的XID的詳細資訊，請參閱本檔案涵蓋 [獲取XID以獲取身份](./list-native-id.md).

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### 取得多個身分的身分對應

使用 `POST` 方法，如批次等值 `GET` 方法，擷取多個身分的對應。

>[!NOTE]
>
>請求應指示最多1000個身分。 超過1000個身分的請求將產生400個狀態代碼。

**API格式**

```http
POST https://platform.adobe.io/data/core/identity/mappings
```

**要求內文**

選項1:提供要檢索映射的XID的清單。

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

選項2:提供身分識別清單作為複合ID，其中每個ID的名稱都是ID值，而命名空間ID是依命名空間ID命名的。 此範例示範如何覆寫預設值時使用此方法 `graph-type` 「私密圖表」。

```shell
{
    "compositeXids": [{
            "nsid": 411,
            "id": "WRbM7AAAAJ_PBZHl"
        },
        {
            "nsid": 411,
            "id": "WY-RNgAAArI4rGBo"
        }
    ],
    "graph-type": "None"
}
```

**要求**

**使用XID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/mappings \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: 111111@AdobeOrg' \
  -d '{
        "xids": ["GesCQXX0CAESEE8wHpswUoLXXmrYy8KBTVgA"],
        "targetNs": "0",
        "graph-type": "Private Graph"
      }' | json_pp
```

**使用UID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/mappings \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: 111111@AdobeOrg' \
  -d '{
            "compositeXids": [{
                    "nsid": 411,
                    "id": "WRbM7AAAAJ_PBZHl"
                },
                {
                    "nsid": 411,
                    "id": "WY-RNgAAArI4rGBo"
                }
            ],
        "targetNs": "0",
        "graph-type": "Private Graph"
      }' | json_pp
```

若未找到所提供輸入的相關身分，則 `HTTP 204` 回應代碼會傳回，但不含任何內容。

**回應**

```json
{
    "version": 1,
    "mappings": [{
        "xid": "CAESEPl1uYyma1kMDWxx7dhbwGo",
        "mapping": [{
            "xid": "81218968060697815473313992060878182012",
            "lastAssociationTime": "1493310475047"
        }],
        "compositeXid": {
            "nsid": 411,
            "id": "WY-RNgAAArI4rGBo"
        },
        "mapping": [{
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNchvdsTSJS"
            },
            "lastAssociationTime": "1493310475047"
        }],

        "regions": [{
            "regionId": "10",
            "lastAssociationTime": "1493310475047"
        }]
    }],
    "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
    "unprocessedNids": [{
        "nsid": 411,
        "id": "WY-RNgAAArI4rGBo"
    }]
}
```

- `lastAssociationTime`:上次與此標識關聯的輸入標識的時間戳。
- `regions`:提供 `regionId` 和 `lastAssociationTime` 在哪裡發現了身份。

## 後續步驟

繼續下一個教學課程，前往 [清單可用命名空間](./list-namespaces.md).
