---
keywords: Experience Platform；首頁；熱門主題；流量服務；
title: 使用流服務API起草資料流
description: 了解如何使用流量服務API將資料流設定為草稿狀態。
badge: label="新功能" type="正"
source-git-commit: d093e34ae4b353d1ed6db922b6da66cf23f25c48
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 2%

---

# 使用流服務API起草資料流

使用流量服務API時，請提供 `mode=draft` 查詢參數。 草稿稍後可以更新為新資訊，並在準備就緒後發佈。 本教學課程涵蓋使用流程服務API，將資料流設定為草稿狀態的步驟。

## 快速入門

本教學課程需要您妥善了解下列Adobe Experience Platform元件：

* [來源](../../home.md): [!DNL Experience Platform] 可讓您從各種來源擷取資料，同時使用來建構、加標籤及增強傳入資料 [!DNL Platform] 服務。
* [沙箱](../../../sandboxes/home.md): [!DNL Experience Platform] 提供可分割單一沙箱的虛擬沙箱 [!DNL Platform] 例項放入個別的虛擬環境，以協助開發及改進數位體驗應用程式。

### 先決條件

本教學課程需要您已產生建立資料流所需的資產。 這包括下列項目：

* 已驗證的基本連接
* 源連接
* 目標XDM架構
* 目標資料集
* 目標連接
* 對應

如果您尚未擁有這些值，請從中選取來源 [來源中的目錄概述](../../home.md). 然後，按照指定源的說明生成起草資料流所需的資產。

### 使用平台API

如需如何成功呼叫Platform API的詳細資訊，請參閱 [Platform API快速入門](../../../landing/api-guide.md).

## 將資料流設定為草稿狀態

以下各節概述了將資料流設定為草稿、更新資料流、發佈資料流並最終刪除資料流的過程。

### 起草資料流

若要將資料流設定為草稿，請向 `/flows` 端點 `mode=draft` 作為查詢參數。 這可讓您建立資料流並將其儲存為草稿。

**API格式**

```http
POST /flows?mode=draft
```

| 參數 | 說明 |
| --- | --- |
| `mode` | 由用戶提供的查詢參數，它決定資料流的狀態。 要將資料流設定為草稿，請設定 `mode` to `draft`. |

**要求**

以下請求將建立草稿資料流。

```shell
  'https://platform-int.adobe.io/data/foundation/flowservice/flows?mode=draft' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
    "name": "HTTP source dataflow for ACME data",
    "sourceConnectionIds": [
        "61c0c5f1-bfe5-40f7-8f8c-a4dc175ddac6"
    ],
    "targetConnectionIds": [
        "78f41c31-3652-4a5e-b264-74331226dcf3"
    ],
    "flowSpec": {
        "id": "c1a19761-d2c7-4702-b9fa-fe91f0613e81",
        "version": "1.0"
    }
  }'
```

**回應**

成功的回應會傳回 `id` 和對應 `etag` 資料流的資料流。

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### 更新資料流

若要更新草稿，請向 `/flows` 端點，同時提供要更新的資料流的ID。 在此步驟中，您也必須提供 `If-Match` header參數，與 `etag` 要更新的資料流。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**要求**

以下請求將映射轉換添加到起草的資料流。

```shell
curl -X PATCH \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
  -H 'If-Match: "69057131-0000-0200-0000-640f48320000"' \
  -d '[
        {
          "op": "add",
          "path": "/transformations",
          "value": [
              {
                  "name": "Mapping",
                  "params": {
                      "mappingId": "44d42ed27c46499a80eb0c0705c38cbd",
                      "mappingVersion": 0
                  }
              }
          ]
      }
  ]'
```

**回應**

成功的回應會傳回您的流程ID，並 `etag`. 若要驗證變更，您可以向 `/flows` 端點，同時提供流ID。

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### 發佈資料流

草稿準備好發佈後，請向 `/flows` 端點，同時提供您要發佈的草稿資料流的ID以及發佈的動作操作。

**API格式**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| 參數 | 說明 |
| --- | --- |
| `op` | 更新查詢的資料流狀態的操作操作。 要發佈草稿資料流，請設定 `op` to `publish`. |

**要求**

以下請求會發佈您的草稿資料流。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的回應會傳回ID和對應的 `etag` 資料流的資料流。

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### 刪除資料流

若要刪除資料流，請向 `/flows` 端點，同時提供要刪除的資料流的ID。 有關如何使用流服務API刪除資料流的詳細步驟，請閱讀 [在API中刪除資料流](./delete-dataflows.md).