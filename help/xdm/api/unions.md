---
keywords: Experience Platform；主題；熱門主題；api;API;XDM;XDM系統；體驗資料模型；體驗資料模型；資料模型；資料模型；資料模型；架構註冊；架構註冊；聯合；聯合；聯合；段成員；時間系列事件；
solution: Experience Platform
title: 聯合API終結點
description: 通過架構註冊表API中的/unions終結點，可以以寫程式方式管理您的體驗應用程式中的XDM聯合架構。
exl-id: d0ece235-72e8-49d9-856b-5dba44e16ee7
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 1%

---

# 聯合終結點

聯合（或聯合視圖）是系統生成的只讀模式，用於聚合共用同一類的所有架構的欄位([!DNL XDM ExperienceEvent] 或 [!DNL XDM Individual Profile])，並啟用 [[!DNL Real-Time Customer Profile]](../../profile/home.md)。

本文檔介紹與架構註冊表API中的工會協作的基本概念，包括各種操作的示例調用。 有關XDM中工會的更多一般資訊，請參見中有關工會的章節 [架構組合基礎](../schema/composition.md#union)。

## 聯合架構欄位

的 [!DNL Schema Registry] 自動包括聯合架構中的三個關鍵字： `identityMap`。 `timeSeriesEvents`, `segmentMembership`。

### 身份映射

聯合架構 `identityMap` 是聯合的關聯記錄架構中已知標識的表示。 標識映射將標識分隔為由命名空間鍵控的不同陣列。 每個列出的標識本身都是包含唯一標識的對象 `id` 值。 查看 [Identity Service文檔](../../identity-service/home.md) 的子菜單。

### 時間系列事件

的 `timeSeriesEvents` array是與與union關聯的記錄架構相關的時間序列事件的清單。 將配置檔案資料導出到資料集時，每個記錄都包括此陣列。 這對於各種使用情形（如機器學習）非常有用，在機器學習中，模型除了需要記錄屬性外還需要配置檔案的整個行為歷史記錄。

### 段成員資格映射

的 `segmentMembership` map儲存段評估的結果。 使用 [分段API](https://www.adobe.io/experience-platform-apis/references/segmentation/)，將更新映射。 `segmentMembership` 還儲存所有預評估的受眾群，這些受眾群被攝取到平台中，從而可以與Adobe Audience Manager等其他解決方案整合。 請參閱上的教程 [使用API建立段](../../segmentation/tutorials/create-a-segment.md) 的子菜單。

## 檢索聯合清單 {#list}

設定 `union` 在架構上標籤， [!DNL Schema Registry] 自動將模式添加到基於該模式的類的聯合中。 如果所涉類不存在聯合，則會自動建立新的聯合。 的 `$id` 因為工會和標準 `$id` 其他 [!DNL Schema Registry] 資源，唯一的區別是用兩個下划線和單詞&quot;union&quot;(`__union`)。

您可以通過向以下站點發出GET請求來查看可用工會清單 `/tenant/unions` 端點。

**API格式**

```http
GET /tenant/unions
```

**要求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

響應格式取決於 `Accept` 請求中發送的標頭。 以下 `Accept` 標題可用於清單聯合：

| `Accept` 標題 | 說明 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每個資源的簡短摘要。 這是列出資源的建議標頭。 (限制：300) |
| `application/vnd.adobe.xed+json` | 為每個資源返回完整的JSON類，原始 `$ref` 和 `allOf` 包含。 (限制：300) |

{style="table-layout:auto"}

**回應**

成功響應返回HTTP狀態200(OK)和 `results` 陣列。 如果定義了聯合，則每個聯合的詳細資訊都作為陣列中的對象提供。 如果尚未定義聯合，則仍返回HTTP狀態200（確定），但 `results` 陣列將為空。

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

## 查找工會 {#lookup}

您可以通過執行包含以下項的GET請求來查看特定聯合 `$id` 和（取決於「接受」標題），以及聯合的部分或全部詳細資訊。

>[!NOTE]
>
>聯合查找可使用 `/unions` 和 `/schemas` 使用端點 [!DNL Profile] 導出到資料集。

**API格式**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{UNION_ID}` | URL編碼 `$id` 要查找的聯盟的URI。 聯合架構的URI將附加「__union」。 |

{style="table-layout:auto"}

**要求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile__union \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

聯合查找請求需要 `version` 包含在「接受」標題中。

以下「接受」標頭可用於聯合架構查找：

| Accept | 說明 |
| -------|------------ |
| `application/vnd.adobe.xed+json; version=1` | 原始 `$ref` 和 `allOf`。 包括標題和說明。 |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 屬性和 `allOf` 已解決。 包括標題和說明。 |

{style="table-layout:auto"}

**回應**

成功的響應返回實現其類的所有架構的聯合視圖 `$id` 在請求路徑中提供。

響應格式取決於請求中發送的「接受」標頭。 使用不同的「接受」標頭進行實驗，以比較響應並確定哪個標頭最適合您的使用情形。

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

## 啟用聯合成員身份的架構 {#enable}

為了將架構包含在其類的聯合中， `union` 必須將標籤添加到架構 `meta:immutableTags` 屬性。 通過發出PATCH請求以添加 `meta:immutableTags` 單字串值為 `union` 到有關的架構。 查看 [架構終結點指南](./schemas.md#union) 的上界。

## 列出聯合中的架構 {#list-schemas}

為了查看哪些架構是特定聯合的一部分，您可以向 `/tenant/schemas` 端點。 使用 `property` 查詢參數，可以將響應配置為僅返回包含 `meta:immutableTags` 和 `meta:class` 等於您要訪問其聯合的類。

**API格式**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CLASS_ID}` | 的 `$id` 要列出其聯合啟用架構的類。 |

{style="table-layout:auto"}

**要求**

以下請求將檢索作為聯合的一部分的所有架構的清單 [!DNL XDM Individual Profile] 類。

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

響應格式取決於 `Accept` 請求中發送的標頭。 以下 `Accept` 標題可用於清單架構：

| `Accept` 標題 | 說明 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 返回每個資源的簡短摘要。 這是列出資源的建議標頭。 (限制：300) |
| `application/vnd.adobe.xed+json` | 為每個資源返回完整的JSON架構（原始） `$ref` 和 `allOf` 包含。 (限制：300) |

{style="table-layout:auto"}

**回應**

成功的響應返回篩選的方案清單，其中只包含屬於已啟用聯合成員資格的指定類的方案。 請記住，當使用多個查詢參數時，會假定AND關係。

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
