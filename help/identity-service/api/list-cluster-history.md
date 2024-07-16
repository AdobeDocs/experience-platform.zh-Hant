---
keywords: Experience Platform；首頁；熱門主題；身分；叢集歷程記錄
solution: Experience Platform
title: 取得身分的叢集記錄
description: 身分可以在各種裝置圖表執行的過程中移動叢集。 Identity Service可讓您檢視特定身分在一段時間內的叢集關聯。
role: Developer
exl-id: e52edb15-e3d6-4085-83d5-212bbd952632
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 1%

---

# 取得身分的叢集歷程記錄

身分可以在各種裝置圖表執行的過程中移動叢集。 [!DNL Identity Service]可顯示特定識別在一段時間內的叢集關聯。

使用選用的`graph-type`引數來指示要從中取得叢集的輸出型別。 選項包括：

- `None` — 不執行身分拼接。
- `Private Graph` — 根據您的私人身分圖表執行身分拼接。 如果未提供`graph-type`，則此為預設值。

## 取得單一身分的叢集歷程記錄

**API格式**

```http
GET https://platform-{REGION}.adobe.io/data/core/identity/cluster/history
```

**要求**

選項1：提供身分做為名稱空間（`nsId`，依ID）和ID值(`id`)。

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?nsId=411&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

選項2：提供識別作為名稱空間（`ns`，依名稱）和識別碼值(`id`)。

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?ns=AMO&id=WTCpVgAAAFq14FMF' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

選項3：以XID (`xid`)提供身分識別。 如需如何取得身分識別的XID的詳細資訊，請參閱本檔案有關[取得身分識別的XID](./list-native-id.md)的章節。

```shell
curl -X GET \
  'https://platform-va7.adobe.io/data/core/identity/cluster/history?xid=CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

## 取得多個身分的叢集歷程記錄

使用`POST`方法作為上述`GET`方法的批次等同方法，以傳回多個身分的叢集記錄。

>[!NOTE]
>
>請求應指示不超過1000個身分。 超過1000個身分的要求將會導致400個狀態代碼。

**API格式**

```http
POST https://platform-va7.adobe.io/data/core/identity/clusters/history
```

**要求內文**

選項1：提供要擷取叢整合員的XID清單。

```shell
{
    "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
    "graph-type": "Private Graph"
}
```

選項2：提供身分清單作為複合ID，其中每個名稱依名稱空間程式碼為ID值和名稱空間命名。

```shell
{
    "compositeXids": [{
            "ns": "AdCloud",
            "id": "WRbM7AAAAJ_PBZHl"
        },
        {
            "ns": "AddCloud",
            "id": "WY-RNgAAArI4rGBo"
        }
    ]
}
```

**要求**

**存根要求**

使用`x-uis-cst-ctx: stub`標頭將傳回存根回應。 這是臨時解決方案，可在服務完成時協助早期整合開發進度。 當不再需要時，這將被取代。

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'x-uis-cst-ctx: stub' \
  -d '{
        "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
        "graph-type": "Private Graph"
      }'
```

**使用XID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "xids": ["GYMBWaoXbMtZ1j4eAAACepuQGhs","b2NJK9a5X7x4LVE4rUqkMyM"],
        "graph-type": "Private Graph"
      }' | json_pp
```

**使用UID**

```shell
curl -X POST \
  https://platform-va7.adobe.io/data/core/identity/clusters/history \
  -H 'authorization: Bearer {ACCESS_TOKEN}' \
  -H 'content-type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
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
        "graph-type": "Private Graph"
      }' | json_pp
```

**回應**

```json
{
    "version": 1,
    "xidsClusterHistory": [{
            "xid": "GZsBQnHQaGtL46ZKSvO9bNRE1DcUyQA",
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNgAAArI4rGBo"
            },
            "clusterHistory": [{
                    "clusterId": "4c686f23-0871-41c2-b4f4-adef89f6bd2c",
                    "cRecordedTS": "1504741401382"
                },
                {
                    "clusterId": "29bf066c-971a-11e7-abc4-cec278b6b50a",
                    "cRecordedTS": "1502063001629"
                },
                {
                    "clusterId": "aeb2f60c-b0f1-446a-91dd-d28ab6a44ff9",
                    "cRecordedTS": "1499384601763"
                }
            ]
        },
        {
            "xid": "CJsDEAMaEAHmCKwPCQYNvzxD9JGDHZ8",
            "compositeXid": {
                "nsid": 411,
                "id": "WY-RNgAAArI4rGBo"
            },
            "clusterHistory": [{
                "clusterId": "4c686f23-0871-41c2-b4f4-adef89f6bd2c",
                "cRecordedTS": "1504741401937"
            }]
        }
    ],
    "unprocessedXids": ["cb0665db616f49758713252d8a335c1e"],
    "unprocessedNids": [{
        "nsid": 411,
        "id": "WY-RNgAAArI4rGBo"
    }]

}
```

>[!NOTE]
>
>無論請求的XID是否屬於相同叢集，或一或多個叢集完全相關，回應中一律會為請求中提供的每個XID各有一個專案。

## 後續步驟

繼續進行下一個教學課程： [列出身分對應](./list-identity-mappings.md)
