---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: PQL轉換
topic: developer guide
translation-type: tm+mt
source-git-commit: 45a196d13b50031d635ceb7c5c952e42c09bd893

---


# PQL轉換

介紹

- 從pql/text和pql/json轉換格式

## 快速入門

本指南中使用的API端點是區段API的一部分。 在繼續之前，請先閱讀區 [段開發人員指南](./getting-started.md)。

尤其是，區 [段開發人員指南的](./getting-started.md#getting-started) 「快速入門」區段包含相關主題的連結、閱讀檔案中範例API呼叫的指南，以及成功呼叫任何Experience Platform API所需之必要標題的重要資訊。

## 從pql/text和pql/json轉換格式

**API格式**

```http
POST /segment/conversion
```

**請求**

```shell
curl -X POST https://platform.adobe.io/data/core/ups/segment/conversion \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {IMS_ORG}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
 -d '
{
  "name": "People who ordered in the last 30 days",
  "expression": {
    "type": "PQL",
    "format": "pql/text",
    "value": "workAddress.country = \"US\""
  },
  "schema": {
    "name": "_xdm.context.profile"
  },
  "ttlInDays": 60
}
 '
```

| 屬性 | 說明 |
| -------- | ----------- |
| `name` | 區段定義的唯一名稱。 |
| `expression.type` | 運算式類型。 它可以是 `PQL` 或 `ARL`。 |
| `expression.format` | 運算式格式。 它可以是 `pql/text` 或 `pql/json`。 |
| `expression.value` | 要轉換的表達式的查詢字串。 |
| `schema.name` | 您所參照之架構的類別ID。 |
| `ttlInDays` | 表示存留時間(TTL)的整數。 |

**回應**

成功的回應會傳回HTTP狀態200，並包含已轉換區段的詳細資料。

```json
{
    "ttlInDays": 60,
    "imsOrgId": "E95186D65A28ABF00A495D82@AdobeOrg",
    "sandbox": {
        "sandboxId": "28e74200-e3de-11e9-8f5d-7f27416c5f0d",
        "sandboxName": "prod",
        "type": "production",
        "default": true
    },
    "expression": {
        "type": "PQL",
        "format": "pql/json",
        "value": "{\"nodeType\":\"fnApply\",\"fnName\":\"=\",\"params\":[{\"nodeType\":\"fieldLookup\",\"fieldName\":\"country\",\"object\":{\"nodeType\":\"fieldLookup\",\"fieldName\":\"workAddress\",\"object\":{\"nodeType\":\"parameterReference\",\"position\":1}}},{\"nodeType\":\"literal\",\"literalType\":\"String\",\"value\":\"US\"}]}"
    }
}
```

## 後續步驟
