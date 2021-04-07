---
keywords: Experience Platform;home；熱門主題；api;API;XDM;XDM;XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；模式註冊表；結構；聯合；聯盟；segmentMembership;timeSeriesEvents;
solution: Experience Platform
title: 工會API端點
description: 架構註冊表API中的/union端點可讓您以程式設計方式管理體驗應用程式中的XDM結合架構。
topic: 開發人員指南
exl-id: d0ece235-72e8-49d9-856b-5dba44e16ee7
translation-type: tm+mt
source-git-commit: 610ce5c6dca5e7375b941e7d6f550382da10ca27
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 1%

---

# 工會端點

聯合（或聯合視圖）是系統生成的只讀模式，可匯總共用相同類（[!DNL XDM ExperienceEvent]或[!DNL XDM Individual Profile]）且為[[!DNL Real-time Customer Profile]](../../profile/home.md)啟用的所有方案的欄位。

本文檔介紹在方案註冊表API中與工會合作的基本概念，包括各種操作的示例調用。 有關XDM中聯合的更多一般資訊，請參見[架構組合基礎](../schema/composition.md#union)中有關聯合的部分。

## 聯合架構欄位

[!DNL Schema Registry]會自動在聯合架構中包含三個鍵欄位：`identityMap`、`timeSeriesEvents`和`segmentMembership`。

### 身分圖

聯合模式的`identityMap`表示聯合的關聯記錄模式內的已知身份。 標識映射將標識分成由命名空間鍵入的不同陣列。 每個列出的身份本身都是包含唯一`id`值的對象。 如需詳細資訊，請參閱[Identity Service檔案](../../identity-service/home.md)。

### 時間系列事件

`timeSeriesEvents`陣列是與與聯合相關聯的記錄方案相關的時間序列事件的清單。 將配置檔案資料導出到資料集時，每個記錄都包含此陣列。 這對於各種使用案例都很有用，例如機器學習，其中模型除了記錄屬性外還需要描述檔的整個行為歷史記錄。

### 區段會籍圖

`segmentMembership`地圖會儲存區段評估的結果。 使用[分段API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)成功執行分段作業時，會更新對應。 `segmentMembership` 此外，還會儲存任何預先評估的受眾細分，這些細分會收錄到Platform中，以便與Adobe Audience Manager等其他解決方案整合。如需詳細資訊，請參閱[使用API建立區段的教學課程。](../../segmentation/tutorials/create-a-segment.md)

## 檢索工會清單{#list}

在架構上設定`union`標籤時，[!DNL Schema Registry]會自動將架構添加到架構所基於的類的聯合中。 如果相關類不存在聯合，則會自動建立新聯合。 聯合的`$id`與其他[!DNL Schema Registry]資源的標準`$id`類似，唯一的區別是附加兩個下划線和單字&quot;union&quot;(`__union`)。

通過向`/tenant/unions`端點發出GET請求，可以查看可用工會的清單。

**API格式**

```http
GET /tenant/unions
```

**請求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

回應格式取決於請求中傳送的`Accept`標題。 下列`Accept`標題可用於列出工會：

| `Accept` 標題 | 說明 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每個資源的簡短摘要。 這是列出資源的建議標題。 (限制：300) |
| `application/vnd.adobe.xed+json` | 傳回每個資源的完整JSON類別，並包含原始的`$ref`和`allOf`。 (限制：300) |

**回應**

成功的響應返迴響應主體中的HTTP狀態200(OK)和`results`陣列。 如果已定義了聯合，則每個聯合的詳細資訊都作為陣列中的對象提供。 如果尚未定義聯合，則仍會返回HTTP狀態200（確定），但`results`陣列將為空。

```JSON
{
    "results": [
        {
            "title": "XDM Individual Profile",
            "$id": "https://ns.adobe.com/xdm/context/profile__union",
            "meta:altId": "_xdm.context.profile__union",
            "version": "1"
        },
        {
            "title": "Property",
            "$id": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590__union",
            "meta:altId": "_{TENANT_ID}.classes.19e1d8b5098a7a76e2c10a81cbc99590__union",
            "version": "1"
        }
    ]
}
```

## 查找聯合{#lookup}

您可以通過執行包含`$id`和（取決於「接受」標題）的GET請求來查看特定的聯合，以及聯合的部分或全部詳細資訊。

>[!NOTE]
>
>聯合查找可使用`/unions`和`/schemas`端點，以便用於[!DNL Profile]導出到資料集中。

**API格式**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{UNION_ID}` | 您要查找的聯合的URL編碼`$id` URI。 聯合結構描述的URI會附加&quot;__union&quot;。 |

**請求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile__union \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

聯合查閱請求需要`version`包含在「接受」標題中。

以下「接受」標題可用於聯合方案查找：

| Accept | 說明 |
| -------|------------ |
| `application/vnd.adobe.xed+json; version=1` | Raw含`$ref`和`allOf`。 包含標題和說明。 |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 屬性並 `allOf` 解析。包含標題和說明。 |

**回應**

成功的響應返回實現`$id`在請求路徑中提供的類的所有方案的聯合視圖。

回應格式取決於請求中傳送的「接受」標題。 嘗試不同的「接受」標題，以比較回應，並判斷哪個標題最適合您的使用案例。

```JSON
{
    "type": "object",
    "description": "Union view of all schemas that extend https://ns.adobe.com/xdm/context/profile",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-person-details"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/477bb01d7125b015b4feba7bccc2e599"
        },
        {
            "$ref": "https://ns.adobe.com/xdm/context/profile-personal-details"
        }
    ],
    "meta:extends": [
        "https://ns.adobe.com/xdm/context/profile",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/xdm/context/identitymap",
        "https://ns.adobe.com/xdm/common/extensible",
        "https://ns.adobe.com/xdm/common/auditable",
        "https://ns.adobe.com/xdm/context/profile-person-details",
        "https://ns.adobe.com/{TENANT_ID}/mixins/477bb01d7125b015b4feba7bccc2e599",
        "https://ns.adobe.com/xdm/context/profile-personal-details"
    ],
    "title": "Union object for https://ns.adobe.com/xdm/context/profile",
    "$id": "https://ns.adobe.com/xdm/context/profile__union",
    "meta:containerId": "tenant",
    "meta:class": "https://ns.adobe.com/xdm/context/profile",
    "meta:altId": "_xdm.context.profile__union",
    "version": "1.0",
    "meta:resourceType": "unions",
    "meta:registryMetadata": {}
}
```

## 為聯合成員資格啟用方案{#enable}

要使架構包含在其類的union中，必須將`union`標籤添加到架構的`meta:immutableTags`屬性中。 您可以通過PATCH請求將`meta:immutableTags`陣列添加到相關方案中，該陣列的單字串值為`union`。 有關詳細示例，請參見[方案端點指南](./schemas.md#union)。

## 列出聯合{#list-schemas}中的方案

為了查看哪些方案屬於特定聯合的一部分，您可以對`/tenant/schemas`端點執行GET請求。 使用`property`查詢參數，可以將響應配置為僅包含`meta:immutableTags`欄位和`meta:class`等於您正在訪問其聯合的類的返回方案。

**API格式**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CLASS_ID}` | 要列出其聯合啟用方案的類的`$id`。 |

**請求**

以下請求將檢索屬於[!DNL XDM Individual Profile]類聯合的所有方案的清單。

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於請求中傳送的`Accept`標題。 以下`Accept`標題可用於列出方案：

| `Accept` 標題 | 說明 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每個資源的簡短摘要。 這是列出資源的建議標題。 (限制：300) |
| `application/vnd.adobe.xed+json` | 傳回每個資源的完整JSON結構描述，並包含原始的`$ref`和`allOf`。 (限制：300) |

**回應**

成功的響應返回已篩選的方案清單，其中僅包含屬於已啟用聯合成員資格的指定類的方案。 請記住，使用多個查詢參數時，會假設AND關係。

```JSON
{
    "results": [
        {
            "title": "Schema 1",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/142afb78d8b368a5ba97a6cc8fc7e033",
            "meta:altId": "_{TENANT_ID}.schemas.142afb78d8b368a5ba97a6cc8fc7e033",
            "version": "1.2"
        },
        {
            "title": "Schema 2",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/e7297a6ddfc7812ab3a7b504a1ab98da",
            "meta:altId": "_{TENANT_ID}.schemas.e7297a6ddfc7812ab3a7b504a1ab98da",
            "version": "1.5"
        },
        {
            "title": "Schema 3",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/50f960bb810e99a21737254866a477bf",
            "meta:altId": "_{TENANT_ID}.schemas.50f960bb810e99a21737254866a477bf",
            "version": "1.2"
        },
        {
            "title": "Schema 4",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/a39655ca8ea3d5c1f36a463b45fccca8",
            "meta:altId": "_{TENANT_ID}.schemas.a39655ca8ea3d5c1f36a463b45fccca8",
            "version": "1.1"
        },
        {
            "title": "Schema 5",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/c063fac45c6d6285ef33b0e2af09f633",
            "meta:altId": "_{TENANT_ID}.schemas.c063fac45c6d6285ef33b0e2af09f633",
            "version": "1.2"
        },
        {
            "title": "Schema 6",
            "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/dfebb19b93827b70bbad006137812537",
            "meta:altId": "_{TENANT_ID}.schemas.dfebb19b93827b70bbad006137812537",
            "version": "1.7"
        }
    ],
    "_links": {
        "global_schemas": {
            "href": "https://platform.adobe.io/data/foundation/schemaregistry/global/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile"
        }
    }
}
```
