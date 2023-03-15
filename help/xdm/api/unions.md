---
keywords: Experience Platform；首頁；熱門主題；API; XDM; XDM系統；體驗資料模型；體驗資料模型；資料模型；結構註冊表；結合；聯合；工會；segmentMembership;timeSeriesEvents;
solution: Experience Platform
title: Union API端點
description: Schema Registry API中的/union端點可讓您以程式設計方式管理體驗應用程式中的XDM聯合結構。
exl-id: d0ece235-72e8-49d9-856b-5dba44e16ee7
source-git-commit: 983682489e2c0e70069dbf495ab90fc9555aae2d
workflow-type: tm+mt
source-wordcount: '896'
ht-degree: 1%

---

# Union端點

聯合（或聯合視圖）是系統生成的只讀架構，用於聚合共用相同類的所有架構的欄位([!DNL XDM ExperienceEvent] 或 [!DNL XDM Individual Profile])和啟用 [[!DNL Real-Time Customer Profile]](../../profile/home.md).

本檔案涵蓋在結構註冊表API中與工會合作的基本概念，包括各種作業的範例呼叫。 如需XDM中工會的更一般資訊，請參閱 [綱要構成基本知識](../schema/composition.md#union).

## 聯合架構欄位

此 [!DNL Schema Registry] 在聯合架構中自動包含三個關鍵欄位： `identityMap`, `timeSeriesEvents`，和 `segmentMembership`.

### 身分對應

聯合方案 `identityMap` 是工會相關記錄結構內已知身分的表示。 身分對應會將身分分割為由命名空間輸入的不同陣列。 所列的每個身分本身都是包含唯一的物件 `id` 值。 請參閱 [Identity服務檔案](../../identity-service/home.md) 以取得更多資訊。

### 時間序列事件

此 `timeSeriesEvents` array是與與聯合關聯的記錄結構相關的時間序列事件清單。 將設定檔資料匯出至資料集時，每筆記錄都會包含此陣列。 這對各種使用案例非常有用，例如機器學習，其中模型除了其記錄屬性外，還需要設定檔的整個行為歷史記錄。

### 區段成員資格對應

此 `segmentMembership` map會儲存區段評估的結果。 區段作業成功執行時，請使用 [區段API](https://www.adobe.io/experience-platform-apis/references/segmentation/)，則會更新地圖。 `segmentMembership` 也會儲存擷取至Platform的任何預先評估對象區段，以便與Adobe Audience Manager等其他解決方案整合。 請參閱 [使用API建立區段](../../segmentation/tutorials/create-a-segment.md) 以取得更多資訊。

## 檢索聯合清單 {#list}

當您設定 `union` 標籤， [!DNL Schema Registry] 自動將架構添加到架構所基於類的聯合。 如果相關類不存在聯合，則會自動建立新聯合。 此 `$id` 適用於聯合的 `$id` 其他 [!DNL Schema Registry] 資源，唯一的差異是附加兩個底線和單字「union」(`__union`)。

您可以向提出GET要求，以檢視可用工會的清單 `/tenant/unions` 端點。

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

回應格式取決於 `Accept` 請求中傳送的標題。 以下 `Accept` 清單工會可使用標題：

| `Accept` 標題 | 說明 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 傳回每個資源的簡短摘要。 這是列出資源的建議標題。 (限制：300) |
| `application/vnd.adobe.xed+json` | 傳回每個資源的完整JSON類別（原始） `$ref` 和 `allOf` 已包含。 (限制：300) |

{style="table-layout:auto"}

**回應**

成功的回應會傳回HTTP狀態200(OK)，並傳回 `results` 陣列。 如果已定義聯合，則每個聯合的詳細資訊將作為陣列內的對象提供。 如果尚未定義聯合，則仍會傳回HTTP狀態200(OK)，但會傳回 `results` 陣列將為空。

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

您可以執行包含 `$id` 和，視Accept標題而定，聯合的部分或全部詳細資訊。

>[!NOTE]
>
>聯合查閱可使用 `/unions` 和 `/schemas` 端點啟用，以用於 [!DNL Profile] 匯出至資料集。

**API格式**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{UNION_ID}` | URL編碼 `$id` 你要查的聯盟的URI。 聯合架構的URI會附加「__union」。 |

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

聯合查詢請求需要 `version` 包含在接受標題中。

下列「接受」標題適用於聯合架構查閱：

| Accept | 說明 |
| -------|------------ |
| `application/vnd.adobe.xed+json; version=1` | 原始格式 `$ref` 和 `allOf`. 包含標題和說明。 |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 屬性和 `allOf` 已解決。 包含標題和說明。 |

{style="table-layout:auto"}

**回應**

成功的回應會傳回實作類別之所有架構的聯合檢視 `$id` 是在要求路徑中提供。

回應格式取決於要求中傳送的Accept標題。 嘗試不同的「接受」標題來比較回應，並判斷哪個標題最適合您的使用案例。

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

## 啟用聯合成員資格的結構 {#enable}

為了將架構包含在其類別的聯合中， `union` 標籤必須新增至架構的 `meta:immutableTags` 屬性。 您可以發出PATCH要求來新增 `meta:immutableTags` 單字串值為 `union` 到有關的方案。 請參閱 [schemas endpoint指南](./schemas.md#union) 以取得詳細範例。

## 列出聯合的結構 {#list-schemas}

若要查看哪些結構屬於特定聯合的一部分，您可以對 `/tenant/schemas` 端點。 使用 `property` 查詢參數，您可以將回應設定為僅傳回包含 `meta:immutableTags` 欄位和 `meta:class` 等於您要存取其聯合的類別。

**API格式**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CLASS_ID}` | 此 `$id` 要列出其聯合啟用結構的類。 |

{style="table-layout:auto"}

**要求**

下列請求會擷取屬於 [!DNL XDM Individual Profile] 類別。

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於 `Accept` 請求中傳送的標題。 以下 `Accept` 標題可用於列出結構：

| `Accept` 標題 | 說明 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 傳回每個資源的簡短摘要。 這是列出資源的建議標題。 (限制：300) |
| `application/vnd.adobe.xed+json` | 傳回每個資源的完整JSON結構（原始） `$ref` 和 `allOf` 已包含。 (限制：300) |

{style="table-layout:auto"}

**回應**

成功的響應返回一個已篩選的架構清單，該清單僅包含屬於已啟用聯合成員資格的指定類的架構。 請記住，使用多個查詢參數時，會假設為AND關係。

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
