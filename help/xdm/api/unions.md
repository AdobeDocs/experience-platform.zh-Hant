---
keywords: Experience Platform;home;popular topics;api;API;XDM;XDM system;;experience data model;Experience data model;Experience Data Model;data model;Data Model;schema registry;Schema Registry;union;Union;unions;Unions;segmentMembership;timeSeriesEvents;
solution: Experience Platform
title: 工會
description: 架構註冊表API中的/union端點可讓您以程式設計方式管理體驗應用程式中的XDM結合架構。
topic: developer guide
translation-type: tm+mt
source-git-commit: 0b55f18eabcf1d7c5c233234c59eb074b2670b93
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 1%

---


# 工會端點

聯合（或聯合視圖）是系統生成的只讀模式，用於聚合所有共用相同類(或[!DNL XDM ExperienceEvent][!DNL XDM Individual Profile])並啟用的方案的欄位 [[!DNL Real-time Customer Profile]](../../profile/home.md)。

本文檔介紹在方案註冊表API中與工會合作的基本概念，包括各種操作的示例調用。 有關XDM中的聯合的更多一般資訊，請參見架構構成基 [礎中的聯合部分](../schema/composition.md#union)。

## 聯合架構欄位

The [!DNL Schema Registry] automatically includes three key fields within a union schema: `identityMap`、 `timeSeriesEvents`和 `segmentMembership`。

### 身分圖

聯合模式是聯 `identityMap` 合的關聯記錄模式內已知身份的表示。 標識映射將標識分成由命名空間鍵入的不同陣列。 每個列出的身份本身都是包含唯一值的 `id` 對象。 See the [Identity Service documentation](../../identity-service/home.md) for more information.

### 時間系列事件

數 `timeSeriesEvents` 組是與與聯合相關聯的記錄方案相關的時間序列事件的清單。 將配置檔案資料導出到資料集時，每個記錄都包含此陣列。 這對於各種使用案例都很有用，例如機器學習，其中模型除了記錄屬性外還需要描述檔的整個行為歷史記錄。

### 區段會籍圖

地圖 `segmentMembership` 儲存區段評估的結果。 使用區段API成功執行區段 [作業時](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/segmentation.yaml)，會更新地圖。 `segmentMembership` 此外，還會儲存任何預先評估的受眾細分，這些細分會納入Platform中，以便與其他解決方案（例如Adobe Audience Manager）整合。 如需詳細資訊，請 [參閱使用API建立區段](../../segmentation/tutorials/create-a-segment.md) 的教學課程。

## 檢索工會清單 {#list}

在架構上設 `union` 置標籤時， [!DNL Schema Registry] 會自動將架構添加到架構所基於的類的聯合中。 如果相關類不存在聯合，則會自動建立新聯合。 聯 `$id` 盟的標準與其他資源 `$id` 的 [!DNL Schema Registry] 標準相似，唯一的區別是附加兩個下划線和&quot;union&quot;(`__union`)。

通過向端點發出GET請求，可以查看可用工會的列 `/tenant/unions` 表。

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

回應格式取決於在請求 `Accept` 中傳送的標題。 下列標 `Accept` 題可用於列出工會：

| `Accept` 標題 | 說明 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每個資源的簡短摘要。 這是列出資源的建議標題。 (限制：300) |
| `application/vnd.adobe.xed+json` | 傳回每個資源的完整JSON類別，其中包含 `$ref` 原始 `allOf` 資源。 (限制：300) |

**回應**

成功的響應返回HTTP狀態200(OK)和響 `results` 應主體中的陣列。 如果已定義了聯合，則每個聯合的詳細資訊都作為陣列中的對象提供。 如果尚未定義聯合，則仍會傳回HTTP狀態200（確定），但 `results` 陣列將為空。

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

## 尋找工會 {#lookup}

您可以通過執行GET請求來查看特定的聯合，該請求包括 `$id` 和（取決於「接受」標題），聯合的部分或全部詳細資訊。

>[!NOTE]
>
>聯合查找可使用 `/unions` 和端 `/schemas` 點，以便用於導 [!DNL Profile] 出到資料集。

**API格式**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{UNION_ID}` | 您要尋找 `$id` 的工會的URL編碼URI。 聯合結構描述的URI會附加&quot;__union&quot;。 |

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
| application/vnd.adobe.xed+json;version={MAJOR_VERSION} | Raw搭配 `$ref` 和 `allOf`。 包含標題和說明。 |
| application/vnd.adobe.xed-full+json;version={MAJOR_VERSION} | `$ref` 屬性和已解 `allOf` 決。 包含標題和說明。 |

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

## 為聯合會成員啟用方案 {#enable}

要使架構包含在其類的union中，必須將標 `union` 記添加到架構的屬 `meta:immutableTags` 性。 您可以通過發出PATCH請求，將單 `meta:immutableTags` 個字串值為的陣列添加 `union` 到有關的架構中。 有關詳細 [示例](./schemas.md#union) ，請參見架構端點指南。

## 列出聯合中的結構 {#list-schemas}

為了查看哪些方案屬於特定聯合的一部分，您可以對端點執行GET請 `/tenant/schemas` 求。 使用查 `property` 詢參數，可以將響應配置為僅返回包含欄位和等於您正在訪問其聯 `meta:immutableTags``meta:class` 合的類的方案的方案。

**API格式**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CLASS_ID}` | 您 `$id` 要列出其聯合啟用方案的類。 |

**請求**

以下請求將檢索屬於類聯合的所有方案的列 [!DNL XDM Individual Profile] 表。

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於在請求 `Accept` 中傳送的標題。 列出方 `Accept` 案時，可使用以下標題：

| `Accept` 標題 | 說明 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每個資源的簡短摘要。 這是列出資源的建議標題。 (限制：300) |
| `application/vnd.adobe.xed+json` | 傳回每個資源的完整JSON結構描述，其中包含 `$ref` 原始 `allOf` 資源。 (限制：300) |

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
