---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: 工會
topic: developer guide
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 1%

---


# 工會

聯合（或聯合視圖）是系統生成的只讀模式，可匯總共用相同類（XDM ExperienceEvent或XDM單個配置檔案）並啟用「即時客戶配置檔案」的所 [有方案的欄位](../../profile/home.md)。

本文檔介紹在方案註冊表API中與工會合作的基本概念，包括各種操作的示例調用。 有關XDM中的聯合的更多一般資訊，請參見架構構成基 [礎中的聯合部分](../schema/composition.md#union)。

## 聯合混音

架構註冊表自動在聯合架構中包含三個混合： `identityMap`、 `timeSeriesEvents`和 `segmentMembership`。

### 身分圖

聯合模式是聯 `identityMap` 合的關聯記錄模式內已知身份的表示。 標識映射將標識分成由命名空間鍵入的不同陣列。 每個列出的身份本身都是包含唯一值的 `id` 對象。

See the [Identity Service documentation](../../identity-service/home.md) for more information.

### 時間系列事件

數 `timeSeriesEvents` 組是與與聯合相關聯的記錄方案相關的時間序列事件的清單。 將配置檔案資料導出到資料集時，每個記錄都包含此陣列。 這對於各種使用案例都很有用，例如機器學習，其中模型除了記錄屬性外還需要描述檔的整個行為歷史記錄。

### 區段會籍圖

地圖 `segmentMembership` 儲存區段評估的結果。 使用區段API成功執行區段 [作業時](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)，會更新地圖。 `segmentMembership` 此外，還會儲存任何預先評估的受眾細分，這些細分會納入Platform中，以便與其他解決方案（例如Adobe Audience Manager）整合。

如需詳細資訊，請 [參閱使用API建立區段](../../segmentation/tutorials/create-a-segment.md) 的教學課程。

## 為聯合會成員啟用方案

要使架構包括在合併的union視圖中，必須將&quot;union&quot;標籤添加到架構的 `meta:immutableTags` 屬性中。 這是通過PATCH請求來更新模式並添加值為&quot;union&quot; `meta:immutableTags` 的陣列來完成的。

>[!NOTE]
>
>不可變標籤是要設定但從不移除的標籤。

**API格式**

```http
PATCH /tenant/schemas/{SCHEMA_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{SCHEMA_ID}` | URL編碼的 `$id` URI或您要 `meta:altId` 啟用用於描述檔的架構。 |

**請求**

```SHELL
curl -X PATCH \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas/_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67 \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '[
        { "op": "add", "path": "/meta:immutableTags", "value": ["union"]}
      ]'
```

**回應**

成功的響應返回更新模式的詳細資訊，該模式現在包 `meta:immutableTags` 含包含字串值&quot;union&quot;的陣列。

```JSON
{
    "title": "Property Information",
    "description": "Property-related information.",
    "type": "object",
    "allOf": [
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590"
        },
        {
            "$ref": "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
        }
    ],
    "meta:class": "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
    "meta:abstract": false,
    "meta:extensible": false,
    "meta:extends": [
        "https://ns.adobe.com/{TENANT_ID}/classes/19e1d8b5098a7a76e2c10a81cbc99590",
        "https://ns.adobe.com/xdm/data/record",
        "https://ns.adobe.com/{TENANT_ID}/mixins/e49cbb2eec33618f686b8344b4597ecf"
    ],
    "meta:containerId": "tenant",
    "imsOrg": "{IMS_ORG}",
    "meta:immutableTags": [
        "union"
    ],
    "meta:altId": "_{TENANT_ID}.schemas.d5cc04eb8d50190001287e4c869ebe67",
    "meta:xdmType": "object",
    "$id": "https://ns.adobe.com/{TENANT_ID}/schemas/d5cc04eb8d50190001287e4c869ebe67",
    "version": "1.2",
    "meta:resourceType": "schemas",
    "meta:registryMetadata": {
        "repo:createDate": 1552088461236,
        "repo:lastModifiedDate": 1552091263267,
        "xdm:createdClientId": "{CREATED_CLIENT}",
        "xdm:repositoryCreatedBy": "{CREATED_BY}"
    }
}
```

## List unions

在架構上設定&quot;union&quot;標籤時，架構註冊表會自動為架構所基於的類建立並維護聯合。 聯 `$id` 合與類的標準類似，唯一的 `$id` 區別是附加兩個下划線和單詞&quot;union&quot;(`"__union"`)。

要查看可用聯合的清單，可以對端點執行GET請 `/unions` 求。

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

**回應**

成功的響應返回HTTP狀態200(OK)和響 `results` 應主體中的陣列。 如果定義了聯合，則每個 `title`聯合的 `$id`、 `meta:altId`和 `version` 作為陣列中的對象提供。 如果尚未定義聯合，則仍會傳回HTTP狀態200（確定），但 `results` 陣列將為空。

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

## 查找特定的聯盟

您可以通過執行GET請求來查看特定的聯合，該請求包括 `$id` 和（取決於「接受」標題），聯合的部分或全部詳細資訊。

>[!NOTE]
>
>聯合查找可使用和 `/unions` 端點 `/schemas` 來啟用它們，以便用於將配置檔案導出到資料集中。

**API格式**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{UNION_ID}` | 您要查閱之 `$id` 工會的URL編碼URI。 聯合結構描述的URI會附加&quot;__union&quot;。 |

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

Union查閱要求必須 `version` 包含在Accept標題中。

以下「接受」標題可用於聯合方案查找：

| 接受 | 說明 |
| -------|------------ |
| application/vnd.adobe.xed+json; version={MAJOR_VERSION} | Raw搭配 `$ref` 和 `allOf`。 包含標題和說明。 |
| application/vnd.adobe.xed-full+json; version={MAJOR_VERSION} | `$ref` 屬性和已解 `allOf` 決。 包含標題和說明。 |

**回應**

成功的響應返回實施在請求路徑中提供的類的所 `$id` 有方案的聯合視圖。

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

## 列出聯合中的結構

為了查看哪些結構是特定聯合的一部分，您可以使用查詢參數來執行GET請求，以篩選租用戶容器內的結構。

使用查 `property` 詢參數，可以將響應配置為僅返回包含欄位和等於您正在訪問其聯 `meta:immutableTags``meta:class` 合的類的方案的方案。

**API格式**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CLASS_ID}` | 您 `$id` 想要存取其工會的類別。 |

**請求**

以下請求查找屬於XDM Individual Profile類聯合的所有方案。

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**回應**

成功的響應返回已篩選的方案清單，僅包含滿足這兩種要求的方案。 請記住，使用多個查詢參數時，會假設AND關係。 回應的格式取決於請求中傳送的「接受」標題。

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
