---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 列出資源
topic: developer guide
translation-type: tm+mt
source-git-commit: 1541b027a4e572dc5e4e64de1117a269c58bafab

---


# 列出資源

您可以執行單一GET請求，以檢視容器內所有資源（結構、類別、混合或資料類型）的清單。 為幫助篩選結果，方案註冊表支援在列出資源時使用查詢參數。

最常見的查詢參數包括：

* `limit` -限制返回的資源數。 範例：將 `limit=5` 返回5個資源的清單。
* `orderby` -按特定屬性對結果排序。 範例：將 `orderby=title` 依標題以升序排序結果(A-Z)。 在標題 `-` 前加入(`orderby=-title`)會依標題以遞減順序(Z-A)排序項目。
* `property` -篩選任何頂層屬性的結果。 例如，只 `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` 返回與XDM Individual Profile類相容的混音。

組合多個查詢參數時，必須以&amp;符號(`&`)分隔。

**API格式**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 資源所在的容器（「全域」或「租用戶」）。 |
| `{RESOURCE_TYPE}` | 要從方案庫中檢索的資源類型。 有效類 `datatypes`型有 `mixins`、 `schemas`和 `classes`。 |

**請求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/global/classes&limit=2 \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於請求中傳送的「接受」標題。 下列「接受」標題可用於列出資源：

| 接受標題 | 說明 |
| ------- | ------------ |
| application/vnd.adobe.xed-id+json | 傳回每個資源的簡短摘要，通常是列出的首選標題 |
| application/vnd.adobe.xed+json | 傳回每個資源的完整JSON結構描述，其中包含 `$ref` 原始資 `allOf` 源 |

**回應**

上述請求使用「 `application/vnd.adobe.xed-id+json` 接受」標題，因此回應僅包含每個資 `title`源的 `$id`、 `meta:altId`和 `version` 屬性。 替換 `full` 到「接受」標題會返回每個資源的所有屬性。 根據您在回應中需要的資訊，選擇適當的「接受」標題。

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```
