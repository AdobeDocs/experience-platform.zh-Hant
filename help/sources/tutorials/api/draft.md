---
keywords: Experience Platform；首頁；熱門主題；流式服務；
title: 使用流服務API繪製資料流
description: 瞭解如何使用流服務API將資料流設定為草稿狀態。
badge: label="新功能" type="正"
exl-id: aad6a302-1905-4a23-bc3d-39e76c9a22da
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 2%

---

# 使用流服務API繪製資料流

使用流服務API時，通過提供 `mode=draft` 查詢參數。 稍後可以用新資訊更新草稿，然後在草稿準備好後發佈。 本教程介紹使用流服務API將資料流設定為草稿狀態的步驟。

## 快速入門

本教程要求您對以下Adobe Experience Platform元件有一定的瞭解：

* [源](../../home.md): [!DNL Experience Platform] 允許從各種源接收資料，同時讓您能夠使用 [!DNL Platform] 服務。
* [沙箱](../../../sandboxes/home.md): [!DNL Experience Platform] 提供虛擬沙箱，將單個沙箱 [!DNL Platform] 實例到獨立的虛擬環境，以幫助開發和發展數字型驗應用程式。

### 先決條件

本教程要求您已生成建立資料流所需的資產。 這包括以下內容：

* 已驗證的基連接
* 源連接
* 目標XDM架構
* 目標資料集
* 目標連接
* 映射

如果尚沒有這些值，則從中選擇源 [源概覽中的目錄](../../home.md)。 然後，按照給定源的說明生成起草資料流所需的資產。

### 使用平台API

有關如何成功調用平台API的資訊，請參見上的指南 [平台API入門](../../../landing/api-guide.md)。

## 將資料流設定為草稿狀態

以下各節概述了將資料流設定為草稿、更新資料流、發佈資料流並最終刪除資料流的過程。

### 起草資料流

要將資料流設定為草稿，請向 `/flows` 添加端點時 `mode=draft` 作為查詢參數。 這允許您建立資料流並將其另存為草稿。

**API格式**

```http
POST /flows?mode=draft
```

| 參數 | 說明 |
| --- | --- |
| `mode` | 用戶提供的查詢參數，它決定資料流的狀態。 要將資料流設定為草稿，請設定 `mode` 至 `draft`。 |

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

成功的響應返回 `id` 和對應 `etag` 資料流。

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### 更新資料流

要更新草稿，請向 `/flows` 終結點，同時提供要更新的資料流的ID。 在此步驟中，您還必須提供 `If-Match` 標頭參數，與 `etag` 要更新的資料流。

**API格式**

```http
PATCH /flows/{FLOW_ID}
```

**要求**

以下請求將映射轉換添加到已起草的資料流。

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

成功的響應返回流ID和 `etag`。 要驗證更改，可向 `/flows` 提供流ID時的終結點。

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### 發佈資料流

一旦您的草稿準備好發佈，請向 `/flows` 終結點，同時提供要發佈的草稿資料流的ID以及用於發佈的操作操作。

**API格式**

```http
POST /flows/{FLOW_ID}/action?op=publish
```

| 參數 | 說明 |
| --- | --- |
| `op` | 更新查詢的資料流狀態的操作操作。 要發佈草稿資料流，請設定 `op` 至 `publish`。 |

**要求**

以下請求發佈您的草稿資料流。

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/flows/c9751426-dff8-49b0-965f-50defcf4187b/action?op=publish' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

**回應**

成功的響應返回ID和相應 `etag` 資料流。

```json
{
  "id": "c9751426-dff8-49b0-965f-50defcf4187b",
  "etag": "\"69057131-0000-0200-0000-640f48320000\""
}
```

### 刪除資料流

要刪除資料流，請向 `/flows` 提供要刪除的資料流的ID時的終結點。 有關如何使用流服務API刪除資料流的詳細步驟，請閱讀上的指南 [刪除API中的資料流](./delete-dataflows.md)。
