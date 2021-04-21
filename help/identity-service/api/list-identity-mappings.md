---
keywords: Experience Platform;home；熱門主題；identity;Identity
solution: Experience Platform
title: 清單標識映射
topic-legacy: API guide
description: 映射是群集中所有標識的集合，用於指定的命名空間。
exl-id: db80c783-620b-4ba3-b55c-75c1fd6e90b1
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 1%

---

# 清單標識映射

映射是群集中所有標識的集合，用於指定的命名空間。

## 取得單一身分的身分對應

給定身份，從請求中由身份表示的相同名稱空間中檢索所有相關身份。

**API格式**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/mapping
```

**要求**

選項1:將識別碼提供為命名空間（`nsId`，依ID）和ID值(`id`)。

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

選項2:將身分提供為namespace（`ns`，依名稱）和ID值(`id`)。

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

選項3:提供身份作為XID(`xid`)。 有關如何獲取身份的XID的詳細資訊，請參閱本文檔中有關[獲取身份的XID的章節](./list-native-id.md)。

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/mapping?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

### 獲取多個身份的身份映射

使用`POST`方法作為與上述`GET`方法相等的批處理，以檢索多個身份的映射。

>[!NOTE]
>
>請求應指明最多1000個身分。 超過1000個身分的要求將產生400個狀態碼。

**API格式**

```http
POST https://platform.adobe.io/data/core/identity/mappings
```

**請求正文**

選項1:提供要檢索映射的XID清單。

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

選項2:提供身分清單作為複合ID，其中每個ID值皆以命名空間ID命名。 此示例演示在覆蓋「專用圖」的預設`graph-type`時使用此方法。

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
        "xids" : ["GesCQXX0CAESEE8wHpswUoLXXmrYy8KBTVgA"],
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

如果所提供的輸入未找到相關身份，則會傳回沒有內容的`HTTP 204`回應碼。

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

- `lastAssociationTime`:輸入身份上次與此身份關聯的時間戳。
- `regions`:提供 `regionId` 和 `lastAssociationTime` 身份的顯示位置。

## 後續步驟

繼續下一個教程，以[列出可用名稱空間](./list-namespaces.md)。
