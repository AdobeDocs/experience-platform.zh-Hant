---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 列出資源
topic: developer guide
translation-type: tm+mt
source-git-commit: fe7b6acf86ebf39da728bb091334785a24d86b49

---


# 列出資源

您可以執行單一GET請求，以檢視容器內所有資源（結構、類別、混合或資料類型）的清單。

**API格式**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}
GET /{CONTAINER_ID}/{RESOURCE_TYPE}?{QUERY_PARAMS}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 資源所在的容器（「全域」或「租用戶」）。 |
| `{RESOURCE_TYPE}` | 要從方案庫中檢索的資源類型。 有效類 `datatypes`型有 `mixins`、 `schemas`和 `classes`。 |
| `{QUERY_PARAMS`} | 可選查詢參數，以篩選結果。 如需詳細資訊，請 [參閱查詢](#query) 參數一節。 |

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

## 使用查詢參數 {#query}

方案註冊表支援在列出資源時使用查詢參數對頁面和篩選結果。

>[!NOTE] 組合多個查詢參數時，必須以&amp;符號(`&`)分隔。

### 分頁

最常用於分頁的查詢參數包括：

| 參數 | 說明 |
| --- | --- |
| `start` | 指定列出結果的起始位置。 範例：將列 `start=2` 出第三個傳回項目的結果。 |
| `limit` | 限制傳回的資源數。 範例：將 `limit=5` 返回5個資源的清單。 |
| `orderby` | 依特定屬性排序結果。 範例：將 `orderby=title` 依標題以升序排序結果(A-Z)。 在標題 `-` 前加入(`orderby=-title`)會依標題以遞減順序(Z-A)排序項目。 |

### 篩選

您可以使用參數來篩選結 `property` 果，該參數可用來對擷取的資源內的指定JSON屬性套用特定運算子。 支援的運算子包括：

| 運算元 | 說明 | 範例 |
| --- | --- | --- |
| `==` | 依屬性是否等於提供的值來篩選。 | `property=title==test` |
| `!=` | 依屬性是否不等於提供的值來篩選。 | `property=title!=test` |
| `<` | 依屬性是否小於提供的值來篩選。 | `property=version<5` |
| `>` | 依屬性是否大於提供的值來篩選。 | `property=version>5` |
| `<=` | 依屬性是否小於或等於提供的值來篩選。 | `property=version<=5` |
| `>=` | 依屬性大於或等於提供的值來篩選。 | `property=version>=5` |
| `~` | 依屬性是否與提供的規則運算式相符來篩選。 | `property=title~test$` |
| (無) | 僅聲明屬性名稱僅返回存在屬性的條目。 | `property=title` |

>[!TIP] 您可以使用參 `property` 數依其相容類別來篩選混音。 例如，只 `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` 返回與XDM Individual Profile類相容的混音。
