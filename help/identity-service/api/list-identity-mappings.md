---
keywords: Experience Platform；首頁；熱門主題；身分；身分
solution: Experience Platform
title: 列出身分對應
description: 對應是叢集中指定名稱空間之所有身分識別的集合。
role: Developer
exl-id: db80c783-620b-4ba3-b55c-75c1fd6e90b1
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 1%

---

# 列出身分對應

對應是叢集中指定名稱空間之所有身分識別的集合。

## 取得單一身分的身分對應

指定身分後，從要求中身分所代表的相同名稱空間擷取所有相關身分。

**API格式**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/mapping
```

**要求**

選項1：提供身分做為名稱空間（`nsId`，依ID）和ID值(`id`)。

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

選項2：提供識別作為名稱空間（`ns`，依名稱）和識別碼值(`id`)。

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

選項3：以XID (`xid`)提供身分識別。 如需如何取得身分識別的XID的詳細資訊，請參閱本檔案有關[取得身分識別的XID](./list-native-id.md)的章節。

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### 取得多個身分的身分對應

將`POST`方法作為上述`GET`方法的批次等同物使用，以擷取多個身分的對應。

>[!NOTE]
>
>請求應指示不超過1000個身分。 超過1000個身分的要求將會導致400個狀態代碼。

**API格式**

```http
POST https://platform.adobe.io/data/core/identity/mappings
```

**要求內文**

選項1：提供要擷取對應之XID的清單。

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

選項2：提供身分清單作為複合ID，其中每個名稱依名稱空間ID命名ID值和名稱空間。 此範例示範在覆寫&quot;Private Graph&quot;的預設`graph-type`時使用此方法。

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

若找不到具有所提供輸入的相關身分，則會傳回`HTTP 204`回應代碼，且不含任何內容。

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

- `lastAssociationTime`：輸入識別上次與此識別相關聯的時間戳記。
- `regions`：提供識別出現位置的`regionId`和`lastAssociationTime`。

## 後續步驟

繼續下一節的教學課程： [列出可用的名稱空間](./list-namespaces.md)。
