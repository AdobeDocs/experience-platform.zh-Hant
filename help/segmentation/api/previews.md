---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 預覽
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# 預覽開發人員指南

介紹

- 建立新預覽
- 擷取特定預覽的結果
- 取消或刪除特定預覽

## 快速入門

本指南中使用的API端點是區段API的一部分。 在繼續之前，請先閱讀區 [段開發人員指南](./getting-started.md)。

尤其是，區 [段開發人員指南的](./getting-started.md#getting-started) 「快速入門」區段包含相關主題的連結、閱讀檔案中範例API呼叫的指南，以及成功呼叫任何Experience Platform API所需之必要標題的重要資訊。

## 建立新預覽

您可以向端點發出POST請求，以建立新的預 `/preview` 覽。

**API格式**

```http
POST /preview
```

**請求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/preview \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
  "predicateExpression": "xEvent.metrics.commerce.abandons.value > 0",
  "predicateType": "pql/text",
  "predicateModel": "_xdm.context.profile",
  "graphType": "pdg"
}
 '
```

body info

**回應**

成功的回應會傳回HTTP狀態201（已建立），並包含您新建立之預覽的詳細資訊。

```json
{
  "state": "NEW",
  "previewQueryId": "e890068b-f5ca-4a8f-a6b5-af87ff0caac3",
  "previewQueryStatus": "NEW",
  "previewId": "MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow",
  "previewExecutionId": 0
}
```

回應資訊，x-location不存在。

## 擷取特定預覽的結果

您可以向端點提出GET請求並在請求路徑中提供預覽值，以檢 `/preview` 索有關特定 `id` 預覽的詳細資訊。

**API格式**

```http
GET /preview/{PREVIEW_ID}
```

- `{PREVIEW_ID}`:您 `id` 要擷取的預覽值。

**請求**

```shell
curl -X GET https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，其中包含指定預覽的詳細資訊。

```json
{
  "state": "RESULT_READY",
  "page": {
    "offset": 0,
    "size": 0
  },
  "results": [],
  "link": {
    "nextPage": ""
  },
  "previewSampledResultsCount": 0
}
```

## 取消或刪除特定預覽

您可以對端點進行DELETE請求，並在請求路徑中 `/preview` 提供預覽值，以刪除 `id` 特定預覽。

**API格式**

```http
DELETE /preview/{PREVIEW_ID}
```

- `{PREVIEW_ID}` 您 `id` 要刪除的預覽值。

**請求**

```shell
curl -X DELETE https://platform.adobe.io/data/core/ups/preview/MDphcHAtMzJiZTAzMjgtM2YzMS00YjY0LThkODQtYWNkMGM0ZmJkYWQzOmU4OTAwNjhiLWY1Y2EtNGE4Zi1hNmI1LWFmODdmZjBjYWFjMzow \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的回應會傳回HTTP狀態200，並顯示下列訊息：

```json
{
  "status": true,
  "message": "KILLED"
}
```

## 後續步驟
