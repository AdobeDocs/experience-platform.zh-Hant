---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;list;List;get;GET
solution: Experience Platform
title: 列出資源
description: 通過執行單個GET請求，可以查看容器內特定類型（類、混合、方案、資料類型或描述符）的所有模式註冊表資源的清單。
topic: developer guide
translation-type: tm+mt
source-git-commit: 74a4a3cc713cc068be30379e8ee11572f8bb0c63
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 2%

---


# 列出資源

您可以執行單一GET請 [!DNL Schema Registry] 求，以檢視容器內特定類型（類、混合、結構、資料類型或描述子）的所有資源清單。

>[!NOTE]
>
>列出資源時，結 [!DNL Schema Registry] 果集限制為300個項目。 若要傳回超出此限制的資源，您必須使用分 [頁參數](#paging)。 建議您使用查詢參數來篩 [選結果](#filtering) ，並減少傳回的資源數。

**API格式**

```http
GET /{CONTAINER_ID}/{RESOURCE_TYPE}
GET /{CONTAINER_ID}/{RESOURCE_TYPE}?{QUERY_PARAMS}
```

| 參數 | 說明 |
| --- | --- |
| `{CONTAINER_ID}` | 資源所在的容器（「全域」或「租用戶」）。 |
| `{RESOURCE_TYPE}` | 要從中檢索的資源類型 [!DNL Schema Library]。 有效類 `classes`型有 `mixins`、 `schemas`、 `datatypes`和 `descriptors`。 |
| `{QUERY_PARAMS}` | 可選查詢參數，以篩選結果。 如需詳細資訊，請 [參閱查詢](#query) 參數一節。 |

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
| application/vnd.adobe.xed-id+json | 返回每個資源的簡短摘要。 這是列出資源的建議標題。 (限制：300) |
| application/vnd.adobe.xed+json | 傳回每個資源的完整JSON結構描述，其中包含 `$ref` 原始 `allOf` 資源。 (限制：300) |
| application/vnd.adobe.xdm-v2+json | 使用端點 `/descriptors` 時，必須使用此接受標頭才能使用尋呼功能。 |

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

在列 [!DNL Schema Registry] 出資源時，支援對頁面使用查詢參數並篩選結果。

>[!NOTE]
>
>組合多個查詢參數時，必須以&amp;符號(`&`)分隔。

### 分頁 {#paging}

最常用於分頁的查詢參數包括：

| 參數 | 說明 |
| --- | --- |
| `start` | 指定列出的結果的開始位置。 此值可從清單回應 `_page.next` 的屬性中取得，並用於存取下一頁的結果。 如果 `_page.next` 值為null，則沒有其他頁面可用。 |
| `limit` | 限制傳回的資源數。 範例： `limit=5` 將會傳回5個資源清單。 |
| `orderby` | 依特定屬性排序結果。 範例： `orderby=title` 將按標題的升序排序結果(A-Z)。 在標題 `-` 前加入(`orderby=-title`)會依標題以遞減順序(Z-A)排序項目。 |

### 篩選 {#filtering}

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
| (None) | 僅聲明屬性名稱僅返回存在屬性的條目。 | `property=title` |

>[!TIP]
>
>您可以使用參 `property` 數依其相容類別來篩選混音。 例如， `property=meta:intendedToExtend==https://ns.adobe.com/xdm/context/profile` 僅傳回與類相容的混 [!DNL XDM Individual Profile] 音。
