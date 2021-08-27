---
keywords: Experience Platform；首頁；熱門主題；API; XDM; XDM系統；體驗資料模型；體驗資料模型；資料模型；結構註冊表；結合；聯合；工會；segmentMembership;timeSeriesEvents;
solution: Experience Platform
title: Union API端點
description: Schema Registry API中的/union端點可讓您以程式設計方式管理體驗應用程式中的XDM聯合結構。
topic-legacy: developer guide
exl-id: d0ece235-72e8-49d9-856b-5dba44e16ee7
source-git-commit: 5160bc8057a7f71e6b0f7f2d594ba414bae9d8f6
workflow-type: tm+mt
source-wordcount: '911'
ht-degree: 3%

---

# Union端點

聯合（或聯合視圖）是系統生成的只讀架構，用於聚合共用相同類（[!DNL XDM ExperienceEvent]或[!DNL XDM Individual Profile]）且為[[!DNL Real-time Customer Profile]](../../profile/home.md)啟用的所有架構的欄位。

本檔案涵蓋在結構註冊表API中與工會合作的基本概念，包括各種作業的範例呼叫。 有關XDM中聯合的更一般資訊，請參閱[架構組成基礎](../schema/composition.md#union)中有關聯合的一節。

## 聯合架構欄位

[!DNL Schema Registry]會自動在聯合架構中包含三個鍵欄位：`identityMap`、`timeSeriesEvents`和`segmentMembership`。

### 身分對應

聯合架構的`identityMap`表示聯合的相關記錄架構內的已知身份。 身分對應會將身分分割為由命名空間輸入的不同陣列。 所列的每個身分本身都是包含唯一`id`值的物件。 如需詳細資訊，請參閱[Identity Service檔案](../../identity-service/home.md)。

### 時間序列事件

`timeSeriesEvents`陣列是與與聯合關聯的記錄架構相關的時間序列事件清單。 將設定檔資料匯出至資料集時，每筆記錄都會包含此陣列。 這對各種使用案例非常有用，例如機器學習，其中模型除了其記錄屬性外，還需要設定檔的整個行為歷史記錄。

### 區段成員資格對應

`segmentMembership`地圖會儲存區段評估的結果。 使用[分段API](https://www.adobe.io/experience-platform-apis/references/segmentation/)成功執行區段作業時，會更新對映。 `segmentMembership` 也會儲存擷取至Platform的任何預先評估對象區段，以便與Adobe Audience Manager等其他解決方案整合。如需詳細資訊，請參閱[使用API建立區段的教學課程。](../../segmentation/tutorials/create-a-segment.md)

## 檢索聯合清單 {#list}

在架構上設定`union`標籤時， [!DNL Schema Registry]會自動將架構添加到架構所基於類的聯合中。 如果相關類不存在聯合，則會自動建立新聯合。 聯合的`$id`與其他[!DNL Schema Registry]資源的標準`$id`類似，唯一的差異是由兩個底線附加，並加上&quot;union&quot;(`__union`)。

您可以向`/tenant/unions`端點提出GET請求，以查看可用聯合的清單。

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
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed-id+json'
```

回應格式取決於要求中傳送的`Accept`標題。 下列`Accept`標題可用於清單聯合：

| `Accept` 標題 | 說明 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 傳回每個資源的簡短摘要。 這是列出資源的建議標題。 (限制：300) |
| `application/vnd.adobe.xed+json` | 傳回每個資源的完整JSON類別，並包含原始的`$ref`和`allOf`。 (限制：300) |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的回應會傳回HTTP狀態200(OK)，以及回應內文中的`results`陣列。 如果已定義聯合，則每個聯合的詳細資訊將作為陣列內的對象提供。 如果未定義聯合，則仍會返回HTTP狀態200(OK)，但`results`陣列將為空。

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

您可以執行包含`$id`的GET請求，並根據Accept標題查看聯合的部分或全部詳細資訊，以查看特定聯合。

>[!NOTE]
>
>聯集查閱可使用`/unions`和`/schemas`端點，以便在[!DNL Profile]匯出至資料集時使用。

**API格式**

```http
GET /tenant/unions/{UNION_ID}
GET /tenant/schemas/{UNION_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{UNION_ID}` | 要查找的聯合的URL編碼的`$id` URI。 聯合架構的URI會附加「__union」。 |

{style=&quot;table-layout:auto&quot;}

**要求**

```SHELL
curl -X GET \
  https://platform.adobe.io/data/foundation/schemaregistry/tenant/unions/https%3A%2F%2Fns.adobe.com%2Fxdm%2Fcontext%2Fprofile__union \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Accept: application/vnd.adobe.xed+json; version=1'
```

聯合查詢請求需要在Accept標題中包含`version`。

下列「接受」標題適用於聯合架構查閱：

| Accept | 說明 |
| -------|------------ |
| `application/vnd.adobe.xed+json; version=1` | 具有`$ref`和`allOf`的原始。 包含標題和說明。 |
| `application/vnd.adobe.xed-full+json; version=1` | `$ref` 屬性和已 `allOf` 解析。包含標題和說明。 |

{style=&quot;table-layout:auto&quot;}

**回應**

成功的回應會傳回實作要求路徑中提供`$id`類別之所有結構的聯合檢視。

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

若要將架構納入其類別的聯合中，必須將`union`標籤新增至架構的`meta:immutableTags`屬性。 您可以發出PATCH要求，將單字串值`union`的`meta:immutableTags`陣列新增至相關架構，以達到此目的。 如需詳細範例，請參閱[綱要端點指南](./schemas.md#union)。

## 列出聯合的結構 {#list-schemas}

若要查看哪些結構屬於特定聯合的一部分，您可以對`/tenant/schemas`端點執行GET請求。 使用`property`查詢參數，可以將響應配置為僅返回包含`meta:immutableTags`欄位和`meta:class`等於您正在訪問其聯合的類的架構。

**API格式**

```http
GET /tenant/schemas?property=meta:immutableTags==union&property=meta:class=={CLASS_ID}
```

| 參數 | 說明 |
| --- | --- |
| `{CLASS_ID}` | 要列出其聯合啟用架構的類的`$id`。 |

{style=&quot;table-layout:auto&quot;}

**要求**

下列請求會擷取屬於[!DNL XDM Individual Profile]類別聯合的所有結構清單。

```SHELL
curl -X GET \
  'https://platform.adobe.io/data/foundation/schemaregistry/tenant/schemas?property=meta:immutableTags==union&property=meta:class==https://ns.adobe.com/xdm/context/profile' \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

回應格式取決於要求中傳送的`Accept`標題。 下列`Accept`標題可用於列出結構：

| `Accept` 標題 | 說明 |
| --- | --- |
| `application/vnd.adobe.xed-id+json` | 傳回每個資源的簡短摘要。 這是列出資源的建議標題。 (限制：300) |
| `application/vnd.adobe.xed+json` | 傳回每個資源的完整JSON結構，並包含原始的`$ref`和`allOf`。 (限制：300) |

{style=&quot;table-layout:auto&quot;}

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
